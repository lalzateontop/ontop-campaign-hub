# Contexto para Campaña de Trade Marketing — Migración de Workers entre Segmentos PES

**Owner:** Luis Miguel Alzate (Senior CSM, Sole Provider)
**Stakeholders:** VP Customer Success, equipo CS, equipo Marketing, equipo Producto
**Periodo objetivo:** Q2–Q4 2026
**Última actualización:** Mayo 2026

---

## 1. Objetivo de la campaña

Diseñar una campaña de trade marketing interna dirigida a los **clientes B2B del portafolio de Luis Miguel** para incentivar que sus workers (usuarios finales B2C) migren a tiers superiores de engagement con la plataforma Ontop, generando más MRR B2C por uso de productos financieros y reforzando la retención del contrato B2B.

**Meta numérica concreta:** generar **+$500/mes de MRR B2C nuevo** cada mes, equivalente a **+0.029 puntos de PES mensuales** (ver sección 6 para el detalle).

---

## 2. El contexto del modelo de comisiones (por qué importa esta campaña)

El modelo de comisión de Luis Miguel está siendo recalibrado. La nueva estructura premia explícitamente el movimiento de workers entre tiers:

- **50% de la comisión** se paga sobre el **NRR** del contrato B2B (retención del cliente).
- **50% de la comisión** se paga sobre el **PES** (Portfolio Engagement Score) — un indicador ponderado de cómo se distribuyen los workers entre los 5 tiers.

El PES tiene dos sub-tranches:
- **Sostenimiento (50%):** premia mantener el PES mes a mes.
- **Crecimiento (50%):** premia subir el PES vs mes anterior (target: +0.029/mes).

**Implicación para la campaña:** cualquier acción que mueva workers a tiers superiores impacta directamente el PES, el MRR B2C, la comisión del CSM, y la probabilidad de renovación B2B. Es una campaña con beneficio multidimensional.

---

## 3. Los 5 segmentos de workers — definición de producto

Los segmentos NO se definen por gasto, sino por **comportamiento de adopción de productos financieros** dentro de Ontop. Esta es la definición canónica del producto:

### 3.1 Starter — "Ontop = payout rail"
- **Mentalidad:** "Ontop es solo un canal de pago para recibir mi sueldo."
- **Comportamiento:** OA (Own Account / transferencia a cuenta propia), transferencia a terceros, o deja los fondos en el wallet.
- **No usa** ningún producto financiero (ni tarjeta, ni future fund, ni Reserve).
- **% del producto global:** 48.03%
- **MRR/user (briefing):** $15.87/mes
- **MRR/user (producto global):** $10.20/mes

### 3.2 Explorer — "Una herramienta financiera útil"
- **Mentalidad:** "Empiezo a usar Ontop para algo más que solo cobrar."
- **Comportamiento:** Hace transferencias **+ activa UN producto financiero** (tarjeta emitida, future fund, **o Quick** — cualquiera de los tres califica).
- **Paso de mentalidad clave:** de "pasivo" a "activo financieramente".
- **% del producto global:** 27.57%
- **MRR/user (briefing):** $18.93/mes
- **MRR/user (producto global):** $12.31/mes

### 3.3 Builder — "Mi plataforma financiera"
- **Mentalidad:** "Ontop es donde manejo varios aspectos de mi vida financiera."
- **Comportamiento:** Transferencias + tarjeta + (future fund **o Quick**) — al menos **dos productos financieros activos**, donde la tarjeta es uno y el otro puede ser future fund o Quick (indistinto).
- **Paso de mentalidad clave:** adopción de múltiples productos.
- **% del producto global:** 12.75%
- **MRR/user (briefing):** $25.48/mes
- **MRR/user (producto global):** $14.73/mes

