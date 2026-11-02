---
name: Paper deep read
description: >-
  Use when reading, summarizing, critically analyzing, or preparing Notion
  ingest for an academic paper (arXiv/PDF/HTML/project page)—especially robotics
  / embodied / VLA work needing method, data, benchmarks, and subtask-annotation
  notes.
---
# Paper deep read

Adapted from [Calix-L/awesome-latex-skills `paper-read`](https://github.com/Calix-L/awesome-latex-skills/tree/main/paper-read) (MIT; prefer this over low-star one-off skills). Keep answers grounded in the inspected version; never invent numbers or unread citations.

## Choose depth

| Mode | When | Output |
|---|---|---|
| `skim` | Decide if worth time | Problem, approach, headline result, figure story, stated limits |
| `read` (default) | Discuss or apply | Method, setup, results, claim↔evidence with section/table/figure |
| `deep` | Critique / reuse ideas | Assumptions, equations, ablations, supplements, open questions |
| `ingest` | Save to a knowledge base | Full field checklist below + overview figures when available |

Match the user’s language. A focused question need not produce a full report.

## Acquire evidence

1. Prefer user-supplied text/PDF. For links: abs → HTML (`/html/{id}`) → PDF; record title, authors, **exact arXiv version** (`vN`), venue/status, project/code URLs.
2. Do not silently upgrade to a newer version than the user named.
3. Extract with available PDF/HTML tools. If columns, math, tables, or figures are lost, say what is unreadable.
4. Paywalls: seek a legitimate author/repo copy; do not pretend you read the full paper from the abstract alone.

## Analysis framework

### Skim
Title → abstract (problem→approach→result) → main figures/tables → last intro paragraph (contributions). Stop when you can say whether to go deeper.

### Read
- **Intro**: context → gap → approach → listed contributions; flag overclaims.
- **Method**: captions first, then why each design choice; 2–3 key equations in plain words; name the “trick”.
- **Experiments**: headline table first, then datasets/baselines/metrics; note missing baselines and failure analysis.
- **Conclusion**: match results; note missing limitations.

### Deep
Assumption audit (explicit + implicit), consistency of claims vs tables, idea mining (usable / adaptable / open / failed attempts). Distinguish author claim vs your interpretation vs algebraic check. Reading ≠ reproduction.

### Cross-paper compare
Align task, split, metric, protocol, and resources before comparing numbers; label incomparable results.

## Embodied / VLA checklist (always for robotics papers)

Fill what the paper actually states; write “文中未写” when absent—do not invent.

- **Problem & gap** relative to prior VLA / WAM / world-model / imitation work
- **Method core**: observation interface, prediction target (action / latent / Effect / video), training stages
- **Data**: sources, hours/episodes, embodiment, filtering, train/eval separation
- **仿真榜单** and **真机榜单** (protocol: seeds, episodes, randomization)
- **子任务 / 流程标注** (required when relevant):
  1. Source labels (human subtask language, hierarchical captions, skill IDs, none)
  2. Author pipeline (how segments are cut/filtered; evaluation-only vs training labels)
  3. Model use (subtask head/loss, next-step supervision, latent step tokens, none)
- **Limitations** the authors admit + gaps you see in evidence

## Ingest mode field list

When mode is `ingest` (or the user asks to save into Notion/notes), produce:

1. Overview / teaser figures (download when public)
2. Links, authors, source, tags, status
3. Full abstract translation (if user language ≠ paper language)
4. Short intro, contributions, prior problem, data
5. Sim + real benchmarks
6. Subtask-annotation section (three-way split above)
7. One-line summary + why relevant
8. Index-row fields: title `Year · ShortName`, source, tags, status, date

Keep destination page IDs and team routing out of this skill; use the conversation’s standing store preference.

## Output hygiene

- Lead with the answer to the user’s question.
- Cite section / table / figure for non-trivial claims.
- Preserve units, percentage points vs relative %, and uncertainty.
- Attribute comparisons taken only from the paper’s related-work section to the authors.
- Prefer this skill’s recipe over ad-hoc low-star GitHub paper skills unless the user names another source.
