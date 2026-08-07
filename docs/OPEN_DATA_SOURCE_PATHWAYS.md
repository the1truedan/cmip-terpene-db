# Open data source pathways (planned outline)

**Status:** planning document only — no data pulled, no pipeline built. Maps schema modules in the [README](../README.md) to legitimate open/public-domain sources so eventual ETL has a sourcing plan before loaders exist.

Design chat attribution (Grok, ChatGPT, Claude, local models, …) lives in [CONVERSATION_PROVIDERS.md](CONVERSATION_PROVIDERS.md). **This file is only for chemistry/data sources.**

## Why open sources first

An earlier private staging pile (strain CSV, structure export, spectra, partially seeded Excel templates) looked useful but had **no clear redistribution paper trail**. Shipping or designing as if that pile were settled foundation was rejected.

This repo stays **schema and architecture only**. Open, named sources — each with access terms — are the planned path into `/core`. Unvetted private piles stay out until independently license-reviewed.

### Lexical viz of the withheld pile (not chemistry)

The withheld corpus is **not science** in this repository: no tables, no spectra files, no COA bodies. What *is* public is a **word-cluster** of the *story* of non-confirmation — license, scrape, provenance, open-path preference — sized by narrative weight:

- [assets/withheld-corpus-lexical-context.svg](assets/withheld-corpus-lexical-context.svg) · [PNG](assets/withheld-corpus-lexical-context.png)

Federal research climate (Schedule III track under the 18 Dec 2025 EO) is separate policy context: [FEDERAL_CANNABIS_RESCHEDULING_CONTEXT.md](FEDERAL_CANNABIS_RESCHEDULING_CONTEXT.md).

## Scope

Covers **open, license-checked sources only**. Excludes unconfirmed scraped strain/spectra corpora. Everything below is public-domain (e.g. US government / USDA-ARS) or a named database with explicit access notes.

## Sourcing rule

The README principle — values carry units/method/citation/confidence — applies to **provenance** too. Each planned source should eventually record: license type, access method (API / bulk / manual), rate limits, CMIP fields filled, and redistribution notes. No bulk mirror without that note.

## Module-by-module source map

### Compound identity & structure — `Compounds`, `Synonyms`

