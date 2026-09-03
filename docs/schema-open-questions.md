# Schema v0.1 — Open Questions from Real-World Conversion

All 9 photographed games were originally run through schema v0.1 (see `docs/processing-status.md`) and have since been upgraded to v0.2. This log collects every situation the conversions hit that the schema didn't clearly resolve, what each conversion actually did about it (as a stopgap, not a ratified rule), and the decision reached. All 4 real decision items (#1, #2, #3, #5) are now resolved, codified in `docs/schema.md` as v0.2, and reworked into every affected game file; items #4, #6, #7 are informational notes rather than open decisions. Resolve a future item by editing `docs/schema.md`, bumping its Version History, and updating this file to say what was decided and when.

## 1. Required frontmatter fields with no source in the photos (`player_count`, `playtime`) — RESOLVED 2026-09-02

**Decision:** both fields stay required. When not stated anywhere in the source photos, write the literal string `"unknown"` — don't guess, don't omit the field, don't use a longer descriptive placeholder. Codified in `docs/schema.md`.

Before this decision, every conversion had improvised a different stopgap:

| Game | Field(s) missing | What it wrote before the fix | Now |
|---|---|---|---|
| Catan | `player_count`, `playtime` | `"not stated in source photos"` | `"unknown"` (both fields) |
| Architects of the West Kingdom | `playtime` | `"Not stated in the photographed rulebook pages"` | `"unknown"` |
| Flamecraft | `playtime` | `"Not stated in the photographed rulebook pages"` | `"unknown"` |
| Trekking the National Parks | `playtime` | `"Not stated in the provided source photos"` | `"unknown"` |
| Zooloretto | `playtime` | field omitted entirely | `"unknown"` (field added) |

All 5 files above have been updated to match.

## 2. Separate reference-guide/appendix photos don't map to one of the 11 sections — RESOLVED 2026-09-02

**Decision:** a physically separate supplementary booklet or sheet — a `ReferenceGuide-NN` insert or a `SoloRules-NN` insert alike — gets its own new §11 "Supplementary Material" section in the same file, rather than being split across the topical sections by subject. Its content is preserved in that document's own physical page order (not reorganized by topic like the rest of the schema). Multiple supplementary documents in one game each get their own `####` subheading. Source References is renumbered §11 → §12. Codified in `docs/schema.md` as schema v0.2.

Before this decision, two games had shipped supplementary printed material beyond the main numbered rulebook, and both had scattered it across topical sections as a stopgap:

- **Tapestry** (2 ReferenceGuide photos): a lookup card with two large tables (the full 33-card tech catalog; all 48 advancement-track space effects) — had been inlined into §2 Components and §5 Actions.
- **Architects of the West Kingdom** (8 ReferenceGuide photos): a genuine appendix *booklet*, explicitly cited by name in the main rulebook ("Refer to the Appendix for..."), containing full Apprentice ability text, full Building effect text, Solo Play rules, and Variable Setup character abilities — had been inlined into §5 Actions and §8 Special Rules/Variants.
- **Tapestry** also has its Automa/Shadow Empire Solo Play content (5 SoloRules photos) nested inside §8 Special Rules/Variants — this also needs to move to §11 under the new rule, since Solo Rules booklets are in scope too.