### 3.4 Power User — "Mi hub financiero"
- **Mentalidad:** "Ontop es mi centro de operaciones financieras."
- **Comportamiento:** Compras con tarjeta + transferencias + (future fund **o Quick**) — todos activos con **uso profundo y recurrente** (no solo "activado", sino verdaderamente usado).
- **Paso de mentalidad clave:** de adopción → frecuencia de uso (hábito).
- **% del producto global:** 5.13%
- **MRR/user (briefing):** $36.74/mes
- **MRR/user (producto global):** $20.50/mes

### 3.5 All-In — "Mi lifestyle financiero"
- **Mentalidad:** "Ontop es mi proveedor financiero principal, todo en uno."
- **Comportamiento:** Todo lo anterior **+ suscripción activa a Reserve**.
- **Paso de mentalidad clave:** compromiso premium / pago de suscripción.
- **% del producto global:** 6.52%
- **MRR/user (briefing):** $56.05/mes
- **MRR/user (producto global):** $22.11/mes

> ⚠️ **Nota importante:** existen dos sets de MRR/user reportados en la documentación interna. El briefing del modelo de comisiones usa los valores más altos; la imagen del producto muestra valores menores. Hay que confirmar cuál es el canónico con producto/finanzas antes de hacer cálculos definitivos. Esta campaña asume los valores del briefing porque son los que ancla el modelo de comisión.

---

## 4. Distribución actual del portafolio de Luis Miguel

Datos de Redshift (última actualización: hace 3 días al momento de esta nota):

### 4.1 Por cliente (clientes B2B)

| Cliente | Total workers | Starter | Explorer | Builder | Power User | All-In |
|---|---|---|---|---|---|---|
| EDTECH PLUS B V | 907 | 462 (51%) | 285 (31%) | 106 (12%) | 22 (2%) | 32 (4%) |
| TOLOKA AI BV | 104 | 58 (56%) | 32 (31%) | 8 (8%) | 0 | 6 (6%) |
| RIDETECHNOLOGY GLOBAL FZ-LLC | 60 | 56 (93%) | 3 (5%) | 1 (2%) | 0 | 0 |
| NEBIUS B.V. | 17 | 8 (47%) | 8 (47%) | 1 (6%) | 0 | 0 |
| JOOM GROUP LIMITED | 1 | 1 (100%) | 0 | 0 | 0 | 0 |
| **TOTAL** | **1,089** | **585 (54%)** | **328 (30%)** | **116 (11%)** | **22 (2%)** | **38 (3%)** |

### 4.2 Métricas agregadas

| Métrica | Valor |
|---|---|
| Workers totales elegibles (con wallet activa) | 1,089 |
| MRR B2C total (workers via productos financieros) | $21,387/mes |
| MRR B2B total (contratos clientes) | $100,353/mes |
| PES baseline (con pesos viejos 1-2-3-4-5) | 1.71 |
| PES baseline (con pesos nuevos anclados al MRR) | 1.24 |

### 4.3 Observaciones críticas sobre el portafolio

- **Concentración brutal en Edtech Plus:** 83% del portafolio (907 de 1,089 workers). Cualquier movimiento de campaña en este cliente domina todos los resultados.
- **Rideтechnology está casi 100% en Starter** (93% de sus workers). Es el cliente con mayor potencial de upgrade Starter→Explorer pero también el más resistente — la propuesta de Ontop probablemente no calzó con sus workers.
- **Toloka y Edtech tienen All-Ins:** señal positiva, hay workers que ya completaron el journey. Se puede estudiar qué hicieron diferente.

### 4.4 Tipos de contrato por cliente — elegibilidad de productos (CRÍTICO)

Esto es un constraint operativo fundamental que determina qué productos se pueden ofrecer a qué workers. **Quick (Paycheck Advance) no está habilitado para contratos PPT.**

