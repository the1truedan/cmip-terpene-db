# Open data source pathways (planned outline)

**Status:** planning document only — no data pulled, no pipeline built. This
maps the schema modules in the main [README](../README.md) to legitimate
open/public-domain data sources, so the eventual ETL has a sourcing plan
before anyone writes a loader.

## How this pivot came to be

The earliest work on this project wasn't a sourcing plan — it was a pile of
data. A run of chat-driven sessions pulled together a large, real dataset:
a many-thousand-row strain/cultivar CSV, a multi-thousand-entry compound
structure export, spectral files, and a couple of Excel schema templates
that had already been partly seeded with real compound rows. It looked like
a running start — the raw material for exactly the kind of chemistry
database this repo's README describes.

Then came the second look. None of that data had a clear paper trail: it had
been gathered opportunistically, not sourced from a named database with
known terms, and there was no way to say with confidence what could be
redistributed, republished, or shipped in a public-facing schema project
versus what was scraped from somewhere that never agreed to that. Real,
substantial, useful — and unvetted. Shipping it, or even designing around it
as if it were a settled foundation, would have meant building on ground
nobody had checked.

So the project redirected. Instead of treating that pile as the seed corpus,
this repo stays **schema and architecture only**, and this document exists
to plan a *different* path to the same data: named, licensed, or
public-domain sources — PubChem, ChEBI, KEGG, ChEMBL, NIST, USDA-ARS — each
with its access terms stated up front, so nothing goes into `/core` without
knowing exactly where it came from and what's allowed to be done with it.
The original pile isn't part of this plan; it's parked separately pending
its own licensing review, and won't be pulled into this repo's story until
that's resolved on its own terms.

## Scope and a deliberate exclusion

This outline covers **open, license-checked sources only**. It deliberately
excludes the already-collected scraped strain/spectra dataset referenced in
private staging notes elsewhere — that data's scraping and redistribution
terms are unconfirmed, so it stays out of this repo (and out of this plan)
until reviewed separately on its own terms. Everything below is either
public-domain (US government / USDA-ARS work), or a named database with its
license/access terms called out explicitly so nothing gets mirrored on an
assumption.

## Sourcing rule, extended from "numbers need a story"

The README's design principle — a value carries units/method/citation/
confidence — applies to *where the value came from* too. Every source entry
below should eventually carry: license type, access method (API / bulk
download / manual), rate limits, which CMIP field(s) it fills, and a
redistribution note. Nothing gets bulk-mirrored without checking that note
first.

## Module-by-module source map

### Compound identity & structure — `Compounds`, `Synonyms`
- **PubChem** (NIH/NLM) — CID, IUPAC name, synonyms, InChI/InChIKey, SMILES,
  formula, molecular weight, exact mass, computed LogP/TPSA. Public domain;
  PUG REST API + bulk FTP.
- **ChemSpider** (RSC) — supplementary cross-ID resolution. Free tier; ToS
  restricts bulk redistribution — use for lookups, not mirroring.
- **ChEBI** (EBI) — curated small-molecule ontology; also feeds Classification
  below.

### Classification — ontology tree
- **ChEBI** — parent/child terms (Organic Compound → Terpenoid →
  Monoterpenoid → Alcohol → [compound]) instead of the flat categories the
  design explicitly rejects.
- **KEGG BRITE** hierarchies — terpenoid backbone biosynthesis classes.
  Free for academic/non-commercial use; commercial redistribution needs a
  license — flag before any public mirror.

### Functional chemistry / properties
- **NIST WebBook** — boiling point, melting point, density, vapor pressure,
  each with method + literature citation attached already. Free to browse;
  bulk scraping is restricted, so pull per-record with citation intact.
- **PubChem computed properties** — LogP/TPSA/solubility estimates, as a
  cross-check against NIST empirical values (computed vs. measured should
  stay distinguishable fields, not merged).

### Pathways — biosynthetic graph
- **KEGG Pathway** (`map00900` terpenoid backbone biosynthesis, `map00902`
  monoterpenoid biosynthesis, etc.) — precursor/enzyme/pathway edges.
- **MetaCyc / PlantCyc** — plant-specific pathway detail, EC numbers.
- **Reactome** — secondary, cross-species pathway context.

### Biological activity & protein targets
- **ChEMBL** — bioassay results (IC50/EC50/Ki) already shaped as
  compound/target/assay/confidence, matching the module's design directly.
