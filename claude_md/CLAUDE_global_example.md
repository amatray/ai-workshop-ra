# CLAUDE.md

<!--
A filled example of CLAUDE_global_template.md, for an invented research
assistant. Names and email addresses are made up. This is the file used on the
workshop slides: with it in place, "Draft an email to my supervisor telling her
the updated debt table is ready for her review" produces an email addressed to
Rosa that points to output/tables/.
-->

## Who I am

My name is Maria Fernanda. I am a Research Assistant at the Inter-American
Development Bank. I am based in Washington DC.

My supervisor is Rosa. Her email is rosa@example.org.

My work is cleaning and merging firm-level data, running regressions, and
producing tables for Rosa's projects. What I want help with: writing and
debugging do-files, checking merges, and formatting tables.

## Language

Everything is in English.

## Tools

| Tool | What I use it for | Where the files live |
|------|-------------------|----------------------|
| Stata 18 | Analysis. Anything I rerun or hand over is a do-file | ~/Documents/projects/ |
| Python | Reading PDFs and calling data APIs | ~/Documents/projects/ |

Do not translate my Stata into Python because Python is easier for you.

## Where my files are stored

Projects live in ~/Documents/projects/, one folder per project.
I save finished tables in output/tables/ inside each project.

## My skill level

Stata intermediate; Python beginner; I have never used a terminal.

## How I prefer to work

- Be concise. When a request is ambiguous, say in one sentence which reading
  you are taking, then proceed.
- Ask before deleting a file or modifying one outside the current task.

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
