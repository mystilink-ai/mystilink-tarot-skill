# Changelog

Version is tracked in `SKILL.md` under `metadata.mystilink.version` and in this file.

## 0.1.0

- Agent Skill for tarot draw and reading
- `scripts/draw.mjs` draws upright and reversed cards for the requested spread
- `references/overview.md` and `references/method-draw.md` document spreads and map cards to Mystilink Wiki card pages (`wiki.mystilink.com`)
- `examples/draw-request.json` gives a runnable draw request
- Runtime: `node >= 18`; the Wiki lookup is optional
- Install by copying this directory into a host skills path that reads `SKILL.md`