**Rework needed:** DONE — `tapestry.md` and `architects-of-the-west-kingdom.md` both had their supplementary content extracted and moved into a new §11 (each in the source document's own physical order, under `#### Reference Guide` / `#### Solo Rules` subheadings where applicable), with the rest of each file renumbered accordingly and both bumped to schema_version "0.2".

## 3. Large per-card/per-tile text libraries ("a card database bolted onto the rules") — RESOLVED 2026-09-02

**Decision:** keep this content organized as close to how it physically appears in the rulebook as possible, and prefer full transcription over a partial/representative sample when the text is legible — consistent with the near-verbatim rule and with the §11 Supplementary Material approach from item #2 above (a card library that comes from a separate reference sheet goes in §11, in its physical order; one printed inline in the main numbered pages stays wherever the schema's topical sections already put it). A dedicated "Card Reference"/card-catalog feature (e.g. a structured, queryable database of every card in a game, separate from the narrative rules file) is a good idea for later, but is explicitly **out of scope for now** — logged as a backlog idea, not designed.

Before this decision:
- **Tapestry**: 33 tech cards, fully transcribed into a table (now relocated to §11 per item #2).
- **Architects of the West Kingdom**: 18 Apprentice types + ~30 Buildings, fully transcribed (now relocated to §11 per item #2).
- **Flamecraft**: 28 Shops, several Fancy Dragons, 7 Companions, 11 Solo Achievements — only *partially* transcribed, citing both "no natural home in the schema" and photo legibility as reasons for stopping short.

**Rework needed:** DONE — `flamecraft.md` got a fuller transcription pass: all 28 Shops' clarifications, the Sun/Moon Fancy Dragon clarifications, all 7 Companions (ability + clarification), and all 11 Solo Achievements (requirement + rewards) are now transcribed in §9/§8, matching the completeness standard Tapestry and Architects already met. A few individual lines carry an explicit residual-legibility caveat (photo angle/rotation on pgs. 15-19) rather than being invented outright — consistent with item #4's "flag it, don't invent" approach. Also bumped to schema_version "0.2" (§11 = "None," since this content lives in the main numbered rulebook pages, not a separate booklet).

## 4. Photo legibility limits (not a schema question, but recurring enough to log)

Three separate illegibility issues came up, all handled the same defensible way (flag it, don't invent the missing text):
- **Zooloretto** — the final FAQ answer is cut off in the photographed page; question kept, answer marked not visible.
- **Architects of the West Kingdom** — two Virtue Track example VP values unreadable due to photo angle/rotation; noted in §9 rather than guessed.
- **Flamecraft** — the 7 Companion cards' small printed icon text was too small/rotated to transcribe with full confidence; the larger, clearly-legible clarification text was used instead (see item #3's resolution), with the "as printed" ability wording flagged as an approximate paraphrase.

Not a schema gap, but worth a note for future photography: angle/rotation and small print are the recurring failure mode. No decision needed here, just logged.

## 5. Borderline strategy/flavor asides and terminology notes — RESOLVED 2026-09-03

**Decision:** flavor text and designer strategy-advice asides are kept, not condensed away — label each clearly as such (e.g. "*Flavor text:*" / "*Strategy tip:*") and place it wherever it physically sits in the source document, rather than moving it to a differently-matched topical section or omitting it. Codified in `docs/schema.md` as part of schema v0.2. Terminology/edition asides (e.g. Catan's old-edition card naming) stay wherever they're physically located too, by the same "location wins" principle — not specifically routed to §10 Glossary.

Before this decision, handling was inconsistent:
- **Zooloretto**'s "Tactical Hints" (designer strategy advice) — had been kept, in §8, but without an explicit "this is commentary, not a rule" label.
- **Catan**'s "Tactics" sidebar (similar strategy advice) — had been omitted entirely, treated like flavor text.
- **Catan**'s aside that older editions called Knight Cards "Soldier Cards" — kept, in §8; stays there under this decision.
- **Catan**'s 5th-edition publication/legal notice — omitted; this is publisher boilerplate rather than flavor or strategy content, so it stays omitted.

**Rework needed:** DONE — `catan.md`'s "Tactics" sidebar was re-transcribed from the source photo and added back into §8 with a "*Strategy tip:*" label; `zooloretto.md`'s Tactical Hints text was rewritten as a near-verbatim "*Strategy tip:*"-labeled passage (and its previously-omitted "Animal Encyclopedia" flavor content was added back too, with a "*Flavor text:*" label, since it's physically on the same source page). Both files also received the mechanical v0.2 upgrade (schema_version bump, §11 Supplementary Material, renumbered §12 Source References).

## 6. Content that exists on physical components but wasn't photographed

**Tapestry**'s 16 Civilization mats each carry unique passive-ability text printed only on the physical mat — not on any rulebook page, so it's absent from `tapestry.md` entirely (noted inline). This isn't fixable by schema changes; it's a photography-completeness question: do card/mat text that isn't in the rulebook need their own photos for games where abilities live on components rather than in the book? Logged here since it'll recur for any game with player-mat or card-text abilities (worth checking Architects' Variable Setup character abilities and Flamecraft's Companions against this too).

## 7. Minor data-quality notes (already fixed or spot-check items, not schema questions)

- Catan's title was initially written as "CATAN" (matching box logo styling) — normalized to "Catan" for consistency with how every other game file spells its title.
- Zooloretto's agent flagged that two of Myles's listed photos (`-04`/`-05`) appear to cover facing pages in reverse order from the filenames' numbering — sequenced by actual content, but worth a quick look in case those two files are mislabeled.
