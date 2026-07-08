# Rediseño UX — Ontop Campaign Hub

**Brief de implementación para Sonnet.**
Objetivo: reestructurar la *arquitectura de información* y la *legibilidad* de la app, **sin tocar la lógica de estrategias, generación de copy, reglas de producto ni las integraciones** (GitHub, Sheets, Claude API).

La app es un único archivo: `index.html` (~2.600 líneas, HTML+CSS+JS vanilla, sin build). Se despliega en Vercel como estático. **Mantener el enfoque de un solo archivo** — no introducir frameworks ni pasos de build.

---

## 0. Resumen ejecutivo del cambio

Hoy la navegación tiene **dos ejes que compiten**: un sidebar que cambia de *cliente* y una barra superior de *7 pasos*. El usuario se pierde ("¿en qué track estoy?, ¿este paso ya lo hice?"), la información es densa y de bajo contraste, y no hay una vista global de arranque.

El rediseño adopta un modelo mental claro de **3 niveles**:

```
HOME (dashboard global)  →  CLIENTE (workspace)  →  TRACK (flujo lineal)
```

- Los **7 pasos actuales** se reagrupan: 3 de ellos no son "por track" y se sacan del flujo.
- Aparece un **Home / dashboard** como pantalla de arranque (hoy "Portafolio", enriquecido).
- Una **barra de contexto persistente** (breadcrumb + estado) resuelve el "no sé dónde estoy".
- Un **sistema visual** con contraste AA y tipografía legible resuelve el "cuesta leer".

Prioridades del usuario (en orden): **(1) orientación, (2) legibilidad, (3) vista global.**

---

## 1. Lo que NO se debe tocar (guardrails)

Romper cualquiera de estos puntos invalida el trabajo. Son datos y lógica de negocio, no UX.

- **Claves de `localStorage`** — no renombrar ni cambiar formato. Hay datos reales guardados:
  - `ontop_api_key`, `ontop_github_token`
  - `statusKey` / `getStatus` / `saveStatus` (líneas ~794-796) → guarda las cadenas de email/WhatsApp por cliente+track+idioma.
  - `ciclosKey` / `getCiclos` / `saveCiclos` (~797-799) → resultados por ciclo.
  - `snapshotKey` (~2408) → snapshots mensuales de Sheets.
- **Modelo de datos bilingüe**: `emails_en` / `emails_es` y los helpers `chainOf` / `hasContent` / `contentCount` (402-415). La app genera EN+ES siempre; eso se conserva.
- **Integración GitHub**: objeto `GITHUB` (423), `MD_FILES` (430), `ghRead`/`ghWrite`/`loadMd`/`appendCicloToMd`/`updateProximoCicloMd` (487-608). Rutas de los `.md` intactas.
- **Integración Sheets**: `syncSheets`, `applySnapshotToClients`, `getAutoMigraciones`, `checkMonthlySync` (2450-2585).
- **Prompts y reglas de producto**: `buildSystem` (613), el `sys` de `editarEstrategiaConIA` (2026) y de `diagnosticarCiclo`. Contienen reglas inviolables (Card standalone, Future Fund Flex/+30, Quick solo Ridetechnology con Legal, Reserve solo Power Users, nombres de tiers solo internos). **No editar el contenido de estos prompts.**
- **Lógica de generación y parsing**: `generateTrack`, `genOne`, `parseChain`, `parseWhatsApp`, `parseAll`, `callClaude`, `callClaudeChat`.
- **Datos de negocio**: objeto `CLIENTS` (329), `PSYCH`, `FRAMEWORKS`, `TONES`, `CHANNELS`. Se pueden *re-presentar* visualmente, pero los valores no cambian.
- **Exportación Word**: `exportClientDoc` (1366) y el `fullHtml` con namespaces de Office.

Regla general: este rediseño reorganiza **cómo se navega y se ve** la información. La lógica que produce esa información se mantiene idéntica.

---

## 2. Diagnóstico — problemas actuales (con evidencia en el código)