| Cliente | Tipo de contrato dominante | Quick disponible | Implicación para la campaña |
|---|---|---|---|
| EDTECH PLUS B V | PPT (prácticamente todos) | ❌ No | No se puede usar Quick como palanca aquí. Limitar a Tarjeta + Future Fund. |
| TOLOKA AI BV | PPT (prácticamente todos) | ❌ No | Mismo caso que Edtech. |
| RIDETECHNOLOGY GLOBAL FZ-LLC (Yango) | Tradicional | ✅ Sí | Único cliente donde Quick es 100% accionable. |
| NEBIUS B.V. | Mixto (tradicional + PPT) | ⚠️ Parcial | Validar caso por caso qué workers son elegibles. |
| JOOM GROUP LIMITED | Por confirmar | — | 1 worker, baja prioridad. |

> ⚠️ **Confirmación pendiente:** "Yango" se refiere a Rideтechnology Global FZ-LLC (operadora de la app Yango). Si el cliente fuera otro, esta tabla debe revisarse.

**Implicación estratégica:** 

- **El 93% del portafolio (Edtech + Toloka, ~1,011 workers) NO puede usar Quick** como palanca de upgrade. Para estos clientes, el único camino al Explorer es vía Tarjeta o Future Fund.
- **Rideтechnology es el único cliente con Quick 100% disponible**, lo cual es relevante porque es el cliente con peor PES (93% Starter). Quick podría ser exactamente la palanca que necesita — atiende una necesidad de liquidez inmediata que tiene mucha resonancia con perfiles de gig economy.
- **Nebius requiere segmentación interna** antes de la campaña: necesitamos saber qué workers están bajo qué tipo de contrato para decidir el mensaje.
- **Joom Group es un cliente nuevo o muy chico:** 1 worker, no es estadísticamente relevante para la campaña.

---

## 5. Las 4 rutas de upgrade — economics por movimiento

### 5.1 Δ MRR por tipo de upgrade

| Ruta | Δ MRR/worker/mes | Δ MRR/worker/año | Notas |
|---|---|---|---|
| Starter → Explorer | +$3.06 | +$36.72 | El menor ROI por worker, pero la ruta con más volumen disponible |
| Explorer → Builder | +$6.55 | +$78.60 | Buen balance volumen/valor |
| Builder → Power User | +$11.26 | +$135.12 | Menos workers disponibles, mayor valor |
| Power User → All-In | +$19.31 | +$231.72 | El mayor ROI/worker pero muy poco volumen |

### 5.2 Cuántos workers se necesita mover para hit target ($500/mes nuevo)

| Ruta | Workers necesarios | Workers disponibles en portafolio |
|---|---|---|
| Starter → Explorer | 163 | 585 (28% del bucket) |
| Explorer → Builder | 76 | 328 (23% del bucket) |
| Builder → Power User | 44 | 116 (38% del bucket) |
| Power User → All-In | 26 | 22 (118% del bucket — ¡no hay suficientes!) |

**Conclusión estratégica:** la única ruta que sola **no puede cumplir el target** es Power User → All-In (faltan workers). El resto son alcanzables pero cada una tiene su propia fricción operativa (ver sección 7).

### 5.3 Pesos PES por tier (modelo recalibrado)

Para tracking del PES con la nueva fórmula:

```
PES = (S×1.00 + E×1.19 + B×1.61 + P×2.32 + A×3.53) / Total Workers
```

| Tier | Peso PES |
|---|---|
| Starter | 1.00 |
| Explorer | 1.19 |
| Builder | 1.61 |
| Power User | 2.32 |
| All-In | 3.53 |

Cada **punto de PES = $15.87 de MRR B2C/mes** (constante, independiente de la ruta).

---

## 6. Target operativo de la campaña

### 6.1 Meta mensual

| Indicador | Valor |
|---|---|
| MRR B2C nuevo a generar | $500/mes |
| Δ PES requerido | +0.029/mes |
| Puntos PES a sumar | 31.5 puntos/mes |
| ARR B2C nuevo (anualizado) | $6,000/año por mes en target |

### 6.2 Comisión de Luis Miguel al lograr el target PES

