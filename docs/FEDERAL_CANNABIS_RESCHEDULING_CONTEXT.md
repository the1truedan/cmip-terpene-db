# Federal cannabis rescheduling context (Schedule III)

**Status:** historical / policy context for CMIP’s architecture docs — **not legal advice**, not a claim about finished full-plant rescheduling of all marijuana under the CSA, and **not chemistry data**.

CMIP is a **schema and open-data sourcing plan**. Federal scheduling matters because it shapes **research access**, banking friction, and how seriously open chemistry provenance can be treated as infrastructure. This page records **citable White House and DOJ primary sources** so the repo’s public story stays tied to official text.

## What President Trump signed (primary)

### Executive Order — 18 December 2025

President **Donald J. Trump** signed the executive order  
**“Increasing Medical Marijuana and Cannabidiol Research”** (18 December 2025).

Among other research-access directions, **Section 2** instructs the **Attorney General** to:

> take all necessary steps to complete the rulemaking process related to **rescheduling marijuana to Schedule III** of the CSA in the most expeditious manner in accordance with Federal law, including 21 U.S.C. 811.

| Document | Official link |
|----------|----------------|
| **Executive Order (full text)** | [https://www.whitehouse.gov/presidential-actions/2025/12/increasing-medical-marijuana-and-cannabidiol-research/](https://www.whitehouse.gov/presidential-actions/2025/12/increasing-medical-marijuana-and-cannabidiol-research/) |
| **White House fact sheet** | [https://www.whitehouse.gov/fact-sheets/2025/12/fact-sheet-president-donald-j-trump-is-increasing-medical-marijuana-and-cannabidiol-research/](https://www.whitehouse.gov/fact-sheets/2025/12/fact-sheet-president-donald-j-trump-is-increasing-medical-marijuana-and-cannabidiol-research/) |

**Important precision (do not over-claim):**

- The **EO itself directs expedited completion of rulemaking**; it is **not** a one-line statute that silently rewrites every CSA schedule entry by presidential signature alone.
- Downstream agency action still matters (see DOJ below).
- CRS and other legal summaries emphasize the distinction between **presidential direction** and **final administrative rescheduling**. See e.g. [Congress.gov CRS LSB11105](https://www.congress.gov/crs-product/LSB11105) (updated after the EO).

### White House “365 wins” summary language

A White House release summarizing first-year actions includes a short line that the President **signed an executive order reclassifying marijuana to Schedule III** in the sense of advancing that policy track:

- [https://www.whitehouse.gov/releases/2026/01/365-wins-in-365-days-president-trumps-return-marks-new-era-of-success-prosperity/](https://www.whitehouse.gov/releases/2026/01/365-wins-in-365-days-president-trumps-return-marks-new-era-of-success-prosperity/)

Prefer the **EO text + fact sheet** as the binding primary sources; treat press summaries as secondary.

## Prior administrative track (pre-EO)

| Step | What happened | Link |
|------|----------------|------|
| HHS / FDA / NIDA scientific recommendation (2023 era) | Support for moving marijuana toward **Schedule III** (accepted medical use framing) | Summarized in the White House EO / fact sheet |
| DOJ/DEA **Notice of Proposed Rulemaking** | **21 May 2024** — proposed rescheduling marijuana **I → III** | [Federal Register 2024-11137](https://www.federalregister.gov/documents/2024/05/21/2024-11137/schedules-of-controlled-substances-rescheduling-of-marijuana) |

## DOJ follow-on (2026) — medical products track

On **~23–24 April 2026**, the Justice Department announced actions **in accordance with** the 18 December 2025 EO, including:

- placing **FDA-approved products containing marijuana** and **qualifying state-licensed medical marijuana products** into **Schedule III** under specified authorities; and  
- initiating an **expedited administrative hearing** path concerning **broader** rescheduling of marijuana **I → III** (hearing calendar noted beginning **29 June 2026** in DOJ materials).

| Document | Official link |
|----------|----------------|
| **DOJ press release** | [https://www.justice.gov/opa/pr/justice-department-places-fda-approved-marijuana-products-and-products-containing-marijuana](https://www.justice.gov/opa/pr/justice-department-places-fda-approved-marijuana-products-and-products-containing-marijuana) |

**Again: precision.** That announcement is **not** the same sentence as “all cannabis plant material and all commercial markets are fully Schedule III forever.” CMIP docs should describe **what the primary sources say**, not media shorthand.

## Why this belongs in a **schema** repo

1. **Research climate** — Schedule I framing blocked ordinary medical-research workflows; Schedule III framing is explicitly about **accepted medical use** and research practicality (White House fact sheet language).  
2. **Provenance culture** — as federal research barriers ease, **citable chemistry** (PubChem, ChEBI, NIST, ChEMBL, …) becomes more valuable than unvetted scrapes.  
3. **CMIP’s open-data pivot** — this repo still ships **no** compound tables, **no** COAs, **no** scraped strain dumps. Scheduling history is **policy context**, not a substitute for [open data source pathways](OPEN_DATA_SOURCE_PATHWAYS.md).

## Link to open sources vs withheld private pile

| Track | What it is | Where documented |
|-------|------------|------------------|
| **Open, citable sources** | PubChem, ChEBI, KEGG, NIST, ChEMBL, Dr. Duke’s, … | [OPEN_DATA_SOURCE_PATHWAYS.md](OPEN_DATA_SOURCE_PATHWAYS.md) |
| **Withheld private staging pile** | Earlier opportunistic CSV / structure / spectra / partial Excel — **no clear redistribution trail** | Same doc · **not loaded into this repo** |
| **Frequency word cloud only** | Token counts from the unverified pile (size ∝ repeats; not measurements) | [assets/withheld-corpus-lexical-context.svg](assets/withheld-corpus-lexical-context.svg) · [frequency JSON](assets/withheld-corpus-word-frequency.json) |

**The withheld pile is not science in this repo.** It is not cited as evidence. The public viz is **silly-but-honest word frequency** of unverified staging text — not open chemistry for `/core`.

## Non-affiliation & medical disclaimer

- Independent architecture notes; **not** affiliated with the White House, DOJ, DEA, HHS, or any lab.  
- **Not medical advice.** Scheduling changes do not make any product safe, effective, or legal in every jurisdiction.  
- Always re-check **current** Federal Register / CSA schedules before relying on status for compliance.

## Related

- [README.md](../README.md)  
- [OPEN_DATA_SOURCE_PATHWAYS.md](OPEN_DATA_SOURCE_PATHWAYS.md)  
- [CONVERSATION_PROVIDERS.md](CONVERSATION_PROVIDERS.md)  
