# Cosmic Signal
**Category:** Misc · **Difficulty:** Easy
**Release Date:** 05-09-2026 · **Close Date:** 16-09-2026 · **Author:** letushackofficial

## Description
Something's hiding in the transmission. Aliens left us a message — you just have to know how to look. Home sweet home ;-)

## Flag Format
```
luh{the discovery}
```

## Solution

There's no file to download and no instance to spin up — "home sweet home" is the giveaway that the challenge isn't on some attachment, it's sitting on the CTF platform's own homepage.

Open the homepage and inspect it (view-source or devtools), then search for `luh{`.

The first match is a dummy flag — a decoy planted to catch anyone who stops at the first hit. Keep going: hit next / search again, and the real flag turns up further down, revealed.