- Tranche PES total: **$501.77/mes** ($250.88 sostenimiento + $250.88 crecimiento)
- Con acelerador (Δ PES ≥ +0.035): **$627.21/mes**

### 6.3 ROI esperado de la campaña (visto desde Ontop)

- Cada mes en target genera $6,000 ARR nuevo recurrente.
- Costo de comisión asociado: $501.77 (one-time mensual).
- **ROI por mes en target: 12×.**

---

## 7. Las palancas operativas por ruta — qué accionar en cada upgrade

Cada salto entre tiers requiere acciones de marketing distintas porque la fricción no es la misma. Esto es lo que la campaña tiene que **diseñar específicamente por ruta**:

### 7.1 Starter → Explorer (activación del primer producto)
- **Fricción principal:** el worker ve a Ontop solo como rail de pago, no sabe que existen productos financieros.
- **Palanca:** **educación + onboarding del primer producto.**
- **Tácticas posibles:**
  - Email/push de bienvenida explicando la tarjeta, Future Fund o Quick.
  - Incentivo de activación (ej. cashback en primera compra con tarjeta).
  - Webinar/contenido educativo para HR del cliente B2B sobre los beneficios.
  - Materiales de comunicación que el cliente B2B distribuya internamente a sus workers.
- **Quién debe involucrarse:** Marketing (contenido), Producto (flow de activación), CSM (alineamiento con HR del cliente).
- **Cliente prioritario:** Rideтechnology / Yango (93% Starters, contratos tradicionales). Es el único cliente donde **las 3 palancas (Tarjeta, Future Fund, Quick) están todas disponibles**. Quick puede ser especialmente potente aquí por el perfil del cliente (gig economy, necesidad recurrente de liquidez).
- **Restricción PPT:** para Edtech Plus y Toloka (contratos PPT), Quick no aplica. El mensaje se limita a Tarjeta + Future Fund. Adaptar la comunicación según el cliente — no enviar mensajes de Quick a workers de Edtech/Toloka.

### 7.2 Explorer → Builder (adopción del segundo producto)
- **Fricción principal:** ya activó UNO, pero no le ve valor a un SEGUNDO.
- **Palanca:** **cross-sell del producto complementario** (Future Fund o Quick, según el caso y el tipo de contrato).
- **Tácticas posibles:**
  - Campañas in-app personalizadas según lo que el worker ya tiene activado **y su tipo de contrato**:
    - **Contratos tradicionales (Yango / Nebius parcial):** las 3 opciones disponibles.
      - Si tiene tarjeta: pushear Future Fund o Quick.
      - Si tiene Future Fund: pushear tarjeta o Quick.
      - Si tiene Quick: pushear tarjeta o Future Fund.
    - **Contratos PPT (Edtech / Toloka):** solo Tarjeta ↔ Future Fund. Quick no aplica.
  - Bundle promocional (ej. tasa preferente en Future Fund por 3 meses si lo activan, o fee reducido en Quick por X usos en clientes elegibles).
- **Cliente prioritario:** Edtech Plus (mayor volumen absoluto, 285 Explorers). Ojo: como es PPT, el cross-sell se limita a Tarjeta ↔ Future Fund.

### 7.3 Builder → Power User (frecuencia de uso, hábito)
- **Fricción principal:** activó los productos pero los usa esporádicamente.
- **Palanca:** **gamificación, hábito, profundidad de uso de los productos ya activados** (tarjeta + Future Fund o tarjeta + Quick, según lo que el worker tenga).
- **Tácticas posibles:**
  - Programa de cashback escalonado por nivel de uso mensual de la tarjeta.
  - Tiers o badges visibles dentro de la app (status driven).
  - Recordatorios contextuales / nudges de uso.
  - Beneficios por uso recurrente (ej. comisiones reducidas tras X compras al mes, bonus por mantener saldo en Future Fund).
- **Cliente prioritario:** Edtech Plus (106 Builders, mayor base potencial).

