# Skill

Reusable assistant Skills. Each skill is a folder with one `SKILL.md`.

## Sync

Keep this repository and the local skills folder in sync whenever a skill is added or changed. Paths and machine-specific details belong in a one-off task, not in skill text.

Layout: one directory per skill → `SKILL.md` (YAML frontmatter + steps).

## Skills

| Directory | Name | When to use |
|---|---|---|
| `annotation/` | annotation 静态页发布 | Build/publish static annotation or pipeline-trace pages for **public** links (GitHub Pages first), optional self-hosted or local preview |
| `paper-deep-read/` | Paper deep read | Paper skim / read / deep critique / Notion ingest (esp. embodied / VLA) |

## Usage

Invoke via `/` or `@` in chat, or describe the task; the assistant follows the matching `SKILL.md`.
