---
type: meta
tags: [meta, root]
updated: 2026-01-12
---

# agents.md: Operating Manual (example)

**Owner:** Ada Mensah · runs Ada's Oven, a home bakery in Accra (fictional)
**Method:** Karpathy-style LLM knowledge base. The LLM writes the wiki; Ada reads it and asks questions.

Start every task at [[wiki/index]]. Unknowns live in [[wiki/gaps]]. History is in [[wiki/log]].

## Owner's rules

- **Priorities:** [[wiki/00-core/goals|goals]]: steady weekly orders, then a second oven.
- **Needs approval:** any message to a customer, any price not in [[wiki/00-core/offers-pricing|offers-pricing]].
- **Prices you may quote:** only those in [[wiki/00-core/offers-pricing|offers-pricing]].

## Hard rules

Never invent facts (unknown → **[CONFIRM]**), never edit `raw/`, record contradictions under Conflicts, never copy passwords anywhere.