### 7.4 Power User → All-In (venta de suscripción Reserve)
- **Fricción principal:** Reserve es un producto pago y requiere "vender el upgrade".
- **Palanca:** **venta directa, demostración de valor premium.**
- **Tácticas posibles:**
  - Free trial de Reserve para Power Users.
  - Comunicación directa de beneficios exclusivos.
  - Posiblemente intervención 1-1 del CSM dado el bajo número.
- **Limitación:** solo hay 22 Power Users en todo el portafolio — el upside total por esta ruta es limitado.

---

## 8. Indicadores de salud B2B que la campaña también impacta

Más allá del MRR directo, la campaña impacta la retención del contrato B2B:

> **Hallazgo interno citado en el briefing:** los clientes B2B donde >20% de los workers están en Builder+ tienen **3× menos probabilidad de churn**.

Estado actual de los clientes del portafolio en esta métrica:

| Cliente | % Builder+ (B + P + A) | ¿Supera el 20%? |
|---|---|---|
| EDTECH PLUS B V | 17.6% | Casi (le falta poco) |
| TOLOKA AI BV | 13.5% | No |
| RIDETECHNOLOGY | 1.7% | Muy lejos |
| NEBIUS B.V. | 5.9% | No |
| JOOM GROUP | 0% | No |

**Implicación:** la campaña debería tener como objetivo secundario llevar a cada cliente al ≥20% Builder+. Edtech está a punto, sería un win rápido. Toloka necesita mover ~8 workers más a Builder+. Los otros tres requieren rediseño profundo.

---

## 9. Restricciones y supuestos importantes para la planificación

### 9.1 Sobre la elegibilidad
- Solo se cuentan workers con **wallet activa**. Los workers excluidos de la wallet no son elegibles para usar productos financieros y no afectan el PES.
- Esto significa que workers nuevos pueden no contar inmediatamente — hay que verificar el flujo de elegibilidad con producto.

### 9.2 Sobre el control del CSM
- El CSM (Luis Miguel) no controla directamente al worker B2C — controla la relación con el HR/admin del cliente B2B.
- La campaña debe estar diseñada para **operarse a través del cliente B2B**, no directamente al worker (excepto comunicaciones in-app/email de Ontop a su base).

### 9.3 Sobre el horizonte temporal
- El target es mensual y acumulativo. Una campaña de 1 mes con buenos resultados pero sin sostenimiento no sirve — el modelo penaliza retrocesos.
- Diseño recomendado: campaña con horizonte mínimo de 3-6 meses, no one-shot.

### 9.4 Sobre los datos
- Los dashboards de PES y migraciones se actualizan vía Redshift. Validar con DataOps la frecuencia de actualización antes de cerrar SLAs operativos.
- Pendiente confirmar la tabla canónica de MRR/user (briefing vs producto global).

---

## 10. Próximos pasos sugeridos para arrancar el proyecto

1. **Validar la fuente canónica de MRR/user** (briefing $15.87 vs producto global $10.20). Definir cuál se usa para tracking de la campaña.
2. **Hacer deep-dive por cliente B2B**, especialmente Rideтechnology (entender por qué no salen del Starter) y Edtech Plus (mayor volumen, palanca principal).
3. **Mapear las acciones de Marketing/Producto disponibles** que ya existen para cada ruta, antes de diseñar nuevas tácticas.
4. **Definir métricas de éxito de la campaña** por ruta (no solo el PES total — también: workers movidos por ruta, % conversion por bucket, time-to-upgrade).
5. **Establecer cadencia de revisión:** mensual con CS, semanal interna entre Luis Miguel y los stakeholders de marketing/producto.
6. **Construir un brief de campaña por cada ruta** (Starter→Explorer, Explorer→Builder, etc.) con audiencia, mensaje, canal, KPI, presupuesto, owner.
7. **Definir cláusulas de la campaña sobre workers nuevos y churn B2B** (cómo se manejan en el cálculo del PES — pendiente del modelo de comisión también).

