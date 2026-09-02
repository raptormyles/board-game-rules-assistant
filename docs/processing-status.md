# Processing Status

Tracks every game with rulebook photos in the local "Boardgame Rulebooks" folder. As of 2026-09-02, all 9 photographed games have been read and converted to schema v0.1 — this file now mainly records what schema version each was built with, for whenever the schema changes and older files need revisiting. See `docs/schema-open-questions.md` for real gaps/ambiguities the schema didn't clearly resolve during these conversions.

Photo counts and completeness checks are based on file names against `docs/naming-convention.md` (a numbered `01..NN` sequence plus `FrontCover`/`BackCover` generally means the whole rulebook booklet was captured).

| Game | Photos | Numbered pages | Cover photos | Looks complete? | Read & saved? | Schema version | Data file | Date processed |
|---|---|---|---|---|---|---|---|---|
| Ticket to Ride | 3 | 01 (1 page) | FrontCover, BackCover | Yes | Yes | 0.1 | [games/ticket-to-ride.md](https://github.com/raptormyles/board-game-rules-assistant-data/blob/main/games/ticket-to-ride.md) | 2026-09-02 |
| Catan | 17 | 01–14 | FrontCover, BackCover, BoxFront | Yes | Yes | 0.1 | [games/catan.md](https://github.com/raptormyles/board-game-rules-assistant-data/blob/main/games/catan.md) | 2026-09-02 |
| Flamecraft | 21 | 01–19 | FrontCover, BackCover | Yes | Yes | 0.1 | [games/flamecraft.md](https://github.com/raptormyles/board-game-rules-assistant-data/blob/main/games/flamecraft.md) | 2026-09-02 |
| Trekking the National Parks | 10 | 01–06 | FrontCover, BackCover, BoxFront, BoxBack | Yes | Yes | 0.1 | [games/trekking-the-national-parks.md](https://github.com/raptormyles/board-game-rules-assistant-data/blob/main/games/trekking-the-national-parks.md) | 2026-09-02 |
| Canvas | 9 | 01–07 | FrontCover, BackCover | Yes | Yes | 0.1 | [games/canvas.md](https://github.com/raptormyles/board-game-rules-assistant-data/blob/main/games/canvas.md) | 2026-09-02 |
| Architects of the West Kingdom | 27 | 01–17 | none (BoxFront/BoxBack only) + ReferenceGuide 01–08 | Yes (confirmed by Myles 2026-09-02 — page 01/17 are the true first/last pages) | Yes | 0.1 | [games/architects-of-the-west-kingdom.md](https://github.com/raptormyles/board-game-rules-assistant-data/blob/main/games/architects-of-the-west-kingdom.md) | 2026-09-02 |
| Machi Koro | 12 | 01–10 | FrontCover, BoxFront (no BackCover) | Yes (confirmed by Myles 2026-09-02 — rulebook doesn't need a separate BackCover) | Yes | 0.1 | [games/machi-koro.md](https://github.com/raptormyles/board-game-rules-assistant-data/blob/main/games/machi-koro.md) | 2026-09-02 |
| Tapestry | 12 | 01–02 | FrontCover, BackCover, BoxFront; + ReferenceGuide 01–02, SoloRules 01–05 | Yes (confirmed by Myles 2026-09-02 — the 2-page core booklet is complete) | Yes | 0.1 | [games/tapestry.md](https://github.com/raptormyles/board-game-rules-assistant-data/blob/main/games/tapestry.md) | 2026-09-02 |
| Zooloretto | 7 | 01–06 | none (BoxFront only) | Yes (confirmed by Myles 2026-09-02 — no separate cover pages needed) | Yes | 0.1 | [games/zooloretto.md](https://github.com/raptormyles/board-game-rules-assistant-data/blob/main/games/zooloretto.md) | 2026-09-02 |

**Not yet photographed:** ~91 of Myles's ~100-game collection have no rulebook photos yet.

## Legend

- **Numbered pages** — the `01`, `02`, ... sequence from the naming convention; this is the main rulebook body.
- **Looks complete?** — "Yes" means either the numbered sequence has no gaps and both a `FrontCover`/`BackCover` exist, or (for the four rows noting "confirmed by Myles") a filename-based gap was flagged and Myles manually checked the photos against the physical rulebook and confirmed nothing is missing.
- **Schema version** — the `schema_version` value written into that game's frontmatter in the data repo, i.e. which revision of `docs/schema.md` it was built against.
