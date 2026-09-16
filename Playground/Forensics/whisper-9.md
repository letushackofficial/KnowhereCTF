# Whisper-9
**Category:** Forensics · **Difficulty:** Medium
**Release Date:** 05-09-2026 · **Close Date:** 16-09-2026 · **Author:** letushackofficial

## Description
A drone's flight recorder is recovered after it went dark mid-mission. A technical bulletin describes most of the file format — but admits one part of the spec was left out of the public version.

## Flag Format
```
luh{the discovery}
```

## Solution

The bulletin explains the recorder's file format: it's a sequence of records, each with a tag, a length, some data, and a checksum. It documents three tag types — a plaintext log, telemetry data, and an embedded image — but it flags that one more, undocumented tag type might show up, and tells you to dump every record and identify each one by its raw bytes.

Write a small parser that walks the file using that record structure, verifies each checksum, and dumps every record's contents to its own file. You end up with four: a syslog (plain drone chatter, mostly flavor and backstory), a block of telemetry floats (a dead end — nothing hidden there), and two more worth a closer look.

One of those two starts with the bytes for "SQLite format 3" — it's a database, even though it wasn't in the documented tag list. The other starts with the standard PNG header — an ordinary-looking inspection-camera photo.

Open the database and query it, and you'll see a clean, gap-free conversation log. That gap-free numbering is itself the tell: a flight recorder logging every exchange shouldn't have such a tidy, round ending. SQLite's `DELETE` doesn't actually erase a row's bytes — it just unlinks it and marks the space free, and this database was never cleaned up (vacuumed). Searching the raw bytes of the database file (with `strings`, SQLite's own recovery tools, or a hex editor) turns up the "deleted" row sitting right there in the leftover space — and it's a full paragraph explaining exactly how the image hides its message: pixels use an indexed color palette, and certain palette entries come in near-identical pairs that differ by just one shade of blue. One member of each pair means a 0 bit, the other means a 1, read in normal left-to-right order, skipping any pixel whose color has no partner.

With that rule in hand, look at the image's palette: it's full of these near-duplicate pairs, each differing only in blue by 1 — invisible to the eye but easy to tell apart in code. Group the palette entries by their red and green values, pair each group's two members, assign 0 to the lower index and 1 to the higher, then walk the image's pixels in order and collect the bits from every pixel that has a partner. The first 32 bits give you a length, and everything after that is the message itself — and the flag is revealed.