---

## 11. Documentos relacionados y referencias internas

- Briefing del modelo de comisión: `Luis_Miguel_Commission_Briefing.md` (Daniel Ortiz, mayo 2026)
- Deck del modelo de comisión: `Luis_Miguel_Commission_Deck.pptx`
- Spreadsheet con datos crudos del portafolio: Google Sheets (sheet "Workers buckets", Redshift Import)
- Documento de recalibración PES (sub-tranches y baseline móvil): `Propuesta_PES_Recalibrado.docx`

---

*Documento de contexto para inicio de campaña · Customer Success · Ontop · Q2 2026*

---

## 12. Catálogo de productos financieros — propuestas de valor para los mensajes

Esta es la materia prima narrativa que el equipo de marketing puede usar para construir los mensajes de la campaña. Cada producto está mapeado al tier que ayuda a desbloquear.

### 12.1 Ontop Global Account / Wallet (producto base — todos los tiers)

- **Qué es:** la cuenta global para recibir pagos, mover dinero y gastar sin fronteras.
- **Para quién:** todo worker que entra a Ontop (es el "rail" que define a un Starter).
- **Mensaje base:** "Recibe tu pago global, sin intermediarios bancarios."
- **Rol en la campaña:** este es el punto de partida — el Starter ya lo usa. La pregunta es qué lo motiva a dar el siguiente paso.

### 12.2 Future Fund (palanca multi-tier: Starter→Explorer, Explorer→Builder, Builder→Power User)

- **URL:** https://www.getontop.com/fund
- **Qué es:** programa de rendimiento sobre el saldo en el wallet. Hasta **3% de retorno anual** sobre fondos elegibles, calculado sobre saldo diario y acreditado mensualmente.
- **Cómo se activa:** un solo tap desde el dashboard ("opt-in"). El worker mantiene un saldo elegible y empieza a generar rendimientos.
- **Acceso a los fondos:** hasta 1 día para mover de vuelta al wallet principal (esto importa para comunicar: no es liquidez inmediata).
- **Lo que NO es:** no es una cuenta bancaria, no está cubierto por FDIC, los retornos no están garantizados. Hay que ser claro en la comunicación.
- **Tarifas:** sin fees de membresía ni mantenimiento.
- **Mensajes posibles para la campaña:**
  - *"Tu dinero debería trabajar tan duro como tú. Hasta 3% anual sobre tu saldo ocioso."*
  - *"Deja de dejar dinero sobre la mesa."*
  - *"3 pasos: opt-in, mantén el saldo, crece."*
- **Audiencia ideal:** workers Starter que mantienen saldos significativos en el wallet sin moverlos (data del wallet puede identificarlos). También Explorers que solo tienen tarjeta (cross-sell del segundo producto).
- **Fricciones a anticipar:**
  - "No es cuenta de banco" puede generar dudas → enfatizar transparencia y opt-out en cualquier momento.
  - La elegibilidad depende de región y tipo de contrato → el equipo de Producto debe darnos lista de elegibles antes de la campaña.

### 12.3 Ontop Card (palanca Starter→Explorer y Builder→Power User)

- **Contexto:** parte del Global Account. Tarjeta para compras en 150+ países, sin foreign transaction fees.
- **Rol dual en la campaña:**
  - **Para Starter→Explorer:** activar la tarjeta es uno de los dos caminos posibles para entrar al Explorer (el otro es Future Fund).
  - **Para Builder→Power User:** la diferencia está en uso profundo y frecuente de la tarjeta (no solo tenerla activada). Aquí entra el cashback como driver de comportamiento.
- **Cashback rates (descritos en el contexto de Reserve, pero base disponible para todos):**
  - **Premium categories (10%):** vuelos, lodging corto plazo, rideshare, comidas, suscripciones digitales.
  - **Everyday purchases (5%).**
