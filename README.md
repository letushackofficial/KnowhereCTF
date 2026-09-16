# Knowhere CTF

A collection of solutions for Knowhere CTF challenges, organized by competition format and category.

## About

This repo holds notes and solving processes for Knowhere CTF challenges. It is mainly for reference, but may also help anyone working through the same problems.

## Index

| Format | Category | Challenge | Difficulty |
|---|---|---|---|
| Playground | Forensics | [The Last Broadcast](https://github.com/letushackofficial/KnowhereCTF/blob/main/Playground/Forensics/the-last-broadcast.md) | Easy |
| Playground | Forensics | [Whisper 9](https://github.com/letushackofficial/KnowhereCTF/blob/main/Playground/Forensics/whisper-9.md) | Medium |
| Playground | Miscellaneous | [Cosmic Signal](https://github.com/letushackofficial/KnowhereCTF/blob/main/Playground/Miscellaneous/cosmic-signal.md) | Easy |
| Playground | Osint | [Quizzle](https://github.com/letushackofficial/KnowhereCTF/blob/main/Playground/Osint/quizzle.md) | Easy |

## Structure

```
.
├── Playground/
│   ├── Forensics/
│   │   ├── the-last-broadcast.md
│   │   └── whisper-9.md
│   ├── Miscellaneous/
│   │   └── cosmic-signal.md
│   └── Osint/
│       └── quizzle.md
├── Battleground/
└── README.md
```

`Playground` contains the current Knowhere CTF challenges grouped by category. `Battleground` is reserved for future challenge solutions. Every challenge gets a single markdown file.

## Solution Format

Each solution file follows roughly this structure:

```markdown
# Challenge Name
**Category:** ... · **Difficulty:** ...
**Release Date:** DD-MM-YYYY · **Close Date:** DD-MM-YYYY · **Author:** ...

## Description
(challenge prompt, as given)

## Flag Format
\`\`\`
flag{...}
\`\`\`

## Solution
(step-by-step process)
```
