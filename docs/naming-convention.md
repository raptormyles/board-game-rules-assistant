# Rulebook Photo Naming Convention

This document describes the naming convention used for raw rulebook photos in the local `Boardgame Rulebooks` folder (iCloud, not committed to either repo). It exists so the convention is recorded somewhere durable and versioned, even though the photos themselves stay local-only.

## Folder names

Each game gets one subfolder, named after the full board game title exactly as it appears on the box (e.g. `Trekking The National Parks`, `Ticket To Ride`).

## File names

```
<FullFolderNameInPascalCaseNoSpaces>-<Label>.<ext>
```

- Take the folder name, strip spaces, and PascalCase it (e.g. `Trekking The National Parks` → `TrekkingTheNationalParks`).
- Keep the original file extension (`jpeg`, `jpg`, `png`, `heic`, etc.).
- `<Label>` is one of:

| Label | Meaning |
|---|---|
| `01`, `02`, `03`, ... | Zero-padded, two-digit numbered rulebook pages, in reading order |
| `BoxFront` / `BoxBack` | Photos of the physical game box (not the rulebook itself) |
| `FrontCover` / `BackCover` | The rulebook booklet's own first/last page |
| `SoloRules-01`, `SoloRules-02`, ... | Pages of a distinct solo-play insert booklet, bound separately from the main rulebook (e.g. an "Automa" booklet) |
| `ReferenceGuide-01`, `ReferenceGuide-02`, ... | Separate reference/appendix sheets that aren't part of the main numbered rulebook sequence |

### Examples

```
Ticket To Ride/
  TicketToRide-FrontCover.jpeg
  TicketToRide-01.jpeg
  TicketToRide-BackCover.jpeg

Tapestry/
  Tapestry-BoxFront.jpeg
  Tapestry-FrontCover.jpeg
  Tapestry-01.jpeg
  Tapestry-02.jpeg
  Tapestry-BackCover.jpeg
  Tapestry-SoloRules-01.jpeg
  ...
  Tapestry-SoloRules-05.jpeg
  Tapestry-ReferenceGuide-01.jpeg
  Tapestry-ReferenceGuide-02.jpeg
```

## Status

Applied to all photographed folders as of 2026-09-01: Ticket To Ride, Zooloretto, Trekking The National Parks, Tapestry, and Flamecraft. No stray camera-default filenames (`IMG_XXXX`, `StreamCam ...`) remain.

A naming-compliance check can be run on demand (fired manually, no fixed schedule) against the local `Boardgame Rulebooks` folder to flag any future non-compliant files — it reports issues only and does not rename anything automatically.
