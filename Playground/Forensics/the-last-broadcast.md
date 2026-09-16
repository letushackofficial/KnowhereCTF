# The Last Broadcast
**Category:** Forensics · **Difficulty:** Easy
**Release Date:** 05-09-2026 · **Close Date:** 16-09-2026 · **Author:** letushackofficial

## Description
A relay station sends back a photo and a set of case notes before it goes quiet. The notes hint that a salvage tool mangled the file on its way out — recover it, and see what's really being said.

## Flag Format
```
luh{the discovery}
```

## Solution

Start by looking at the image file. Running `file` on it says "data" instead of "PNG image data" — the header's broken. A hex dump shows why: there are 4 junk bytes stuck in front of the real PNG signature, and the checksum on the first chunk (IHDR) has been zeroed out. Strip those junk bytes off the front and recompute that checksum, and the file opens normally — a night-sky photo of the relay station.

Nothing's visible in the image itself, so check the metadata next. `exiftool` turns up three useful fields: the camera model, the exact timestamp the photo was taken, and a "User Comment" field full of uppercase text ending in `=` — that's Base32. Decode it and you get a full paragraph of instructions: the real payload is hidden in the blue channel's least-significant bit, the pixels aren't read in normal order but in a scrambled order driven by a well-known pseudo-random formula (an LCG) seeded with the photo's timestamp, and the extracted bytes turn out to be a password-protected ZIP.

Convert that timestamp to a Unix epoch (using UTC, not local time), then write a small script that runs the LCG from that seed, uses it to generate a pixel order, and reads the blue channel's last bit from each pixel in that order. The first 32 bits tell you how long the payload is; the rest is the payload itself. Run it, and out comes a ZIP file.

That ZIP is locked. The comment also told you the password rule: it's the first 12 hex characters of MD5 of the camera model and the timestamp combined. Hash that, use it to unlock the archive, and inside is a short voice memo and a note that says the message isn't meant to be heard — it's meant to be looked at.

That's your cue to generate a spectrogram of the audio (with `sox`, or Audacity's spectrogram view). Text has been baked directly into the sound's frequency pattern, and it shows up as visible glyphs across the spectrogram image — and the flag is revealed.