- **Mensajes posibles para la campaña:**
  - *"Tu tarjeta global, sin fees por usarla afuera."*
  - *"Cashback en tu próximo vuelo, comida o suscripción — directo al wallet en segundos."*

### 12.4 Paycheck Advance / Ontop Quick (palanca multi-tier: Starter→Explorer, Explorer→Builder, Builder→Power User)

- **URL:** https://www.getontop.com/paycheck-advance
- **Qué es:** adelanto del próximo pago según días trabajados desde el último ciclo. Acceso instantáneo, depósito directo en el Global Account.
- **Cómo funciona (ejemplo del sitio):** Laura cobra $900 el día 30. El día 15 (15 días trabajados) tiene disponibles $450 (900 ÷ 30 × 15). Pide $300, los recibe al instante. En el siguiente payday, Ontop deduce $300 + service fee y le acredita el resto.
- **Fees:** una "small service fee" que se muestra antes de confirmar.
- **Repago:** automático, en el siguiente payday.
- **Rollout y elegibilidad:**
  - Está rolando en fases — no todos los workers lo ven aún en su app.
  - **Restricción crítica de tipo de contrato:** Quick NO está habilitado para contratos PPT. Esto excluye prácticamente todo el portafolio de Edtech Plus y Toloka. Solo Rideтechnology (Yango, contratos tradicionales) y la porción tradicional de Nebius son elegibles.
  - **Verificar con Producto** la lista exacta de workers elegibles antes de incluirlos en la campaña — no se debe enviar comunicación de Quick a workers que no lo verán activable en su app.
- **Rol multi-tier:**
  - **Para Starter→Explorer:** activar Quick cuenta como adoptar el primer producto financiero.
  - **Para Explorer→Builder:** si el worker ya tiene tarjeta, activar Quick lo lleva a Builder (Quick puede ser el segundo producto, intercambiable con Future Fund).
  - **Para Builder→Power User:** uso recurrente y profundo de Quick contribuye al "hub financiero" característico del Power User.
- **Por qué es palanca clave:** atiende una necesidad real e inmediata (liquidez antes de payday). Un worker que vivió la experiencia de pedir un adelanto cambia su percepción de Ontop de "rail de pago" a "herramienta financiera útil" — exactamente el salto mental que define al Explorer y refuerza tiers superiores.
- **Mensajes posibles:**
  - *"Tu pago, cuando lo necesitas. No esperes al payday."*
  - *"Accede a parte de lo que ya ganaste — instantáneo, transparente, automático."*
- **Advertencia regulatoria:** este producto es sensible (puede leerse como préstamo). Cualquier comunicación debe pasar por Legal/Compliance.

### 12.5 Ontop Reserve (palanca exclusiva Power User→All-In)

- **URL:** https://www.getontop.com/ontop-reserve
- **Qué es:** membresía financiera premium que desbloquea $4,150/año en beneficios.
- **Precio:** $14.9/mes o **$145/año** (ahorro de ~20% si paga anual).
- **ROI para el worker:** "más de 25× el valor de la membresía" según el sitio.
- **Beneficios desglosados:**

| Beneficio | Valor anual |
|---|---|
| Cashback rewards (hasta 10% en categorías premium, 5% everyday) | Hasta $2,400 |
| Global transfer savings | Hasta $600 |
| Travel perks | $300 |
| Productivity tools | $200 |
| Wellness benefits | $200 |
| Pet care benefits | $200 |
| Travel protection | $250 |
| **TOTAL** | **$4,150** |

- **Audiencia target del sitio:** "Creators, Freelancers, Builders, Founders" — gente con vida internacional, ingresos globales, alto gasto en categorías premium (viaje, suscripciones, rideshare).
- **Mensajes posibles para la campaña:**
  - *"Tu lifestyle, recompensado. Gasta, sube tu recibo, recupera."*
  - *"$4,000+ en beneficios anuales por $145/año."*
  - *"Una membresía financiera diseñada para quienes construyen carreras sin fronteras."*
