# CMIP — Cannabis Molecular Intelligence Platform

**Status:** schema and architecture notes. **No code and no lab data** live
in this repo yet.

## Why this exists

Most “terpene databases” are giant spreadsheets: the same molecule appears
under five spellings, boiling points show up as bare numbers with no source,
and aroma wheels get mixed into chemistry columns. CMIP is a design for doing
that job properly — one place for compounds, cultivars, lab COAs, and the
links between them — so charts and tools can share a single backbone.

## Design principles (in plain language)

- **One row per real chemical.** Everything else points at it; do not paste
  the same molecule into ten tables.
- **Numbers need a story.** A boiling point is not just `177` — units, method,
  citation, and confidence travel with the value.
- **Isomers stay distinct.** α-pinene is not β-pinene; cis/trans matter for
  pathways and effects.
- **Pretty wheels are not chemistry.** Aroma/flavor/effect taxonomies sit
  beside the science, not inside the compound record.

## Layered architecture

```
Knowledge Layer (literature/patents)
  → Reference Tables
  → Chemistry
  → Cultivars
  → Lab Results (Certificates of Analysis)
  → Retail Products
  → Genetics
  → Visualization
```

## Core schema modules

- **Compounds** — the master registry
- **Synonyms**
- **Classification** — a real ontology (Organic Compound → Terpenoid →
  Monoterpenoid → Alcohol → [specific compound]), not flat categories
- **Functional Chemistry / Properties**
- **Biological Activity** — structured as
  `compound / target / effect / species / model / dose / citation /
  confidence`, never a bare label like "anti-anxiety"
- **Protein Targets**
- **Pathways** — the biosynthetic graph (isomer-distinct, per above)
- **Measurements**
- **Cultivars**
- **Genetics** — parent/child graph
- **Lab Results** (COAs)
- **Products**
- **Labs / Instruments**
- **References**
- **Visualization layer** — kept separate, as above

## Storage recommendation (polyglot, not a single database)

```
raw ingestion (versioned XML/JSON/CSV)
  → DuckDB + Parquet analytics warehouse
  → PostgreSQL canonical relational store
  → Neo4j/Memgraph for genetics & pathway graph queries
  → full-text + vector search (Postgres FTS+pgvector, or OpenSearch)
  → JSON/Parquet visualization-cache exports
```

## ETL as an immutable staged pipeline

```
/raw      unchanged sources
/staging  parsed, normalized, validated
/core     compounds, cultivars, measurements, references
/marts    derived exports — terpene_wheel.csv, cannabinoid_summary.csv,
          cultivar_profiles.parquet, aroma_network.json
```

## Example schema: master compound registry

A representative field list (not a full DDL):

```
compound_id, canonical_name, display_name, compound_group, compound_class,
subclass, isomer, synonyms, iupac_name, cas, pubchem_cid, chemspider, chebi,
inchi, inchikey, smiles, formula, molecular_weight, exact_mass,
boiling_point_c, melting_point_c, density, logP, tpsa, water_solubility,
ethanol_solubility, biosynthetic_pathway, precursor, enzyme, plant_part,
occurrence_cannabis, relative_abundance, coa_panel, aroma_primary,
aroma_secondary, flavor_primary, odor_descriptors, reported_effects,
receptor_targets, evidence_level, fda_gras, ifra, toxicity_notes,
color_group, wheel_order, hex_color, notes, source_refs
```

## Example schema: terpene-specific table

```
canonical_name, display_name, aliases, parent_class, isomer, aroma_family,
flavor_notes, common_in_cannabis, relative_abundance, reported_effects,
evidence_strength, fda_gras, boiling_point_c, molecular_formula,
pubchem_cid, color_group, wheel_order, notes
```

## What's deliberately not in this repo

No real compound, strain, or spectral data ships here — schema and
architecture only. If you build a real instance of this design, you'll
need to source your own licensed chemistry/strain data; be mindful of
scraping and redistribution terms for any commercial or scraped source
before republishing it anywhere.

## License

MIT — see `LICENSE`.

## Non-affiliation

This is an independent architecture sketch, not affiliated with,
endorsed by, or sponsored by any lab, vendor, or database referenced
generically above.
