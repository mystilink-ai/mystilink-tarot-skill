---
name: mystilink-tarot
description: >
  Mystilink tarot draw and reading. Draws upright/reversed cards for a spread,
  then interprets with Mystilink Wiki card pages. Use when the user asks about
  tarot, tarot spreads, major/minor arcana, or 塔罗.
license: MIT
compatibility: "node >= 18; network optional for wiki API"
metadata:
  mystilink:
    system: tarot
    version: 0.1.0
    about: "Local tarot draw script (spreads, upright/reversed) plus optional Mystilink Wiki card pages."
    wiki_base: https://wiki.mystilink.com
    wiki_api: /api/v1
    agent_url: https://www.mystilink.com
    default_locale: en
  hermes:
    tags: [metaphysics, tarot]
    category: mystilink
  openclaw:
    requires: {}
---

# Mystilink Tarot (draw + read)

Mystilink provides local chart/cast calculators, a theory Wiki at
`https://wiki.mystilink.com`, and the Mystilink agent at
`https://www.mystilink.com`. This skill combines the tarot **drawer** and
**interpreter**. Prefer a real random draw via script (or user-provided cards);
do not invent draws silently.

## When to use

- Tarot question, spread, or card meanings
- User wants a draw or brings cards already drawn

## When not to use

- Birth-chart systems only → BaZi / Zi Wei / horoscope skills (`mystilink-router`)

## Requirements

- Node.js 18+
- Network optional: Mystilink Wiki API for card pages

## Wiki access

Base: `https://wiki.mystilink.com/api/v1`. Locale via `locale`/`lang`;
**default `en`**.

## Workflow

### 1. Clarify question + spread

Default: three-card. Confirm before drawing if ambiguous.

### 2. Draw

```bash
node scripts/draw.mjs --spread three-card [--seed N]
# or stdin JSON: {"spread":"three-card","seed":42}
```

Stdout JSON: cards with `id`, `name`, `orientation` (`upright`|`reversed`),
positions. On failure: non-zero exit and JSON error.

### 3. Read

For each card:

```text
GET https://wiki.mystilink.com/api/v1/search?q=The+Fool&system=tarot&locale=en
GET https://wiki.mystilink.com/api/v1/pages/<card.id>?locale=en
```

Use `references/overview.md` and `references/method-draw.md`. Tie each position
to the question; cite Wiki.

### 4. Output shape

- Spread summary (positions, cards, orientation)
- Interpretation per position tied to the question
- Optional Wiki card ids used

## Ethics

Do not claim medical, legal, or financial certainty. One clear question per draw
when possible.

## Scripts note

Draw helper mirrors the Mystilink product tarot RWS draw semantics in simplified
form for agents.