- **Open Targets** — compound–target–disease association graph with
  genetic/clinical evidence scoring.
- **UniProt** — canonical target records (CB1/CNR1, CB2/CNR2, TRPV1, 5-HT1A,
  etc.) for the Protein Targets module.
- **PubMed / PMC** — primary-literature citations, so each biological-activity
  row's `evidence_level` and `confidence` are earned, not asserted.

*(Note: this session has live query access to ChEMBL, Open Targets, PubMed,
ClinicalTrials.gov, and bioRxiv/medRxiv via connected tools — small
prototype pulls for a handful of terpenes are feasible on request before any
real ETL is built.)*

### Clinical relevance (optional layer, evidence-only, not medical advice)
- **ClinicalTrials.gov** — registered trials on cannabinoids/terpenes for
  PTSD, chronic pain, cancer-symptom management; structured eligibility and
  endpoint data.
- **bioRxiv / medRxiv** — early entourage-effect research, explicitly flagged
  as non-peer-reviewed if pulled in.

### Cross-plant occurrence
- **Dr. Duke's Phytochemical and Ethnobotanical Databases** (USDA-ARS,
  public domain) — terpene occurrence across thousands of plant species;
  the natural source for a `common_in_other_plants`-style field.
- **FooDB** — food-source occurrence and aroma/flavor descriptors. Research-
  use license — check redistribution terms before any bulk mirror.
- **GBIF / USDA PLANTS** — taxonomic backbone for *Cannabis* and related
  Cannabaceae species (plant taxonomy context, not cultivar genetics).

### Regulatory / safety fields
- **FDA GRAS Notices database** — public, searchable; fills `fda_gras`.
- **IFRA standards** — access is restricted/paid; record this as an open gap
  rather than guessing a value.
- Seed-to-sale / COA data stays out of this list until a specific source's
  license is confirmed — do not backfill `coa_panel`-style fields from
  scraped data.

## Correlated-connections layer

The point of sourcing openly isn't just filling columns — it's letting the
schema express relationships across modules instead of leaving each field
isolated:

- **Property ↔ pathway** — boiling point/LogP (NIST/PubChem) against
  biosynthetic class (KEGG) turns "which compounds share an extraction
  profile" into a join, not a guess.
- **Pathway ↔ bioactivity** — precursor/enzyme chain (KEGG/MetaCyc) against
  receptor target (ChEMBL/Open Targets) lets you ask "which co-occurring
  compounds share both a biosynthetic precursor *and* a receptor target" —
  the entourage-effect question, answerable structurally instead of
  anecdotally.
- **Bioactivity ↔ clinical evidence** — ChEMBL/Open Targets preclinical
  binding data against ClinicalTrials.gov registered trials gives each
  `biological_activity` row an `evidence_level` that distinguishes
  preclinical-only from registered-trial-backed, instead of one flat label.
- **Occurrence ↔ classification** — Dr. Duke's cross-plant occurrence against
  ChEBI classification shows whether a reported effect is cannabis-specific
  or a broader terpenoid-class pattern (e.g., linalool's lavender occurrence
  contextualizes its own literature independent of cannabis-specific claims).

## Suggested build order

1. **Compound registry seed** — PubChem bulk pull for the terpenes/terpenoids
   already named in the design's example schema. Public domain, lowest
   licensing risk, unblocks everything downstream.
2. **Classification tree** — ChEBI ontology import for the same compound set.
3. **Pathway edges** — KEGG terpenoid-biosynthesis maps for precursor/enzyme
   fields.
4. **Bioactivity + targets** — ChEMBL/Open Targets/UniProt, each row
   citation-linked to PubMed.
5. **Clinical layer** (optional, later) — ClinicalTrials.gov cross-reference,
   kept clearly separate from preclinical evidence.
6. **Cross-plant occurrence** — Dr. Duke's for comparative context.
7. **Regulatory fields** — FDA GRAS only where a clean public record exists;
   leave IFRA/toxicity marked "gap, needs licensed source" rather than
   guessing.

Each phase follows the ETL layering already in the README: raw pull →
`/staging` normalize → `/core` load, with per-record license and citation
preserved — not a single bulk "source: PubChem" footnote covering everything.

## Explicit non-goals

- Does not include the previously-staged scraped strain/spectra dataset —
  excluded pending a separate licensing review.
- Does not stand up the actual Postgres/DuckDB/Neo4j warehouse — this is a
  sourcing plan, not an implementation.
