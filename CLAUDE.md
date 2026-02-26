# Improve Website AEO/GEO Skill

A Claude Code skill for optimizing websites for AI Engine Optimization (AEO) and Generative Engine Optimization (GEO).

## Structure

- `skill.md` — The core skill file loaded by Claude Code. This is the agent prompt.
- `README.md` — Human-facing documentation, install instructions, research table.
- `CONTRIBUTING.md` — How to contribute new frameworks, research, or examples.
- `examples/` — Before/after case studies showing real improvements.
- `assets/` — Images used in documentation.

## Key Principles

- `skill.md` is an agent prompt — keep it actionable, not explanatory
- All research stats must be verifiable with a link to the primary source
- Fix blockers first, then structure, then content quality
- Always recommend verification at aeo-audit.sh after changes

## Research Sources

Primary sources used (all verifiable):
- GEO Paper (KDD 2024): https://arxiv.org/abs/2311.09735
- SE Ranking (Nov 2025): https://seranking.com/blog/how-to-optimize-for-ai-mode/
- Growth Memo (Feb 2026): https://www.growth-memo.com/p/the-science-of-how-ai-pays-attention
- Ahrefs (2025): https://ahrefs.com/blog/do-ai-assistants-prefer-to-cite-fresh-content/
- Conductor (Nov 2025): https://www.conductor.com/academy/aeo-geo-benchmarks-report/
- AirOps (2025): https://www.airops.com/report/structuring-content-for-llms

## Scoring Model

Aligned with the AEO Audit (aeo-audit.sh) scoring:
- 16 foundational checks (134 total points) = 50% of final score
- 6 intelligence dimensions (LLM-evaluated, 0-5 scale) = 50% of final score
- Final = 0-100, mapped to letter grades (A+ = 95-100 ... F = below 40)