### 2.1 Orientación — "no sé dónde estoy"
- **Doble eje de navegación** sin ancla común: `setClient` (804) cambia cliente en el sidebar; `goStep`/`activateStep` (813-833) cambian el paso en la topbar. En ningún lugar persistente se ve *cliente + track + paso* juntos.
- **El track (unidad real de trabajo) está enterrado.** Se entra a un track desde tarjetas dentro del paso 1 (`tierBar`, 842) o desde selectores intermedios. La variable `S.track` puede ser `null` o un objeto, y **cada paso renderiza dos pantallas distintas según eso** (ej. `renderEdit` 1241: si no hay track muestra lista; si hay, muestra edición). Esa dualidad desorienta.
- **El stepper miente sobre el progreso.** `activateStep` (813) marca como "done" todo paso con `i < n`, sea o no que se hizo. Saltar al paso 6 pinta 1-5 como completados aunque nunca se generó nada.
- **"Estrategia" existe dos veces**: como *vista* del sidebar → `renderEstrategia` (2104, chat genérico) y como *paso 7* → `renderEstrategiaCliente` (1935, .md + chat del cliente). Comparten `S.chatHistory`, así que el contexto se mezcla entre ambas.

### 2.2 Legibilidad — "cuesta leer la info"
- **Contraste por debajo de WCAG AA.** El token `--text3:#5a5550` sobre `--bg:#0e0f0f` (línea 9) da ~2.6:1 (AA exige 4.5:1 para texto normal). Y `--text3` se usa por todos lados: labels, `msub`, `email-num`, subtítulos, estados de conexión.
- **Tipografía muy pequeña.** Abundan `font-size:10px` y `11px` en labels, chips, monoespaciado y subtítulos (`.mlabel`, `.clabel`, `.flabel`, `.msub`, `.email-num`, etc.). Mucho por debajo del mínimo cómodo (12-13px).
- **Densidad alta.** Grids de 4-5 columnas de métricas + varias tarjetas apiladas + `DM Mono` para texto descriptivo. La jerarquía visual es plana: título de sección, título de tarjeta y valores compiten por atención.
- **Exceso de monoespaciado.** `DM Mono` es correcto para números/llaves, pero se usa también para frases (`msub`, indicadores), lo que reduce legibilidad a tamaño pequeño.

### 2.3 Vista global — "falta panorama"
- El arranque (`init` → `goStep(1)`, 2586) cae directo en **un cliente** (Edtech, paso 1), no en un panorama.
- Existe `renderPortfolio` (2244) pero está escondido como una "vista" secundaria y **no muestra el estado operativo** de cada cliente (cuántos tracks generados/enviados, avance vs target); solo bucket dominante y MRR.

---

## 3. Nueva arquitectura de información (modelo objetivo)

### 3.1 Modelo mental
```
┌─ HOME ─────────────────────────────────────────────┐
│  Dashboard global: los 4 clientes de un vistazo,    │
│  su estado operativo y el mix hacia el +$500/mes.   │
└───────────────┬─────────────────────────────────────┘
                │ clic en un cliente
┌───────────────▼─ CLIENTE (workspace) ───────────────┐
│  Tabs de nivel cliente:                              │
│   • Resumen   (métricas + lista de tracks)           │
│   • Estrategia (.md + chat)   ← reemplaza paso 7     │
│   • Ajustes de generación     ← reemplaza "Skills"   │
└───────────────┬─────────────────────────────────────┘
                │ clic en un track
┌───────────────▼─ TRACK (flujo lineal real) ─────────┐
│  Stepper propio del track, con estado VERDADERO:     │
│   1 Generar → 2 Editar → 3 Status → 4 Resultados     │
│  Sub-header fijo: Cliente · Track X — ruta · EN/ES   │
└──────────────────────────────────────────────────────┘
```

### 3.2 Mapa: dónde va cada uno de los 7 pasos actuales

| Paso actual | Destino en el nuevo modelo |
|---|---|
| 1 · Resumen | **Tab "Resumen" del cliente** (default al entrar al cliente) |
| 2 · Skills | **Tab "Ajustes de generación" del cliente** (es config global del cliente, no del track) |
| 3 · Generar | **Paso 1 del flujo de track** |
| 4 · Editar | **Paso 2 del flujo de track** |
| 5 · Status | **Paso 3 del flujo de track** |
| 6 · Resultados | **Paso 4 del flujo de track** |
| 7 · Estrategia | **Tab "Estrategia" del cliente** (unificar con la vista de sidebar) |

Resultado: el "stepper" pasa de 7 pasos ambiguos a **4 pasos reales por track**, y lo que no es por-track (config y estrategia) se vuelve tab de cliente.

