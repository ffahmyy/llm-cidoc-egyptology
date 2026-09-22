# LLM-Supported Metadata Aggregation for Egyptology

CIDOC-CRM knowledge graph integrating First Dynasty Egyptian collections from
the Musée du Louvre and the British Museum, built through an LLM-assisted
extract–transform–load pipeline.

This repository accompanies the thesis "Collections as Data in Egyptology: Evaluating an LLM-Supported Metadata Aggregation Workflow" (UCL), [2026)
and contains the source data, the scripts produced at each stage of the
workflow, and the SPARQL queries used to evaluate the resulting graph.

## Contents

| Path | Contents |
|---|---|
| `data/raw/` | Source data as harvested, unmodified |
| `data/reconciliation/` | Entity reconciliation sheets, before and after merging |
| `data/enrichment/` | Chronological hierarchy CSV and the Turtle file generated from it |
| `scripts/` | Pipeline scripts, numbered in execution order |
| `queries/` | Competency question SPARQL queries and diagnostic queries |
| `docs/` | Schema mapping matrix and runbook |

## Pipeline

The workflow runs in seven stages. Each script corresponds to one stage and is
numbered accordingly.

1. **Harvesting** — source data downloaded from each museum's collections site
2. **Mapping and transformation** — source schemas mapped to CIDOC-CRM, each
   object written as an XML document
3. **Enrichment** — translation, entity reconciliation, chronological hierarchy
4. **Integration** — reconciliation sheets merged, URIs injected into both
   collections in a single pass
5. **Serialization** — XML converted to RDF/Turtle
6. **Validation** — SHACL validation against the application profile
7. **Loading and querying** — Turtle loaded into an Oxigraph triplestore and
   queried through SPARQL

See `docs/RUNBOOK.md` for the commands to reproduce each stage.

## Requirements

Python 3.11.1 or later. Install dependencies with:

```
pip install -r requirements.txt
```

## Data sources

Louvre object records were retrieved from collections.louvre.fr as JSON.
British Museum records were exported from britishmuseum.org/collection as CSV.
Both were retrieved in [MONTH YEAR]. Source data is included here under the
terms each institution publishes it; see `data/raw/README.md`.

## Vocabularies

| Class | Vocabulary |
|---|---|
| `crm:E4_Period` | Thesauri and Ontology for Ancient Egyptian Resources (THOT) |
| `crm:E57_Material`, `crm:E55_Type` | Getty Art & Architecture Thesaurus |
| `crm:E53_Place`, `crm:E39_Actor` | Wikidata, with local URIs where no match exists |
