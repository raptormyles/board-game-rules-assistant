# Product Requirements Document: Board Game Rules Assistant

**Author:** Myles
**Status:** Draft v4
**Last updated:** 2026-09-01

---

## 1. Overview

An AI-assisted pipeline that converts photos of physical board game rulebooks into (a) a short, orienting **comparison pitch** — "if you know X, this is X but with these differences" — and (b) a clean, structured, easy-to-scan **rules reference** for that game. The comparison pitch is the headline feature: the fastest way to help someone size up a new game using games they already know. The pilot targets two games — Ticket to Ride and Catan — so the comparison logic has real data on both sides.

The project is organized into three major phases (§2). Everything currently scoped as "v1" in this document is entirely inside **Phase 1: Extraction & Storage** — Myles owns roughly 100 games whose rulebooks could eventually feed this pipeline, so Phase 1's design needs to generalize well even though the pilot itself only covers two games.

This project has a dual purpose:
1. **Learning project:** a hands-on way to build practical AI/tooling skills (image-to-text extraction, LLM-based structuring and reasoning, Python) for job search purposes, built by Myles with AI guidance/review rather than handed over as a finished product.
2. **Real utility, with room to grow:** even at v1 scale, it should be something Myles and his regular game group actually use — and it's being designed with an eye toward eventually supporting more games and more users, not just as a disposable demo.

## 2. Project Phases / Milestones

This project breaks into three major phases. Everything else in this PRD (scope, requirements, roadmap) describes **Phase 1** work; Phases 2 and 3 are named here so the overall shape is clear, but are not designed in detail yet.

### Phase 1 — Extraction & Storage (current focus)
Turn photographed rulebook pages into complete, well-organized Markdown files with a consistent structure. Central questions this phase has to answer: what are the common elements present across virtually any rulebook (the shared schema/sections), how much detail gets kept vs. summarized, and how/where the result is stored and accessed. This phase must generalize — Myles owns roughly 100 games whose rulebooks could eventually run through it, even though the pilot itself covers only Ticket to Ride and Catan.

### Phase 2 — Analysis
Once multiple games exist in a consistent structured format, find commonalities and relationships across them — shared mechanisms, structural similarities, what makes two games alike or different — and research effective methods for doing that well. This is where the comparison-pitch capability is ultimately grounded at scale: it depends on Phase 1 producing data structured consistently enough to compare across many games, not just the two pilot games.

### Phase 3 — Presentation / User-Facing Functions
Decide how results (structured references, comparisons, and whatever else Phase 2 surfaces) are actually shown to and used by people — output formats, interfaces, and functionality beyond raw files. Deliberately left open until Phases 1 and 2 prove out; the "files only" output decision in Phase 1 scope (§6) is a placeholder, not a final answer for the project as a whole.

## 3. Problem Statement

Picking up a new board game is daunting. Rulebooks are dense, inconsistently organized, and every publisher writes them differently — different section structures, different terminology, different assumptions about what a reader already knows. Reading one cover-to-cover just to decide "is this easy for me to learn?" is slow, and re-finding a specific rule later is often slower still.

One of the fastest ways an experienced player actually sizes up a new game is by comparison: "oh, this is basically Dominion, but you build a city instead of a deck" tells you more in one sentence than several pages of rules. That shortcut mostly lives in individual players' heads and hobbyist reviews — there's no quick, reliable way to generate it for an arbitrary rulebook you've just picked up.

## 4. Goals

- Generate a short, accurate "if you know X, this is X + these differences" comparison pitch for a game, anchored to well-known reference games — the primary way this project helps someone size up a new game fast.
- Prove that a rulebook's photographed pages can be reliably turned into accurate, well-structured, human-readable rules content using an LLM-based pipeline (secondary, supporting output).
- Produce something Myles and his game group would genuinely reach for.
- Use the build process to develop transferable AI/tooling skills (working with the Claude API, image-based extraction, comparative reasoning over structured data, Python pipeline design) that support Myles's job search.
- Design Phase 1's storage schema to generalize across Myles's much larger collection (~100 games), not just the two pilot games — even though only two games are actually processed in v1.