- **Por qué cuesta vender:** es el único producto con cobro mensual recurrente. Requiere convencer al worker de que sus gastos justifican la membresía.
- **Estrategia recomendada para Power User→All-In:** ofrecer **free trial** (por ejemplo, 1 o 2 meses) a los 22 Power Users del portafolio. Validar primero con Producto/Pricing si esto es viable. Si en el trial el worker recibe cashback suficiente para "ver" el valor, la conversión a pagado es mucho más fácil.

### 12.6 Mapeo producto → ruta de upgrade

Este es el cuadro síntesis que el equipo de marketing necesita para diseñar las acciones:

| Ruta de upgrade | Producto(s) clave a impulsar | Tipo de acción |
|---|---|---|
| Starter → Explorer | Tarjeta **O** Future Fund **O** Quick (cualquiera de los tres) | Activación del primer producto financiero |
| Explorer → Builder | El producto complementario al que ya tiene (Future Fund o Quick son intercambiables como segundo producto) | Cross-sell del segundo producto |
| Builder → Power User | Profundidad de uso de los productos ya activos (tarjeta + Future Fund/Quick) | Gamificación / hábito / cashback escalonado |
| Power User → All-In | Reserve (suscripción) | Venta directa / free trial / case studies de ROI |

### 12.7 Implicación táctica clave: tres productos = tres palancas paralelas

A diferencia de un modelo de upsell tradicional donde hay una sola vía de upgrade, aquí **el worker tiene tres caminos paralelos** para subir de tier: tarjeta, Future Fund y Quick. Cada producto resuelve una necesidad distinta:

| Producto | Necesidad que resuelve | Worker target ideal |
|---|---|---|
| **Tarjeta** | Quiero gastar lo que gano sin fricción internacional | Workers con alto consumo, viajeros, vida digital |
| **Future Fund** | Quiero hacer crecer lo que no estoy usando | Workers con saldos acumulados, mentalidad de ahorro |
| **Quick** | Necesito acceso a mi pago antes del payday | Workers con flujo de caja apretado, gastos urgentes |

Esto tiene cuatro implicaciones estratégicas para la campaña:

1. **Segmentación del Starter por necesidad latente:** en vez de pushear un producto único a todos los Starters, vale la pena segmentarlos por patrón de comportamiento del wallet (¿acumulan saldo? → Future Fund. ¿hacen muchas transferencias? → tarjeta. ¿retiran todo apenas les pagan? → posible candidato a Quick, si el contrato lo permite).
2. **El cross-sell del Explorer al Builder es flexible PERO depende del tipo de contrato:**
   - **Contratos tradicionales (Yango / Nebius parcial):** un Explorer con tarjeta tiene **dos opciones** para llegar a Builder (FF o Quick) — la campaña debe testear cuál convierte mejor.
   - **Contratos PPT (Edtech / Toloka):** solo hay UNA opción de cross-sell: el producto que falta entre Tarjeta y Future Fund. Esto simplifica el mensaje pero limita las palancas.
3. **Rideтechnology / Yango es el "laboratorio" ideal para probar Quick:**
   - 100% contratos tradicionales (todos elegibles para Quick).
   - 93% del cliente está en Starter → enorme potencial de upgrade Starter→Explorer.
   - Perfil de gig economy (rideshare) encaja perfecto con la propuesta de Quick (liquidez antes de payday).
   - Sugerencia: usar Yango como caso piloto para Quick antes de escalar a otros clientes elegibles.
4. **El segmento dominante del portafolio (Edtech + Toloka, ~1,011 workers PPT) no tiene Quick disponible**, por lo que las campañas para estos clientes deben enfocar en Tarjeta + Future Fund. Esto reduce el menú táctico para el 93% del portafolio, lo que hace que el incentivo de activación y el cashback sean palancas aún más importantes para mover el PES en estos clientes.
