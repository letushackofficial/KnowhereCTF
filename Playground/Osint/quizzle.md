# Quizzle
**Category:** Misc · **Difficulty:** Easy
**Release Date:** 05-09-2026 · **Close Date:** 16-09-2026 · **Author:** letushackofficial

## Description
A rover named g3kko.g left a cryptic message buried somewhere online. Your job: find the account, follow the trail, and dig out the message.

## Flag Format
```
LUH{the discovery}
```

## Solution

Start by tracking down g3kko.g on Instagram. The account has a bunch of odd posts, and a couple of them are just rickroll links thrown in to waste your time — ignore those.

Look closer and you'll notice several posts contain pieces of a QR code, split across them. Download each of those images individually, then stitch them together in an image editor (or just place them side by side) to rebuild the full QR code. Scan the reconstructed code and you get a long base64-looking string.

Decode it and you get three things, in this order: an invite link, a key, and an IV. One of the posts has a comment that says "cheff likes it with key and IV" — a nod to CyberChef, and "A+", "E+", "S" spells out AES if you squint. If you don't already know what AES is, this is the point where a quick search tells you enough to keep going.

Follow the invite into the Discord server. Search the server for the word "flag" and you'll turn up a barcode. Scan it and pull the string out of it — that's your ciphertext, and it's in hex.

At this point you've got everything CyberChef needs: the key (hex), the IV (hex), and the input (the barcode string, also hex). Set up an AES decrypt recipe with those three values and let it run — the raw output is the flag, revealed.