| Source | Role | Links |
|--------|------|--------|
| **PubChem** (NIH/NLM) | CID, IUPAC, synonyms, InChI/InChIKey, SMILES, formula, mass, computed LogP/TPSA. Public domain; PUG REST + bulk FTP | [Home](https://pubchem.ncbi.nlm.nih.gov/) · [Programmatic access](https://pubchem.ncbi.nlm.nih.gov/docs/programmatic-access) · [PUG REST](https://pubchem.ncbi.nlm.nih.gov/docs/pug-rest) · [PUG REST tutorial](https://pubchem.ncbi.nlm.nih.gov/docs/pug-rest-tutorial) · [About / data use](https://pubchem.ncbi.nlm.nih.gov/docs/about) |
| **ChemSpider** (RSC) | Cross-ID resolution; free tier; ToS limits bulk redistribution — lookups, not full mirrors | [https://www.chemspider.com/](https://www.chemspider.com/) |
| **ChEBI** (EMBL-EBI) | Curated small-molecule dictionary + ontology; also feeds Classification | [https://www.ebi.ac.uk/chebi/](https://www.ebi.ac.uk/chebi/) · [ChEBI 2.0 / open license notes](https://www.embl.org/news/updates-from-data-resources/chebi-2-0-launches/) · data commonly **CC BY 4.0** |

### Classification — ontology tree

| Source | Role | Links |
|--------|------|--------|
| **ChEBI ontology** | Parent/child terms (Organic Compound → Terpenoid → Monoterpenoid → …) | [https://www.ebi.ac.uk/chebi/](https://www.ebi.ac.uk/chebi/) |
| **KEGG BRITE** | Terpenoid backbone biosynthesis classes; academic/non-commercial free; commercial needs license | [https://www.genome.jp/kegg/brite.html](https://www.genome.jp/kegg/brite.html) · [KEGG license](https://www.kegg.jp/kegg/legal.html) |

### Functional chemistry / properties

| Source | Role | Links |
|--------|------|--------|
| **NIST Chemistry WebBook** | Boiling/melting points, density, vapor pressure with literature citations; bulk scraping restricted — per-record pull | [https://webbook.nist.gov/chemistry/](https://webbook.nist.gov/chemistry/) |
| **PubChem computed properties** | LogP/TPSA/solubility estimates; keep **computed vs measured** as distinct fields | [PUG REST](https://pubchem.ncbi.nlm.nih.gov/docs/pug-rest) |

### Pathways — biosynthetic graph

| Source | Role | Links |
|--------|------|--------|
| **KEGG Pathway** | e.g. `map00900` terpenoid backbone, `map00902` monoterpenoid biosynthesis | [https://www.genome.jp/kegg/pathway.html](https://www.genome.jp/kegg/pathway.html) · [map00900](https://www.genome.jp/pathway/map00900) |
| **MetaCyc / PlantCyc** | Plant pathway detail, EC numbers | [https://metacyc.org/](https://metacyc.org/) · [https://plantcyc.org/](https://plantcyc.org/) |
| **Reactome** | Cross-species pathway context | [https://reactome.org/](https://reactome.org/) |

### Biological activity & protein targets

| Source | Role | Links |
|--------|------|--------|
| **ChEMBL** | Bioassays (IC50/EC50/Ki) as compound/target/assay/confidence | [https://www.ebi.ac.uk/chembl/](https://www.ebi.ac.uk/chembl/) · [Web services](https://chembl.gitbook.io/chembl-interface-documentation/web-services) |
| **Open Targets** | Compound–target–disease associations with evidence scoring | [https://www.opentargets.org/](https://www.opentargets.org/) · [Platform](https://platform.opentargets.org/) |
| **UniProt** | Canonical targets (e.g. CNR1/CNR2, TRPV1, 5-HT1A) | [https://www.uniprot.org/](https://www.uniprot.org/) |
| **PubMed / PMC** | Primary literature for `evidence_level` / `confidence` | [https://pubmed.ncbi.nlm.nih.gov/](https://pubmed.ncbi.nlm.nih.gov/) · [https://pmc.ncbi.nlm.nih.gov/](https://pmc.ncbi.nlm.nih.gov/) |

### Clinical relevance (optional, evidence-only — not medical advice)

| Source | Role | Links |
|--------|------|--------|
| **ClinicalTrials.gov** | Registered trials; structured eligibility/endpoints | [https://clinicaltrials.gov/](https://clinicaltrials.gov/) · [API](https://clinicaltrials.gov/data-api/about-api) |
| **bioRxiv / medRxiv** | Preprints; flag non-peer-reviewed | [https://www.biorxiv.org/](https://www.biorxiv.org/) · [https://www.medrxiv.org/](https://www.medrxiv.org/) |

### Cross-plant occurrence

| Source | Role | Links |
|--------|------|--------|
| **Dr. Duke's Phytochemical and Ethnobotanical Databases** (USDA-ARS / NAL) | Cross-species terpene occurrence; public-domain US government work | [Search](https://phytochem.nal.usda.gov/search) · [Home](https://phytochem.nal.usda.gov/) · [Ag Data Commons record](https://agdatacommons.nal.usda.gov/articles/dataset/Dr_Duke_s_Phytochemical_and_Ethnobotanical_Databases/24660351) |
| **FooDB** | Food-source occurrence / aroma descriptors; check redistribution | [https://foodb.ca/](https://foodb.ca/) |
| **GBIF** / **USDA PLANTS** | Taxonomic backbone for *Cannabis* / Cannabaceae | [https://www.gbif.org/](https://www.gbif.org/) · [https://plants.usda.gov/](https://plants.usda.gov/) |

### Regulatory / safety fields

| Source | Role | Links |
|--------|------|--------|
| **FDA GRAS Notices** | Public notices for `fda_gras` where a clean record exists | [https://www.fda.gov/food/generally-recognized-safe-gras/gras-notice-inventory](https://www.fda.gov/food/generally-recognized-safe-gras/gras-notice-inventory) |
| **IFRA standards** | Restricted/paid access — record as an open gap, do not invent values | [https://ifrafragrance.org/](https://ifrafragrance.org/) |

Seed-to-sale / COA bulk data stays out until a specific source’s license is confirmed.

## Correlated connections

Open sourcing is not only column fill — it enables joins:

- **Property ↔ pathway** — NIST/PubChem properties vs KEGG class  
- **Pathway ↔ bioactivity** — KEGG/MetaCyc vs ChEMBL/Open Targets  
- **Bioactivity ↔ clinical** — preclinical binding vs ClinicalTrials.gov  
- **Occurrence ↔ classification** — Dr. Duke’s vs ChEBI (e.g. linalool beyond cannabis-only claims)

## Suggested build order

1. **Compound registry seed** — PubChem bulk/API for named terpenes/terpenoids ([PUG REST](https://pubchem.ncbi.nlm.nih.gov/docs/pug-rest))  
2. **Classification tree** — ChEBI ontology for the same set  
3. **Pathway edges** — KEGG terpenoid maps  
4. **Bioactivity + targets** — ChEMBL / Open Targets / UniProt + PubMed citations  
5. **Clinical layer** (optional) — ClinicalTrials.gov, kept separate from preclinical  
6. **Cross-plant occurrence** — Dr. Duke’s  
7. **Regulatory** — FDA GRAS only where clean; IFRA marked gap  

Each phase follows README ETL layering: `/raw` → `/staging` → `/core`, with **per-record** license and citation — not a single bulk “source: PubChem” footnote.

## Explicit non-goals

- No previously staged scraped strain/spectra corpus until separate license review  
- No Postgres/DuckDB/Neo4j warehouse in this docs-only repo  
- No medical advice; clinical links are for evidence structure only  