### Success metrics for v1 (Phase 1 pilot)

- **Comparison quality:** the "it's like X" pitch for Ticket to Ride and Catan is accurate, specific, and actually useful for orienting someone who knows one but not the other (not generic or shallow).
- **Extraction accuracy:** the structured reference output for both games is correct and complete against the real rulebooks (verified manually, section by section — see §8).
- **Usefulness:** Myles or someone in his game group would actually use the output to size up or learn a game.
- **Demo/code quality:** the pipeline and code are clean and explainable enough to walk through in a job interview context.

## 5. Target Users

**v1:** Myles and his regular game group (informal, direct use — not a public release).

**Longer-term (not committed, noted as direction):** general board game hobbyists picking up a new game and wanting a fast way to size it up. v1 decisions should not deliberately foreclose this, but nothing in v1 scope requires building for it yet (see §7, out of scope).

## 6. Use Cases / User Stories

- As someone who's about to learn a new game, I want a one-line comparison to a game I already know, so I can quickly gauge how different (or similar) it really is before committing time to learning it.
- As a player who owns a game but hasn't played in a while, I want a quick, organized reference so I can re-learn the rules faster than re-reading the full rulebook.
- As a player mid-game, I want to quickly check a specific rule (e.g., a scoring detail or an edge case) without flipping through the physical rulebook.
- As someone introducing a game to my group, I want both the comparison pitch (to set expectations fast) and a clean setup/turn-structure summary to reference while teaching it.
- As Myles, I want a working, well-structured example of an AI extraction + comparative-reasoning pipeline I can discuss and show in interviews.

## 7. Scope (Phase 1 / v1)

### In scope for v1
- **Two pilot games**, so comparison logic has real data on both ends:
  - **Ticket to Ride** (3 rulebook photos already collected).
  - **Catan** (photos not yet collected — needs to be added to the source folder before this game can be processed).
