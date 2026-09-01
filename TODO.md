# Project TODO

Running list of concrete next actions. See `PRD.md` for the full design and reasoning behind each of these.

## Setup (blocking before pipeline code starts)
- [ ] Decide Python environment tooling — venv, poetry, or uv — or confirm starting from scratch
- [ ] Confirm the Cosmos DB read-only enrichment approach for Phase 1 metadata: read `display_name`, player counts, playtime, `mechanisms`/`categories`, and `bgg_weight` from the existing `derosse-assistant-cosmos` database instead of deriving them from rulebook text (see PRD §12 discussion)
- [ ] Photograph Catan's rulebook and add the photos to `Boardgame Rulebooks/Catan` in the iCloud folder — needed to complete the two-game pilot (Ticket to Ride is already photographed)
