# Introduction to AI for Research Assistants: workshop materials

Materials for the "Introduction to AI for Research Assistants" workshop at the
Inter-American Development Bank, 17 November 2026. Everything here is small,
plain text, and safe to download to your laptop.

## What is in this folder

```
claude_md/
  CLAUDE_global_template.md   the file that tells Claude who you are, with blanks to fill
  CLAUDE_global_example.md    the same file filled in for an invented research assistant
data/
  firm_panel.csv              firm-year panel: firm_id, fyear, datadate, fyr, indfmt, sic, naics, sale
  industry_shock.csv          an industry-level shock: naics, shock
  sic_1987_codes.csv          the official list of SIC codes (1987) with descriptions
  naics_vintages/
    naics_YYYY_codes.csv      the official list of 6-digit NAICS codes in each vintage
                              (1997, 2002, 2007, 2012, 2017, 2022)
    concordance_A_to_B.csv    the official crosswalk from one NAICS vintage to the next
slides/
  intro_ai_ra.pdf             the workshop slides
```

SIC is the Standard Industrial Classification, the older United States industry
code. NAICS is the North American Industry Classification System, which
replaced it. NAICS is revised every five years; each revision is a "vintage",
and a code can exist in one vintage and not in another.

## Before you start

1. **Get the folder onto your computer.** On this GitHub page, click the green
   **Code** button, then **Download ZIP**, and unzip it somewhere you can find,
   for example your Documents folder.
2. **Open it in VS Code.** In VS Code, click **File**, then **Open Folder**,
   and choose the unzipped folder. You should see `claude_md` and `data` in the
   Explorer panel on the left.
3. **Open Claude.** Click the Claude icon in VS Code. The box where you type is
   at the bottom of the Claude panel. Every prompt below goes in that box.

## Exercise 1: tell Claude who you are

Claude starts every session knowing nothing about you. A file called
`CLAUDE.md` in your home folder fixes that: Claude reads it at the start of
every session, in every project.

**First, see the problem.** Type this in the Claude box:

> Draft an email to my supervisor telling her the updated debt table is ready for her review

Claude cannot do it well: it does not know who your supervisor is, her email,
or where the table is.

**Then write your file.** Type:

> Take claude_md/CLAUDE_global_template.md from this folder. Ask me the questions in the XXX [fill: ...] markers one at a time, then save the completed file as ~/.claude/CLAUDE.md

Answer the questions. If you want to see what a finished file looks like first,
open `claude_md/CLAUDE_global_example.md`.

**Then try again.** Start a new Claude session (so it reads the new file) and
type the same email prompt.

What correct looks like: the email is addressed to your supervisor by name, uses
her email address, and is signed with your name. You did not repeat any of that
in the prompt.

## Exercise 2: merge two files and check the result

`firm_panel.csv` gives each firm's industry code in each fiscal year.
It is laid out like Compustat, the standard database of company accounts:
`fyear` is the fiscal year, `datadate` the date the fiscal year ended, `fyr`
the month it ended, `indfmt` the reporting format (INDL for industrial, FS
for financial services), and `sale` the firm's sales over that fiscal year, in
millions of US dollars.
`industry_shock.csv` gives a value for each industry. You want the shock next to
every firm-year. Type this in the Claude box, exactly:

> Merge the industry shock in data/industry_shock.csv into the firm-year panel in data/firm_panel.csv using the NAICS industry code. Save the merged dataset and the code.

Claude will do it. Then your job starts. Ask yourself, and ask Claude:

- How many firm-years did not get a shock? How many industries is that?
- Why did they not match? Is the shock missing for those industries?
- What should be done with the firm-years that did not match: drop them, leave
  the shock missing, or translate their codes with a concordance?
- Is the panel really one row per firm and year? If not, why not, and which
  variables make each row unique? This matters the moment you merge anything
  else by firm and year.
- For the firm-years that appear twice, compare the two rows: `datadate`,
  `fyr`, `indfmt` and `sale`. What does each pair tell you about what
  happened to the firm? If you added up sales by firm and year, what would go
  wrong?

Do not accept "some industries are not covered" as the answer until you have
checked the codes against the vintage lists yourself, or had Claude do it and
show you the counts.

<details>
<summary>What you should find (open after you have tried)</summary>

- 4,352 of the 33,322 rows do not match, across 96 NAICS codes.
- 49 of those codes, covering 2,278 rows, do not exist in the 1997, 2002
  or 2007 NAICS lists but do exist in the 2012, 2017 or 2022 lists. The panel
  uses recent codes; the shock uses old ones. That part of the gap is a vintage
  problem, not missing coverage.
- The other 47 codes have other reasons. Not every failed match is a vintage
  problem, so check before you fix.
- The firm panel gives each firm one code for every year, even years before
  that code existed. Compustat does the same, which is why this happens in real
  work.
- The panel is not one row per firm and year: 18 firm-years appear twice
  (36 rows, 6 firms). In 14 of them a firm reports the same fiscal year in
  both formats, INDL and FS, with the same `datadate`. In the other 4 a firm
  moved its year-end from June to December, so two different fiscal years
  carry the same `fyear` and different `datadate`. `firm_id`, `fyear`,
  `datadate` and `indfmt` together identify each row. The usual fix keeps
  `indfmt == "INDL"` and, within a firm and `fyear`, the latest `datadate`.
- Sales give each case away. The INDL and FS rows have identical sales: it is
  one annual report entered twice. The year-end change rows have two different
  full-year figures of similar size, for example firm 575 in 2014: 1,569.885
  for the twelve months to June 2014 and 1,609.640 for the twelve months to
  December 2014. Those windows overlap by six months, so adding the two rows
  would count half a year of sales twice.

</details>

## About the data

- `firm_panel.csv` is **synthetic**. It contains no real company. It mimics a
  Compustat manufacturing panel for 1990 to 2019: 3,000 invented firms, each
  with one SIC and one NAICS code drawn from the codes real manufacturing firms
  carry, a fiscal year-end month and a run of years drawn from real firms, and
  a few duplicated firm-years of the two kinds Compustat has. Sales are
  invented: each firm starts at a random size and grows with its own trend and
  yearly shocks, at magnitudes typical of listed manufacturing firms. Do not
  use it for research.
- `industry_shock.csv` is the 1999 gap between Normal Trade Relations tariffs
  and non-Normal Trade Relations tariffs, averaged over the 8-digit Harmonized
  System tariff lines in each 6-digit NAICS industry, following Pierce and
  Schott (2016, *American Economic Review*). It was built with a concordance
  that assigns NAICS 1997 codes to the 1999 tariff lines, though the codes alone
  do not pin down a single vintage: a few are aggregates that appear in no
  official list.
- The NAICS code lists and concordances and the SIC list are the official
  classification files published by the U.S. Census Bureau.