- Ingestion of rulebook page photos as input, for each game independently.
- AI-based (Claude API, vision) extraction of rulebook text/content from those photos.
- Structuring the extracted content into a consistent set of sections per game (secondary output), stored **near-verbatim** (condensed only where the source is pure flavor/marketing text — no functional rules content is summarized away):
  - Overview (theme/premise, win condition in brief)
  - Components
  - Setup
  - Turn Structure / Core Loop (includes automated/system steps, e.g. a cooperative game's "Infect"-style phase, not just player actions)
  - Actions
  - Scoring & Win Conditions (explicitly allows "no scoring, shared win/loss" as a valid answer for cooperative games, not just numeric scoring)
  - End-of-Game Trigger
  - Special Rules / Variants (player-count adjustments, solo mode, expansions called out in the base rulebook)
  - Edge Cases / FAQ / Clarifications
  - Glossary of terms
  - Source references (which photo(s) each section was extracted from, for traceability during manual verification)
- **Structured metadata (YAML frontmatter)** at the top of each game's Markdown file: `title`, `player_count`, `playtime`, `mechanisms/tags`, `interaction_model` (competitive / cooperative / team), `source_photos`, `date_processed`. Deliberately excludes a complexity/weight field (that's the deferred difficulty-scoring idea, §14).
- A simple **`games_index.md`** catalog at the top level of the source folder: one row per processed game (title, status, player count, playtime, tags), linking to each game's file — started now rather than deferred to Phase 2.
- **Comparison pitch generation (primary/headline output):** given a processed game's structured rules, generate a short, specific "if you know X, this is X but with these differences" statement.
  - Anchored to **well-known reference games generally** (using the model's own broad knowledge of popular board games), not limited to only games that have been run through this pipeline — the pipeline doesn't need every possible anchor game structured and stored to make a comparison.
  - For the pilot specifically, Ticket to Ride and Catan double as both subject and anchor for each other, so the comparison can be validated against real structured data on both sides.
- Output as **files** (Markdown) — no CLI or web UI required for v1.
- Manual verification pass: Myles reviews both the extracted/structured output and the comparison pitch, section-by-section and statement-by-statement, against the real rulebooks and his own game knowledge.
- Source material limited to what's **printed in the rulebook itself** — no official errata or FAQ documents in v1.
- Storage/schema design that could plausibly extend to the other ~100 games Myles owns, even though only 2 are processed now (this is a Phase 1 design constraint, not a Phase 1 deliverable — see §12 for detail once settled).

### Explicitly out of scope for v1
(See §13 Scenarios/Backlog for future-revisit detail on each of these.)
- Phase 2 (Analysis) and Phase 3 (Presentation) work of any kind — v1 is Phase 1 only.
- Difficulty/complexity scoring ("how hard will this be for me to learn") — lower priority, logged as a future scenario rather than designed now.
- Machi Koro — used only as an illustrative example in discussion; not added to pilot scope (no photos to be taken for it in v1).
- A browsable "list of games I own" / picker UI — deferred; v1 works directly with the two pilot games.
- The other 4 already-photographed games (Tapestry, Trekking the National Parks, Zooloretto, Flamecraft) — deferred until the pilot pipeline and comparison logic are validated.
- Any chatbot / conversational Q&A interface (evaluated and deliberately not chosen).
- A CLI tool or web front-end (deferred; output is just files for now).
- Official errata/FAQ ingestion beyond the printed rulebook.
- Public hosting, multi-user accounts, or any public-facing release.
- Search or querying across more than the two pilot games.

## 8. Functional Requirements

1. **Image ingestion:** the pipeline reads in a set of rulebook page photos for a given game (organized into per-game folders).
2. **Text/content extraction:** each page image is processed via an LLM with vision capability (Claude API) to extract its text/content accurately, including tables and diagrams where feasible to describe.
3. **Structuring:** extracted raw content is organized by an LLM step into the fixed 11-part section set (§7), stored near-verbatim, rather than left as a flat transcript.
4. **Metadata generation:** the pipeline produces YAML frontmatter for each game (title, player count, playtime, mechanisms/tags, interaction model, source photos, date processed).
5. **Index maintenance:** processing a game updates a top-level `games_index.md` catalog row for that game.
6. **Comparison pitch generation:** given a game's structured rules (and, where relevant, another processed game's structured rules), generate a short, specific comparison statement identifying a well-known anchor game and the key differences — not a generic genre label.
7. **Output:** the structured reference (with frontmatter), the comparison pitch, and the index update are saved as readable Markdown files.
8. **Verification support:** the output should make it easy for Myles to check each section, and the comparison pitch's claims, against the source photos and his own game knowledge (e.g., retaining a way to trace a section back to its source page(s)).

## 9. Non-Functional Requirements / Constraints

- **Language/stack:** Python.
- **Involvement model:** Myles writes the implementation code; Claude's role is to guide, explain, and review rather than produce the finished pipeline directly. This is treated as a hard constraint, not a preference — it's the point of the project.
- **Verification rigor:** every extracted section, and every comparison pitch, is manually reviewed by Myles against the source rulebook and his own game knowledge before being considered "done" for a pilot game (learning-focused, not a rubber stamp).
- No committed constraint on API cost tracking or data locality at this stage (considered, not flagged as a hard requirement for v1).

## 10. Risks & Open Questions

