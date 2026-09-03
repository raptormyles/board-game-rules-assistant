# Rulebook Data Schema

**Current version: `0.2`** — see Version History at the bottom of this document.

This document is the formal definition of the per-game Markdown schema described in `PRD.md` (§7, §8, §12). It's the spec the pipeline (and, for now, manual test runs) writes to. A blank, fillable copy of this structure lives in `docs/game-template.md`.

**Format:** one Markdown file per game, stored in the private `board-game-rules-assistant-data` repo at `games/<game-slug>.md` (slug = lowercase, hyphenated title, e.g. `ticket-to-ride.md`). Each file is YAML frontmatter followed by 12 fixed sections.

**Detail level (applies to every section):** near-verbatim. Keep functional rules content essentially as written in the rulebook — do not summarize, paraphrase away detail, or "clean up" rules language. Flavor text (thematic narration, box copy) and designer strategy-advice asides are KEPT, not condensed away — label each one clearly as flavor or strategy commentary (e.g. a "*Flavor text:*" or "*Strategy tip:*" lead-in) so it's never confused with a binding rule, and place it in whichever section covers the content it's physically located next to in the source (not a separate section, unless it comes from a document covered by §11 Supplementary Material). When in doubt, keep it.

**Traceability (applies to every section):** every fact must be traceable back to a specific source photo. See "12. Source References" below for how this is recorded.

---

## Frontmatter

```yaml
---
title: string              # required — full title as printed on the box/rulebook
designers: [string]        # optional — as credited in the rulebook
publisher: string          # optional — as credited in the rulebook
player_count: string       # required — as printed, e.g. "2-5". If not stated anywhere in the source photos, use the literal string "unknown" rather than guessing or omitting the field.
playtime: string           # required — as printed, e.g. "30-60 minutes". If not stated anywhere in the source photos, use the literal string "unknown" rather than guessing or omitting the field.
min_age: integer           # optional — as printed, e.g. 8
mechanisms: [string]       # required — tags describing the game's mechanisms (e.g. route-building,
                            #   set collection, hand management). This is the main hook Phase 2 will
                            #   use for cross-game comparison, so err toward specific, genre-standard terms.
interaction_model: string  # required — one of: competitive | cooperative | team
source_photos: [string]    # required — every source photo filename used for this game, in reading order
date_processed: date       # required — ISO 8601, e.g. 2026-09-02
schema_version: string     # required — schema version this file conforms to (current: "0.2"). See Version History below.
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

### 11. Supplementary Material
Content from any physically separate supplementary booklet or sheet — a `ReferenceGuide-NN` insert, a `SoloRules-NN` insert, or similar per `docs/naming-convention.md` — that isn't part of the main numbered rulebook pages.

Unlike every other section, this one is NOT reorganized by topic. Preserve each supplementary document's own physical structure and reading order — the way its content actually appears on the page — rather than splitting it across Components/Actions/Special Rules/etc. by subject matter. If a game has more than one such document (e.g. both a Reference Guide and a Solo Rules insert), give each its own `####` subheading (e.g. `#### Reference Guide`, `#### Solo Rules`) and preserve that document's internal order within its own subheading. A game with no supplementary material still keeps this section, stating "None — no supplementary reference material for this game" rather than omitting it (same convention as an empty §8).

The main topical sections (1–10) should NOT duplicate this content — if something here is directly relevant to, say, Actions, a brief cross-reference ("see §11, Reference Guide") is fine, but the actual text lives only here.

### 12. Source References
A table mapping each of sections 1–11 to the source photo(s) it was drawn from, so any claim can be checked against the original page during manual review.

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
| Supplementary Material | ... |
```

---

## Version History

| Version | Date | Changes |
|---|---|---|
| 0.1 | 2026-09-02 | Initial schema: frontmatter spec + 11 fixed sections, formalized from PRD §7/§8/§12 and validated against Ticket to Ride as a first test conversion. |
| 0.2 | 2026-09-02 | Resolved three open questions found converting all 9 photographed games (see `docs/schema-open-questions.md`): (1) `player_count`/`playtime` stay required, using the literal string `"unknown"` when not stated in the source photos, instead of ad hoc placeholder text or omitting the field; (2) added a new §11 "Supplementary Material" section — content from a physically separate Reference Guide or Solo Rules insert is now kept together, preserved in that document's own physical order, instead of being split across the topical sections by subject (Source References renumbered §11 → §12 accordingly); (3) flavor text and designer strategy-advice asides are now kept (clearly labeled as such) instead of being condensed away, placed by physical location in the source rather than omitted. |

Schema versions stay below `1.0` while the section set and frontmatter fields are still being validated against real rulebooks (per PRD §10's open question on generalization). Each time the schema changes, add a new row here — that way every existing `games/<slug>.md` file's `schema_version` field points to a documented revision, and a future schema change doesn't silently invalidate older files without a record of what changed.

## Known gaps (not solved by this schema)

- **Legacy/campaign games** (persistent state and rules that change across sessions, e.g. a Legacy-style game) aren't handled — logged in PRD §14 as a future scenario, not needed for the current pilot.
- **Errata/FAQ documents** beyond the printed rulebook are out of scope for v1 (PRD §7).
