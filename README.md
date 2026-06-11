# Cytron Masters Remake

A modern web remake of **Cytron Masters** (SSI, 1982) — Dan Bunten's
(Danielle Bunten Berry's) proto-real-time-strategy game for the Apple II and
Atari 8-bit, and one of the earliest games recognizable as an RTS.

## Status

Research phase. Before writing any code, we are documenting everything
knowable about the original game: its complete mechanics, history,
reception, technical design, surviving artifacts, and legal status.

- **[Deep research report](docs/research/cytron-masters-research.md)** —
  the full, cited research document: gameplay rules, unit stats,
  development history, reception/sales, surviving manuals & disk images,
  IP analysis, and design lessons for the remake.

## Key takeaways so far

- The complete rules are recoverable: the original **manual and Bunten's
  Programmer's Notes are scanned on archive.org**, and disk images for both
  platforms run in modern emulators.
- **No prior remake exists** — this would be the first.
- The game is **not public domain** (copyright runs to ~2078; SSI's catalog
  chain ends at Ubisoft, with the Bunten estate a possible rights holder) —
  so the remake must be a from-scratch reimplementation of the mechanics
  with original code, art, sound, and text.
- The design's validated core to preserve: the capturable-generator energy
  economy, the hard-counter unit roster, and the fragile **Commander** unit
  as a group-order relay. The known flaws to fix: fixed 5/10-space movement
  deltas, weak AI, and battlefield legibility.