### 3.3 Sidebar nuevo (simplificado)
```
Ontop Hub
─────────────
◎  Home                     ← nuevo, es el arranque
─────────────
CLIENTES
●  Edtech Plus     ▓▓▓░  ← mini-indicador de progreso REAL (no solo color de marca)
●  Toloka AI       ▓░░░
●  Ridetechnology  ░░░░
●  Nebius          ▓▓░░
─────────────
CONEXIONES
●  Claude API          lista
●  GitHub (.md)        sync ✓
●  Google Sheets       snapshot ✓
⚙  Configurar conexiones
─────────────
?  Cómo funciona el hub
```
- Se elimina la sección "Vistas" (Portafolio → Home; Estrategia → tab de cliente).
- "Skills activos" (badges decorativos PSY/EMAIL/ADS/MKT) se quita del sidebar; si se quiere conservar, va como nota discreta en el Home o en la ayuda. No es navegación.
- El punto de cada cliente deja de ser solo color de marca y refleja **estado**: p. ej. gris = sin actividad, ámbar = en progreso, verde = ciclo completo. (Reusar la lógica de `hasContent`/`getCiclos` que ya existe.)

---

## 4. Sistema visual / legibilidad

Definir tokens que cumplan **WCAG AA** y una escala tipográfica. Cambiar en el bloque `:root` (línea 9) y propagar.

### 4.1 Color de texto (antes → después)
| Token | Antes | Después | Contraste s/ `--bg` | Uso |
|---|---|---|---|---|
| `--text`  | `#f0ede8` | `#f2efea` (igual, ok) | ~15:1 | Texto principal, valores |
| `--text2` | `#9a9590` | `#b3aea7` | ~9:1 | Texto secundario, descripciones |
| `--text3` | `#5a5550` | `#8f8981` | ~5.2:1 (AA ✓) | Labels, metadatos — **solo cuando deba leerse** |
| `--text-faint` | — | `#5a5550` | decorativo | Separadores/placeholders NO informativos |

Regla: **ningún texto que el usuario deba leer usa un color por debajo de 4.5:1.** El gris más oscuro queda solo para elementos puramente decorativos.

### 4.2 Escala tipográfica (mínimos)
- Cuerpo/base: **14px** (hoy 13px).
- Labels de sección/campo: **12px** mínimo (hoy 10-11px). `text-transform:uppercase` + `letter-spacing` se conserva.
- Chips/tags: **11px** mínimo.
- Valores de métrica (`.mval`): mantener grande (Syne), pero garantizar `line-height` y espacio.
- **Reducir `DM Mono`** a números, llaves y datos tabulares. El texto descriptivo pasa a `DM Sans`.

### 4.3 Densidad y jerarquía
- Grids de métricas: máximo **3 columnas** en desktop para los paneles de cliente (hoy `mgrid` usa 4). El Home puede usar tabla/lista.
- Subir padding de `.card` (hoy 18px) y el ritmo vertical entre bloques; menos tarjetas visibles a la vez, más aire.
- Jerarquía explícita por tamaño y color: **título de sección** (Syne, `--text`) > **título de tarjeta** > **label** (`--text3`, 12px) > **valor** (`--text`). Que no compitan.
- Mantener el tema oscuro y la identidad (acento lima `--accent:#c8f04a`); esto es refinamiento, no rebranding.

### 4.4 Accesibilidad (conservar y reforzar)
- Ya existen `:focus-visible` y `prefers-reduced-motion` (164-165) — conservarlos y extenderlos a los nuevos elementos interactivos (tabs, breadcrumb, tarjetas clicables).
- Las tarjetas clicables (`clirow`, tracks) deben ser focusables por teclado (`tabindex`, `role="button"`, Enter/Espacio), no solo `onclick`.

---

## 5. Orientación permanente — barra de contexto ("dónde estoy")

Elemento **nuevo y central** para la prioridad #1. Una barra fija arriba del panel, siempre visible, que refleja el nivel actual:

- En Home: `Home`
- En cliente: `Home / Edtech Plus` + tabs (Resumen · Estrategia · Ajustes)
- En track: `Home / Edtech Plus / Track B — Explorer→Builder` + stepper del track + toggle `EN/ES`

Requisitos:
- Cada segmento del breadcrumb es **clicable** para subir de nivel (Home ← Cliente ← Track).
- Muestra siempre el **idioma en edición** (`S.viewLang`) cuando aplica.
- El **stepper del track refleja estado real**, no posicional:
  - Generar: "done" si `hasContent(getStatus(client,track))`.
  - Editar: disponible si hay contenido.
  - Status: badge `X/Y enviados` desde la cadena.
  - Resultados: "done" si `getCiclos(client,track).length > 0`.
- Reemplazar la lógica `i < n` de `activateStep` (813) por estos chequeos reales.

Esto elimina la necesidad de los mini-selectores de track intermedios (`trackSwitcher`, 1354) porque el contexto ya vive en la barra; se puede conservar `trackSwitcher` como cambio rápido entre tracks *dentro* del flujo.

---

