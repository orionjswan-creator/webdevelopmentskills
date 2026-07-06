# Claude Code guidance

This repository is a skill library for building award-quality websites. The routing table and
hard rules live in [AGENTS.md](AGENTS.md) — follow them exactly. Summary:

- Building a site → follow `skills/site-builder/SKILL.md`
- Creating/spec'ing assets → follow `skills/asset-creation/SKILL.md`
- Aesthetic + stack decisions → the chosen skill under `skills/styles/`

When editing the skills themselves: keep every SKILL.md self-contained (an agent with no other
context must be able to follow it), keep code recipes copy-paste runnable, and keep the
frontmatter `name`/`description` accurate — the description is what triggers skill selection.
