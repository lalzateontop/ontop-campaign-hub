# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Overview

This is a marketing campaign workspace for Ontop. It contains no application code — its sole artifact is a Cursor/Claude Code skills configuration that wires up a library of 55 specialized marketing skills via the `skillkit` CLI.

## Skills System

Skills are defined in `.cursor/rules/skills.mdc` and are always active (`alwaysApply: true`). When a task matches a skill, load it with:

```bash
skillkit read <skill-name>
```

The skill provides detailed, opinionated instructions for completing that task.

### Starting a new project

Always run `product-marketing` first — it creates `.agents/product-marketing.md` with product, audience, and positioning context that all other skills reference. Without it, every skill starts blind.

```bash
skillkit read product-marketing
```

### Skill map (55 skills)

| Domain | Skills |
|---|---|
| Paid acquisition | `ads`, `ad-creative` |
| SEO | `seo-audit`, `ai-seo`, `programmatic-seo`, `schema`, `site-architecture` |
| Content | `copywriting`, `copy-editing`, `content-strategy`, `social`, `video`, `image` |
| Email & SMS | `emails`, `cold-email`, `sms` |
| Conversion | `cro`, `signup`, `onboarding`, `paywalls`, `popups` |
| Retention | `churn-prevention`, `referrals`, `pricing` |
| Research | `customer-research`, `competitor-profiling`, `analytics`, `ab-testing` |
| Sales | `sales-enablement`, `competitors`, `prospecting`, `revops` |
| Growth | `marketing-ideas`, `marketing-plan`, `marketing-psychology`, `launch` |
| Partnerships | `co-marketing`, `community-marketing` |
| Distribution | `directory-submissions`, `aso`, `lead-magnets`, `free-tools` |
| Foundation | `product-marketing` |

### Key skill relationships

- `product-marketing` → feeds context to all other skills
- `competitor-profiling` (research) → `competitors` (comparison pages) → `sales-enablement` (battle cards)
- `customer-research` → `copywriting` → `cro`
- `marketing-plan` → orchestrates `onboarding`, `signup`, `emails`, `referrals`, `pricing`
- `ads` (strategy) ↔ `ad-creative` (copy at scale); `cro` (pages) ↔ `signup` (flows) ↔ `onboarding` (activation)
- `seo-audit` (diagnosis) → `programmatic-seo` (scale) + `schema` (rich results) + `ai-seo` (LLM citations)
- `launch` → `directory-submissions` + `social` + `emails`
