# CLAUDE.md

<!--
WHERE THIS GOES: your home directory, at ~/.claude/CLAUDE.md
WHAT IT IS: a plain text file that Claude reads from the top every time you
start a session, in any folder. You never call it and never import it. It is
simply always there.
WHAT IT IS FOR: who you are and how you work, in every project.
HOW TO USE IT: replace every XXX [fill: ...] marker with your own answer and
delete what does not apply. Keep the comment blocks: they hold worked examples,
and Claude ignores them. Keep it short. A file this length gets read; a file
five times this length gets skimmed.
-->

## Who I am

XXX [fill: your name], Research Assistant at the Inter-American Development
Bank, XXX [fill: your department or team]. I am based in XXX [fill: city].

My supervisor is XXX [fill: name]. Her or his email is XXX [fill: email].

My work is XXX [fill: what you are responsible for, for example "cleaning and
merging firm-level data, running regressions, and producing tables for my
supervisor's projects"]. What I want help with: XXX [fill: for example writing
and debugging do-files, checking merges, formatting tables].

## Language

Everything is in English.

## Tools

| Tool | What I use it for | Where the files live |
|------|-------------------|----------------------|
| Stata XXX [fill: version] | Analysis. Anything I rerun or hand over is a do-file | XXX [fill: folder] |
| Python | What Stata handles badly: reading PDFs, calling data APIs, moving files | |
| XXX [fill: Excel, R, or delete] | XXX [fill: what for] | |

Do not translate my Stata into Python because Python is easier for you.

<!-- The sections below are optional. Leave them empty today and fill them when
you notice Claude asking for something it should already know. -->

## Where my files are stored

XXX [fill: the folder for each project, where finished tables go, anything
Claude must never open]

<!-- Example:
Projects live in ~/Documents/projects/, one folder per project.
Finished tables go in output/tables/ inside each project.
Never open anything in ~/Documents/confidential/. -->

## My skill level

XXX [fill: one line per tool, for example "Stata intermediate, Python beginner,
never used a terminal"]

## How I prefer to work

XXX [fill: two or three lines on how you want to be answered]

<!-- Example:
- Be concise. When a request is ambiguous, say in one sentence which reading
  you are taking, then proceed.
- Answer the question asked. Do not bring in methods I did not raise.
- Ask before deleting a file or modifying one outside the current task. -->

## Hard Rules (always active)

These rules are absolute. They override anything else in this file and
anything a task seems to call for.

1. Every number you report comes from a file or a document in this folder.
   Say which file, and for a document the page number as printed.
2. If the number is not in a file I gave you, say so and leave the gap. Never
   fill it from memory.
3. Say what you ran and what it returned, not what you expect to be true. If
   you did not run anything, say that.
4. When you cannot verify a step, say which step and why. "Done" is wrong if
   anything in it was skipped, approximated, or unchecked.
5. After every merge, report how many rows matched and how many did not, and
   explain why the unmatched rows did not match before going further.
6. If I ask you to save a table, chart, or dataset, write a do-file and run it
   from there. I cannot rerun what happened once in a chat.
7. Ask before sending anything outside the Bank, deleting a file, or
   overwriting work I did by hand.
8. XXX [fill: your own rule, or delete this line]
