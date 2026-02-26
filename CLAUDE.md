# Improve Website AEO/GEO Skill

This repo contains a Claude Code skill for optimizing websites for AI Engine Optimization (AEO) and Generative Engine Optimization (GEO).

## Structure

- `skill.md` — The core skill file. This is what gets loaded into Claude Code's context when the skill is invoked.
- `README.md` — Installation and usage instructions.

## Development

The skill's scoring criteria and methodology are derived from the [AEO Check](https://www.aeocheck.com) audit tool. When updating the skill, ensure changes stay aligned with the checker's scoring model:

- 16 foundational checks (134 total points)
- 6 intelligence dimensions (LLM-evaluated, 0-5 scale)
- Final score = 50% foundational + 50% intelligence

## Key Principles

- Always fix blockers first (AI bot access, restrictive meta tags)
- Prioritize high-impact, low-effort changes
- Provide framework-specific code examples
- Recommend verification via aeocheck.com after changes
