# Project TODO

Running list of concrete next actions. See `PRD.md` for the full design and reasoning behind each of these.

## Recently completed
- [x] Establish and apply a rulebook-photo naming convention across all photographed folders — see `docs/naming-convention.md`
- [x] Resolve GitHub authentication friction — run `gh auth login` directly in Terminal on the Mac (stores credentials via the macOS keychain-backed git credential helper), replacing the earlier PAT/env-var workaround

## Setup (blocking before pipeline code starts)
- [ ] Decide Python environment tooling — venv, poetry, or uv — or confirm starting from scratch
- [ ] Confirm the Cosmos DB read-only enrichment approach for Phase 1 metadata: read `display_name`, player counts, playtime, `mechanisms`/`categories`, and `bgg_weight` from the existing `derosse-assistant-cosmos` database instead of deriving them from rulebook text (see PRD §12 discussion)
- [ ] Photograph Catan's rulebook and add the photos to `Boardgame Rulebooks/Catan` in the iCloud folder — needed to complete the two-game pilot (Ticket to Ride is already photographed)

## Housekeeping
- [ ] Approve the two scheduled tasks ("Rulebook Photo Naming Checker" and "Unpushed Commits Reminder") binding to this Mac in the desktop app — they're created but can't run against local files until approved