- **Copyright/IP (flagged risk):** rulebooks are copyrighted content owned by their publishers. Personal/private use for a small group is low-risk, but if this project ever moves toward "seed of a real product" territory with other users or public distribution, redistributing extracted rulebook content raises IP questions that need to be addressed before any public launch. Not a blocker for v1; explicitly carried forward as an open risk.
- **Comparison quality is subjective and hard to verify automatically.** A weak or generic comparison ("it's a strategy game") defeats the point; validating "good" comparisons for the pilot relies on Myles's own judgment as a player, not an automated metric.
- **Extraction accuracy varies by rulebook.** Ticket to Ride and Catan were chosen partly for being well-known and reasonably simple; more visually complex rulebooks (icons, diagrams, tables) may need a different or extended approach later.
- **Generalization is unproven — and now higher-stakes.** The fixed section structure and the comparison approach are hypotheses based on two games, but the goal is a schema that could extend to ~100 games; a Phase 1 schema that only fits Ticket to Ride and Catan comfortably would need rework before scaling. Different games (worker placement vs. route-building vs. deck-building, party games vs. heavy strategy games) may stress the schema in different ways.
- **Anchor-game knowledge depends on the model's general training, not this project's data.** Comparisons to games outside the pilot set (e.g., a future user's copy of Machi Koro) rely on the LLM already knowing that game well — quality may vary by how well-known the anchor game is.
- **Roadmap after v1 is intentionally undecided** beyond the items logged in §13.

## 11. Technical Approach (brief)

- **Extraction & structuring:** Python scripts calling the Claude API (vision-capable model) — a pass to extract raw content from each page image, then a pass to organize content into the fixed section structure, per game.
- **Comparison generation:** a further LLM pass (or combined step) that takes a game's structured rules and produces the comparison pitch, drawing on the model's general board-game knowledge plus (for the pilot) the other processed game's structured data.
- **Storage:** Markdown files per game, colocated with or referencing the source rulebook photos.
- **Source material:** existing "Boardgame Rulebooks" folder of page photos, organized one subfolder per game. Ticket to Ride currently has 3 photos; Catan photos still need to be added.
- Further architectural detail (repo structure, exact prompts, file schema — the specific Phase 1 questions raised in §2 and §7) to be worked out collaboratively as implementation begins — deliberately kept light here since Myles is writing the code and the design will evolve through that process.

## 12. Phase 1 Design Decisions

These were the open Phase 1 questions raised because of the ~100-game scaling ambition; all are now resolved and reflected in §7/§8 above.

- **Schema:** an 11-part section set (Overview, Components, Setup, Turn Structure/Core Loop, Actions, Scoring & Win Conditions, End-of-Game Trigger, Special Rules/Variants, Edge Cases/FAQ, Glossary, Source references), stress-tested against Catan, Pandemic (cooperative), and Codenames (party game) before locking in. Two sections were deliberately generalized during that stress test: "Scoring & Win Conditions" (renamed from "Scoring" to explicitly cover shared win/loss with no numeric score) and "Turn Structure / Core Loop" (broadened to include automated/system steps, not just player actions).
- **Known gap, not solved now:** legacy/campaign games (persistent state and rules that change across sessions, e.g. Pandemic Legacy) break this schema. Neither pilot game needs it; logged in §14 as a future scenario rather than designed today.
- **Detail level:** near-verbatim. Nothing functional is summarized away; only pure flavor/marketing text is condensed.
- **Metadata:** YAML frontmatter per game (`title`, `player_count`, `playtime`, `mechanisms/tags`, `interaction_model`, `source_photos`, `date_processed`) — decided on rather than staying plain Markdown, specifically because `mechanisms/tags` is expected to be the main hook Phase 2 uses for cross-game comparison later.
- **File organization:** one Markdown file per game (frontmatter + all 11 sections), plus a top-level `games_index.md` catalog — started now rather than deferred to Phase 2, since it's cheap to maintain incrementally as each game is processed.

## 13. Source Material Inventory (as of 2026-09-01)

| Game | Photos | Notes |
|---|---|---|
| Ticket to Ride | 3 | **Pilot game for v1** |
| Catan | 0 | **Pilot game for v1 — action needed: photograph the rulebook and add it to the source folder before this game can be processed.** |
| Tapestry | 12 | Deferred |
| Trekking the National Parks | 10 | Deferred |
| Zooloretto | 7 | Deferred |
| Flamecraft | 1 | Deferred; existing image is a screen capture, not a rulebook photo — will likely need to be replaced |

Myles owns roughly 100 games in total; the remaining ~95 have not yet had rulebook photos taken. Expanding source material beyond the 5 folders above is a Phase 1 scaling activity, not required for the two-game pilot.

## 14. Scenarios / Backlog (lower priority, logged for future revisit)

| Scenario | Description | Priority | Phase |
|---|---|---|---|
| Difficulty/complexity scoring | "How hard will this be for me to learn" — either AI judgment from general game knowledge, or relative complexity compared across processed games. Explicitly deferred from v1; worth revisiting once the comparison pitch is solid. | Low | 2/3 |
| Browsable game library / picker | A simple UI or list to pick from games you own, beyond just running the pipeline directly on two named games. | Low-Medium | 3 |
| Expand to remaining photographed games | Tapestry, Trekking the National Parks, Zooloretto, Flamecraft. | Medium | 1 |
| Expand toward full ~100-game collection | Photograph and process the rest of Myles's collection. | Low (long-term) | 1 |
| Cross-game search/query | Ask a question and get an answer pulling from multiple processed games' rules. | Low-Medium | 2/3 |
| Official errata/FAQ ingestion | Pull in publisher errata/FAQ documents beyond the printed rulebook. | Low | 1 |
| Public-facing / multi-user | Requires resolving the copyright/IP risk (§10) before any real consideration. | Not committed | 3 |
| Legacy/campaign game support | The Phase 1 schema doesn't capture persistent, session-to-session state (e.g. Pandemic Legacy). Not needed for the pilot; revisit if/when such a game is processed. | Low (until relevant) | 1 |

## 15. Roadmap

- **v1 (current):** Phase 1 pilot — Ticket to Ride + Catan, comparison pitch + structured reference, Markdown file output, manually verified.
- **Beyond v1:** intentionally undecided beyond the candidates logged in §14. Phase 2 (Analysis) and Phase 3 (Presentation) are named but not scoped yet — see §2.

## 16. Decision Log

| Decision | Choice |
|---|---|
| Project structure | Three phases: (1) Extraction & Storage, (2) Analysis, (3) Presentation/User-Facing Functions. v1 = Phase 1 only. |
| Scale consideration | Myles owns ~100 games; Phase 1's schema/storage design should generalize to that scale even though the pilot covers only 2 games. |
| Primary output (v1) | Comparison pitch ("if you know X, this is X + differences") — the headline feature |
| Secondary output (v1) | Structured rules reference (Setup/Turn Structure/Scoring/Edge Cases/Glossary), kept but no longer primary |
| Comparison basis | Well-known anchor games generally, using the model's own broad game knowledge — not limited to a personally-owned library |
| Pilot data approach | Process two real games (not one) so comparison logic has real structured data on both sides |
| Second pilot game | Catan (photos still need to be taken/added) |
| Storage format | Markdown (decided over JSON) |
| Phase 1 schema | 11-part section set per game (Overview, Components, Setup, Turn Structure/Core Loop, Actions, Scoring & Win Conditions, End-of-Game Trigger, Special Rules/Variants, Edge Cases/FAQ, Glossary, Source references); stress-tested against Catan, Pandemic, and Codenames |
| Detail level | Near-verbatim — no functional content summarized away |
| Metadata | YAML frontmatter per game: title, player_count, playtime, mechanisms/tags, interaction_model, source_photos, date_processed — no complexity/weight field |
| Index/catalog | `games_index.md` started now (not deferred to Phase 2) |
| Difficulty/complexity scoring | Deferred — logged in Scenarios/Backlog (§14) as lower priority, not designed in v1 |
| Machi Koro | Illustrative example only — not added to pilot scope |
| Browsable game library | Deferred to post-v1 (§14) |
| Primary purpose | Seed of a real product — design with future extension in mind even though v1 is narrow |
| Target user (v1) | Myles + his regular game group |
| Output form (v1) | Markdown files only — no CLI or web UI yet |
| Source scope | Printed rulebook only — no errata/FAQ in v1 |
| Verification approach | Manual review of both structured sections and comparison claims, against source rulebooks and Myles's own game knowledge |
| Flagged constraint | Copyright/IP noted as an open risk for any future public-facing direction |
| Stack | Python |
| Involvement model | Myles writes the code; Claude guides and reviews |