## 6. Home / Dashboard global (spec)

Reemplaza a `renderPortfolio` como **pantalla de arranque** (`init` debe abrir Home, no un cliente). Reusa sus métricas y añade estado operativo por cliente.

**Contenido:**
1. **KPIs globales** (fila superior, máx 4): Total workers (de snapshot si existe), MRR B2C, PES baseline, Target `+$500`. (Ya están en `renderPortfolio` 2276-2283.)
2. **Tabla/lista de clientes** — una fila por cliente, legible, con:
   - Nombre + punto de estado real.
   - Bucket predominante + % (ya calculado, 2250-2260).
   - **Tracks:** `generados/total` y `completos` (nuevo — derivar de `hasContent` y ciclos).
   - **Avance del ciclo:** migraciones logradas vs target agregado del cliente (barra).
   - MRR y aporte al target.
   - Clic → workspace del cliente.
3. **Mix del target** (cómo se arma el +$500) — ya existe (2288-2297), conservar pero con la tipografía nueva.
4. **Economics de rutas** — ya existe (2299-2303), conservar.

El Home es de **lectura rápida**: el usuario entiende en 5 segundos qué cliente necesita atención.

---

## 7. Workspace de cliente (spec)

Al elegir un cliente (desde Home o sidebar), se entra a su workspace con **tabs de nivel cliente** bajo el breadcrumb:

### Tab "Resumen" (default) — base: `renderBrief` (838)
- Banner de setup si faltan llaves (ya existe, 915-919) — conservar.
- KPIs del cliente en **3 columnas** (Workers, Bucket predominante, MRR/Contrato).
- **Lista de tracks** (base `tierBar`, 842) rediseñada para leerse mejor: por track, un renglón claro con label, prioridad, workers, target, migraciones y **estado** (Sin generar / Generado / Enviado X/Y / N ciclos). Clic en el track → abre su flujo (paso Generar o Editar según tenga contenido).
- Quitar la "Configuración general de generación" embebida al final (938-951): eso ahora vive en el tab "Ajustes".

### Tab "Ajustes de generación" — base: `renderSkills` (1079)
- Es **configuración del cliente que aplica a todos sus tracks** (dejarlo explícito con un subtítulo). Contenido igual: Canales, aviso de idioma EN+ES, Framework, Psicología (chips con tooltip), Tono, Contexto adicional (`extra-ctx`), y el resumen "Configuración activa".
- El botón de acción ya no dice "Generar" aquí; genera desde el track. Este tab solo **configura**.

### Tab "Estrategia" — base: `renderEstrategiaCliente` (1935)
- Sub-tabs existentes: **Estrategia (.md)** (visor + editar-con-IA, 1989) y **Chat de estrategia** (2086).
- **Unificar** aquí la vista de sidebar `renderEstrategia` (2104): eliminar la entrada duplicada del sidebar y que toda la estrategia sea a nivel cliente. Esto también corrige la mezcla de `S.chatHistory` entre ambas.

---

## 8. Flujo por track (spec)

Al seleccionar un track, se abre su **flujo lineal de 4 pasos** con el sub-header de contexto (Cliente · Track — ruta · EN/ES · volver).

1. **Generar** — base `renderGenerate` (1153). Usa los Ajustes del cliente. Progreso por track (ya existe). Al terminar, avanza a Editar.
2. **Editar** — base `renderEdit` (1241, modo individual). Tarjetas de email/WhatsApp, edición manual o con IA, toggle EN/ES, export Word.
3. **Status** — base `renderStatus` (1538). Marcar enviados.
4. **Resultados** — base `renderResultados` (1630). Registrar ciclo, estado de tiers desde Sheets, diagnóstico con IA, empujar a `.md`.

Notas:
- Como el contexto (cliente/track) ahora es persistente, las **pantallas "sin track" de cada paso** (las listas selectoras dentro de `renderEdit`/`renderStatus`/`renderResultados`) dejan de ser el modo por defecto: la selección de track ocurre en el Resumen del cliente. Se pueden conservar como fallback, pero el camino principal entra ya con `S.track` definido.
- `S.track` nunca debería quedar en un estado ambiguo dentro del flujo; el breadcrumb es la fuente de verdad.

---

## 9. Conexiones y estados (spec)

- Consolidar la lectura de estado: hoy los dots viven en 3 sitios (sidebar `conn-row`, topbar `periodo-indicator`, y modal). `refreshConnStates` (2344) ya centraliza la lógica — conservarla.
- Mejorar **legibilidad del estado**: además del dot, texto claro (`lista` / `falta key` / `sync ✓` / `cargando` / `sin datos`) a 12px con contraste AA. Evitar depender solo del color (accesibilidad).
- El modal de conexiones (267-300) se conserva tal cual funcional; solo aplica el nuevo sistema tipográfico.
- Mantener el mensaje de privacidad ("las llaves se guardan solo en este navegador").

