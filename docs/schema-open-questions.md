# Schema v0.1 — Open Questions from Real-World Conversion

All 9 photographed games have now been run through schema v0.1 (see `docs/processing-status.md`). This log collects every situation the conversions hit that the schema doesn't clearly resolve, what each conversion actually did about it (as a stopgap, not a ratified rule), and the decision still needed. Resolve an item by editing `docs/schema.md`, bumping its Version History, and updating this file to say what was decided and when.

## 1. Required frontmatter fields with no source in the photos (`player_count`, `playtime`)

The schema marks these required, but 5 of 9 games don't print one or both anywhere in their photographed pages (this info often lives only on the box side/back, which isn't always in the photo set). Every conversion improvised a different stopgap:

| Game | Field(s) missing | What it wrote |
|---|---|---|
| Catan | `player_count`, `playtime` | `"not stated in source photos"` |
| Architects of the West Kingdom | `playtime` | `"Not stated in the photographed rulebook pages"` |
| Flamecraft | `playtime` | `"Not stated in the photographed rulebook pages"` |
| Trekking the National Parks | `playtime` | `"Not stated in the provided source photos"` |
| Zooloretto | `playtime` | field omitted entirely |

**Decision needed:** pick one convention — e.g. omit the field entirely when unknown (and drop "required" from the schema for these two fields), or a single fixed placeholder string, or require re-photographing the box for any game missing this before it's considered processed. Whatever's chosen, the 5 files above need a pass to match it.

## 2. Separate reference-guide/appendix photos don't map to one of the 11 sections

Two games shipped supplementary printed material beyond the main numbered rulebook (per `docs/naming-convention.md`'s `ReferenceGuide-NN` label):

- **Tapestry** (2 ReferenceGuide photos): a lookup card with two large tables (the full 33-card tech catalog; all 48 advancement-track space effects). Inlined into the closest topical sections (§2 Components, §5 Actions) with a note on the real source.
- **Architects of the West Kingdom** (8 ReferenceGuide photos): a genuine appendix *booklet*, explicitly cited by name in the main rulebook ("Refer to the Appendix for...") — not just a lookup aid. Contains full Apprentice ability text, full Building effect text, Solo Play rules, and Variable Setup character abilities. Inlined the same way, into §5 Actions and §8 Special Rules/Variants.

Both conversions followed the same "inline by topic" approach for consistency, but Architects' case is qualitatively different — that appendix is load-bearing core rules, not a supplementary card. **Decision needed:** is "inline into the closest topical section, note the real source photo" the permanent rule, or does a separate reference/appendix document deserve its own schema section (e.g. a 12th section, or an explicit subsection convention) so it isn't scattered across §2/§5/§8 depending on content?

## 3. Large per-card/per-tile text libraries ("a card database bolted onto the rules")

Several games have many individual cards/tiles each with their own printed rule text — more like a card database than prose rules:

- **Tapestry**: 33 tech cards (fully transcribed into a table, §2).
- **Architects of the West Kingdom**: 18 Apprentice types + ~30 Buildings (fully transcribed, §5).
- **Flamecraft**: 28 Shops, several Fancy Dragons, 7 Companions, 11 Solo Achievements — only *partially* transcribed. The agent named the cards and included only what it could clearly read (e.g. the 6 Artisan Dragon abilities), citing both "no natural home in the 11-part schema" and photo legibility as reasons for stopping short.

**Decision needed:** two separate questions here —
   (a) Should full per-card text always be attempted (as Tapestry/Architects did), or is naming the cards plus a representative sample acceptable when the set is large? This affects how "near-verbatim" gets applied to card-heavy games.
   (b) Does a large card library deserve a dedicated section/convention (e.g. "Card Reference") instead of being folded into whichever topical section seems closest?

## 4. Photo legibility limits (not a schema question, but recurring enough to log)

Three separate illegibility issues came up, all handled the same defensible way (flag it, don't invent the missing text):
- **Zooloretto** — the final FAQ answer is cut off in the photographed page; question kept, answer marked not visible.
- **Architects of the West Kingdom** — two Virtue Track example VP values unreadable due to photo angle/rotation; noted in §9 rather than guessed.
- **Flamecraft** — the 7 Companion cards' ability text was too small/rotated to transcribe reliably; described the framework, didn't assert specific wording.

Not a schema gap, but worth a note for future photography: angle/rotation and small print are the recurring failure mode. No decision needed here, just logged.

## 5. Borderline strategy/flavor asides and terminology notes

Handled inconsistently across games — none of these is wrong exactly, but there's no stated rule for them:
- **Zooloretto**'s "Tactical Hints" (designer strategy advice, not a rule) — kept, placed in §8 as the closest physical-location fit, even though it isn't really a special rule.
- **Catan**'s "Tactics" sidebar (similar strategy advice) — omitted entirely, treated like flavor text.
- **Catan**'s aside that older editions called Knight Cards "Soldier Cards" — kept, placed in §8, though it's a terminology/edition note, not a variant. (Might fit better in §10 Glossary.)
- **Catan**'s 5th-edition publication/legal notice — omitted, treated like flavor text.

**Decision needed:** should strategy-advice asides be captured at all (and if so, where — a dedicated note, or omitted like flavor per the existing rule), and should edition/terminology asides go in §10 Glossary rather than §8?

## 6. Content that exists on physical components but wasn't photographed

**Tapestry**'s 16 Civilization mats each carry unique passive-ability text printed only on the physical mat — not on any rulebook page, so it's absent from `tapestry.md` entirely (noted inline). This isn't fixable by schema changes; it's a photography-completeness question: do card/mat text that isn't in the rulebook need their own photos for games where abilities live on components rather than in the book? Logged here since it'll recur for any game with player-mat or card-text abilities (worth checking Architects' Variable Setup character abilities and Flamecraft's Companions against this too).

## 7. Minor data-quality notes (already fixed or spot-check items, not schema questions)

- Catan's title was initially written as "CATAN" (matching box logo styling) — normalized to "Catan" for consistency with how every other game file spells its title.
- Zooloretto's agent flagged that two of Myles's listed photos (`-04`/`-05`) appear to cover facing pages in reverse order from the filenames' numbering — sequenced by actual content, but worth a quick look in case those two files are mislabeled.
