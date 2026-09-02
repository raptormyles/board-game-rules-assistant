# Rulebook Data Schema (v1)

This document is the formal definition of the per-game Markdown schema described in `PRD.md` (§7, §8, §12). It's the spec the pipeline (and, for now, manual test runs) writes to. A blank, fillable copy of this structure lives in `docs/game-template.md`.

**Format:** one Markdown file per game, stored in the private `board-game-rules-assistant-data` repo at `games/<game-slug>.md` (slug = lowercase, hyphenated title, e.g. `ticket-to-ride.md`). Each file is YAML frontmatter followed by 11 fixed sections.

**Detail level (applies to every section):** near-verbatim. Keep functional rules content essentially as written in the rulebook — do not summarize, paraphrase away detail, or "clean up" rules language. The only thing that may be condensed is pure flavor/marketing text (box copy, thematic narration) that carries no rules content. When in doubt, keep it.

**Traceability (applies to every section):** every fact must be traceable back to a specific source photo. See "11. Source References" below for how this is recorded.

---

## Frontmatter

```yaml
---
title: string              # required — full title as printed on the box/rulebook
designers: [string]        # optional — as credited in the rulebook
publisher: string          # optional — as credited in the rulebook
player_count: string       # required — as printed, e.g. "2-5"
playtime: string           # required — as printed, e.g. "30-60 minutes"
min_age: integer           # optional — as printed, e.g. 8
mechanisms: [string]       # required — tags describing the game's mechanisms (e.g. route-building,
                            #   set collection, hand management). This is the main hook Phase 2 will
                            #   use for cross-game comparison, so err toward specific, genre-standard terms.
interaction_model: string  # required — one of: competitive | cooperative | team
source_photos: [string]    # required — every source photo filename used for this game, in reading order
date_processed: date       # required — ISO 8601, e.g. 2026-09-02
schema_version: string     # required — schema version this file conforms to, e.g. "1.0"
---
```

Notes:
- `designers`, `publisher`, and `schema_version` are additions beyond the exact field list in PRD §12 (which specified `title`, `player_count`, `playtime`, `mechanisms/tags`, `interaction_model`, `source_photos`, `date_processed`). They're included here because they're cheap to capture from the cover/credits and (for `schema_version`) useful if the schema changes later — drop them if you'd rather stick to the PRD list exactly.
- No complexity/weight field — deliberately excluded per PRD §12 (deferred backlog item, §14).
- `mechanisms` and `interaction_model` are the fields Phase 2 is expected to lean on most, per PRD §12 — worth getting right even at pilot scale.

---

## Sections

### 1. Overview
Theme/premise in brief, and the win condition in one or two sentences. This is scene-setting, not the full Scoring section — just enough for someone to know what the game is "about" before reading further.

### 2. Components
The full component list, as printed (board(s), cards, tokens, player pieces, counts). Keep counts and material descriptions exact — this is often used to verify a physical copy is complete.

### 3. Setup
Step-by-step setup instructions, in the order printed. Include table/board setup, starting hands, initial resource distribution, and anything else needed before the first turn.

### 4. Turn Structure / Core Loop
How a turn (or round) is structured, including turn order determination and any automated/system steps that aren't player actions (e.g. a cooperative game's "Infect" or event-deck phase). This section describes the *shape* of a turn; section 5 describes what each action actually does.

### 5. Actions
Every action a player can take on their turn, with full mechanical detail for each — including any named sub-mechanics tied to a specific action (e.g. wild-card rules, special card types, exceptions). If an action has enough internal complexity to warrant its own subheading in the source rulebook, keep that structure here.

### 6. Scoring & Win Conditions
How points are scored (tables, formulas, per-item values) and how the winner is determined, including tie-break rules. Explicitly allows "no numeric score, shared win/loss" as a valid answer for cooperative games — this section is about *how the game is won*, not necessarily about points.

### 7. End-of-Game Trigger
The specific condition that ends the game (a supply running out, a player reaching a threshold, a fixed round count, a shared loss condition, etc.), and what happens between that trigger and the game actually ending (e.g. "each other player gets one final turn").

### 8. Special Rules / Variants
Player-count-specific adjustments, solo-mode rules, and any expansion or variant content called out directly in the base rulebook (not separate expansion products). If the rulebook has nothing here for a given game, say so explicitly rather than omitting the section — an empty section is a fact ("this rulebook has no variants"), not a gap.

### 9. Edge Cases / FAQ / Clarifications
Anything the rulebook flags as an exception, a special case, an "important note," or a clarification of an otherwise-ambiguous interaction. Also covers rulebook-stated behavior for edge conditions (e.g. what happens if a shared deck runs out).

### 10. Glossary
Game-specific terms a new player wouldn't already know, defined briefly. Skip generic board-game vocabulary (e.g. "turn," "player") unless the rulebook gives it a special meaning in this game.

### 11. Source References
A table mapping each of sections 1–10 to the source photo(s) it was drawn from, so any claim can be checked against the original page during manual review.

```markdown
| Section | Source photo(s) |
|---|---|
| Overview | ... |
| Components | ... |
| Setup | ... |
| Turn Structure / Core Loop | ... |
| Actions | ... |
| Scoring & Win Conditions | ... |
| End-of-Game Trigger | ... |
| Special Rules / Variants | ... |
| Edge Cases / FAQ | ... |
| Glossary | ... |
```

---

## Known gaps (not solved by this schema)

- **Legacy/campaign games** (persistent state and rules that change across sessions, e.g. a Legacy-style game) aren't handled — logged in PRD §14 as a future scenario, not needed for the current pilot.
- **Errata/FAQ documents** beyond the printed rulebook are out of scope for v1 (PRD §7).