---

## 10. Plan de implementación por fases (construir sin romper)

Aunque el alcance es restructura completa, conviene construir en este orden para poder verificar en cada paso y no romper datos:

- **Fase A — Sistema visual (aislado, bajo riesgo).**
  Aplicar tokens de color, escala tipográfica y densidad (Sección 4). No cambia navegación. Verificable de inmediato: la app se lee mejor y todo sigue funcionando.

- **Fase B — Barra de contexto + stepper real.**
  Introducir breadcrumb persistente (Sección 5) y reemplazar el "done" posicional de `activateStep` por estado real. Aún con los 7 pasos, pero ya orientado.

- **Fase C — Home como arranque.**
  Enriquecer `renderPortfolio` con estado operativo y hacer que `init` abra Home (Sección 6). Añadir "Home" al sidebar.

- **Fase D — Reagrupar navegación (el corazón del rediseño).**
  Convertir Skills→tab Ajustes, Estrategia→tab cliente (unificando la de sidebar), y colapsar Generar/Editar/Status/Resultados en el flujo de 4 pasos por track (Secciones 3, 7, 8). Simplificar el sidebar.

- **Fase E — Pulido.**
  Accesibilidad de teclado en tarjetas, responsive del nuevo layout, microcopy consistente (idioma), limpieza de duplicados.

Cada fase debe dejar la app **funcional y desplegable**. Commit por fase.

---

## 11. Criterios de aceptación / QA

Orientación:
- [ ] En cualquier pantalla se ve *cliente + track + paso* sin adivinar (breadcrumb).
- [ ] El stepper del track refleja estado real (nada de "done" falso).
- [ ] "Estrategia" existe en un solo lugar (tab de cliente); no hay dos chats con contexto cruzado.

Legibilidad:
- [ ] Ningún texto informativo por debajo de contraste 4.5:1 (validar `--text3` nuevo).
- [ ] Ningún texto informativo por debajo de 12px.
- [ ] Máx 3 columnas de métricas en paneles de cliente; `DM Mono` solo para datos numéricos.

Vista global:
- [ ] La app arranca en Home con los 4 clientes y su estado operativo visible.
- [ ] Desde Home se llega a cualquier cliente/track en ≤2 clics.

Integridad (regresión — debe seguir intacto):
- [ ] Generar EN+ES, editar (manual e IA), marcar enviados, registrar ciclo y diagnóstico funcionan igual.
- [ ] `loadMd`, `syncSheets`, editar y guardar `.md` en GitHub funcionan igual.
- [ ] Export Word (`exportClientDoc`) funciona igual.
- [ ] Datos previos en `localStorage` (cadenas, ciclos, snapshots, llaves) se leen sin migración.
- [ ] Los prompts y reglas de producto no cambiaron.

Responsive/A11y:
- [ ] El nuevo layout funciona en móvil (breakpoint 860px ya existe).
- [ ] Tarjetas y tabs navegables por teclado con foco visible.

---

## 12. Notas técnicas

- **Un solo archivo.** Todo el CSS en el `<style>` (7-185) y todo el JS en el `<script>` (325-2597). No dividir.
- **Router simple.** Hoy la "navegación" es imperativa (`setClient`/`goStep` reescriben `#panel`). El nuevo modelo puede seguir igual: una función que pinta Home / cliente(tab) / track(paso) según un estado de vista. Sugerencia: extender `S` con `S.view` (`'home' | 'client' | 'track'`) y `S.clientTab` (`'resumen' | 'estrategia' | 'ajustes'`) y `S.trackStep` (1-4), y un único `render()` que despacha. Conservar los `render*` existentes como los cuerpos de cada vista.
- **No romper `S`.** Añadir campos nuevos, no renombrar los existentes (`client`, `track`, `viewLang`, `channels`, `psych`, `framework`, `tone`, `extraCtx`, `emailChain`, `campaignMd`, `mdLoaded`, `chatHistory`).
- **Idioma de la UI:** consistente en español (hoy hay mezcla ES/EN en labels como "Skills", "Status"). Renombrar labels visibles a español claro ("Ajustes de generación", "Estado de envío", etc.). El *contenido generado* sigue siendo EN+ES.

---

*Fin del brief. Implementar por fases (Sección 10); cada fase es un commit desplegable.*
