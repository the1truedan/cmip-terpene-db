# CMIP — Cannabis Molecular Intelligence Platform (schema + architecture)

**Status:** early architecture sketch. Schema and design documentation
only — **no code and no data ship in this repo.**

## What this is

A normalized, provenance-aware schema design for cannabis/hemp chemistry
and cultivar data — compounds, terpenes, cultivars, lab results, and the
relationships between them — intended to replace flat "terpene database"
spreadsheets with a proper relational/graph model that can power
visualization, cheminformatics, and analytics from one underlying source
of truth.

## Design principles

- **Never duplicate chemistry.** A compound exists exactly once (a
  `Compound` table keyed by `compound_uuid`); everything else (cultivar
  measurements, lab results, retail products) references it rather than
  re-storing values.
- **Every value carries provenance.** Never store a bare number like
  `177` for a boiling point — store
  `{value, units, method, reference, confidence, version}`.
- **Isomers are never merged.** α-pinene and β-pinene, cis- and
  trans-ocimene, stay distinct compounds — the biosynthetic/pathway graph
  needs that granularity to mean anything.
- **Visualization stays separate from chemistry.** Aroma/flavor/effect
  wheels are their own weighted taxonomies, not mixed into the compound
  record itself.

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
