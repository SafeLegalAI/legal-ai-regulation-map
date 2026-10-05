---
license: cc-by-4.0
pretty_name: "SafeLegalAI Legal AI Regulation Map"
language:
  - en
multilinguality:
  - monolingual
annotations_creators:
  - expert-generated
language_creators:
  - found
source_datasets:
  - original
size_categories:
  - n<1K
tags:
  - legal
  - law
  - regulation
  - ai-governance
  - courts
  - bar-guidance
  - comparative-law
  - generative-ai
  - ai-regulation
  - ai-safety
  - safelegalai
configs:
  - config_name: countries
    default: true
    data_files:
      - split: train
        path: data/countries.jsonl
  - config_name: cells
    data_files:
      - split: train
        path: data/cells.jsonl
---

# SafeLegalAI Legal AI Regulation Map

**What do the rules on AI in legal practice say, country by country, across 20 categories?**

130 countries and entities · 102 with at least one rule · 20 categories · 3299 scored cells · last checked 2026-09-16 · synced from [safelegalai.com](https://safelegalai.com) on 2026-10-05.

Countries and supranational entities scored across 20 categories of rule on AI in legal practice — disclosure in filings, verification duty, judicial use, AI-decision prohibition, evidence admissibility, client confidentiality, bar guidance, sanctions record and more. Each cell carries a status (binding · guidance · proposed · case-law · none · unclear), a note naming the document, sources and its own last-checked date. Records marked `provisional` were AI-researched under the published taxonomy rules and await editor re-verification; they are labelled as such everywhere on the site.

This is a mirror. The canonical, always-current version lives at **[safelegalai.com/regulation](https://safelegalai.com/regulation)**, where every record has a permanent page, a citation block and its last-checked date; the JSON served there ([/regulation/map.json](https://safelegalai.com/regulation/map.json)) is the source of this repository. Each row's `url` field points to its record page. The same files are mirrored on GitHub at [github.com/SafeLegalAI/legal-ai-regulation-map](https://github.com/SafeLegalAI/legal-ai-regulation-map) (issues welcome there).

## Tables

| config | rows | what a row is | files |
|---|---|---|---|
| `countries` | 130 | one row per country or entity; `categories` and `subdivisions` are JSON strings (normalised in `cells`) | [`data/countries.jsonl`](data/countries.jsonl) · [`csv/countries.csv`](csv/countries.csv) |
| `cells` | 3299 | long format — one row per country × category (× subdivision) with its status, note, sources and check date | [`data/cells.jsonl`](data/cells.jsonl) · [`csv/cells.csv`](csv/cells.csv) |

## Fields

| field | meaning |
|---|---|
| `iso` · `name` · `region` · `legalSystem` | ISO 3166-1 alpha-2 (or EU / INT), region bucket, legal tradition |
| `summary` | 40–60 words on the overall posture, datestamped |
| `regulators` | `[{name, url, role}]` |
| `categories` | JSON string: map of the 20 taxonomy ids → `{status, note, documents[], sources[], lastVerified}`; use the `cells` config for one row per cell, or the fully nested JSON at the canonical `/regulation/map.json` |
| `subdivisions` | JSON string: sub-national units (US states, Canadian provinces, Australian states) with their own `categories`; also flattened into `cells` with `scope = subdivision` |
| `provisional` | true = AI-researched, not yet editor-verified source by source |
| `lastUpdated` · `lastVerified` | record dates |

Dates are `YYYY-MM-DD`. Optional fields are absent (JSONL) or empty (CSV) when unknown — nothing is guessed. In the CSV, arrays of scalars are joined with `; ` and nested objects are JSON strings.

## Method

We record findings made by courts and regulators; we do not make them. Every record links a primary source (judgment, order, regulator notice, official document or vendor page) and carries the date it was last re-opened against that source. Unverified records are flagged `unverified`, never silently included. Inclusion criteria, the correction process and the ownership/funding disclosure are published at [safelegalai.com/editorial-standards](https://safelegalai.com/editorial-standards); every content run is logged at [safelegalai.com/changelog](https://safelegalai.com/changelog).

## Use

```python
from datasets import load_dataset
ds = load_dataset("safelegalaidata/legal-ai-regulation-map", "countries")
```

## Uses

**Suited to:** counting and comparing what the record shows (by court, jurisdiction, date, actor, outcome, status); building watch-lists and alerts from the `url` and last-checked fields; grounding retrieval or summarisation on cited primary documents; teaching and library guides that need a dated, sourced list.

**Not suited to:** ranking products, people or courts; inferring prevalence beyond what a court or regulator has itself stated; any use that treats a coding column as a finding of fact or law. Where a row names a person or organisation it does so as they appear in a public document; anyone named may request a correction or right of reply at https://safelegalai.com/report.

## Cite

> SafeLegalAI (published by SafeLegalAI), "Legal AI Regulation Map", safelegalai.com, accessed 2026-10-05. https://safelegalai.com/regulation — data: CC BY 4.0.

```bibtex
@dataset{safelegalai_legal_ai_regulation_map_2026_10_05,
  title        = {Legal AI Regulation Map},
  author       = {{SafeLegalAI (SafeLegalAI)}},
  year         = {2026},
  url          = {https://safelegalai.com/regulation},
  note         = {Mirror: https://huggingface.co/datasets/safelegalaidata/legal-ai-regulation-map. Data CC BY 4.0. Last checked 2026-09-16.}
}
```

Cite the primary source as the authority and this dataset as the structured record that surfaced it. Corrections and right of reply: [safelegalai.com/report](https://safelegalai.com/report).

## Licence

[CC BY 4.0](https://creativecommons.org/licenses/by/4.0/). Attribution: **SafeLegalAI (safelegalai.com), published by SafeLegalAI** with a link to https://safelegalai.com/regulation. Primary sources keep their own licences and copyright.

## Disclaimer and notices

**Provided "as is", without warranty of any kind** — the CC BY 4.0 licence excludes all warranties and limits liability (section 5), and those exclusions apply to this dataset. **Not legal advice**; no lawyer–client relationship arises from using it. SafeLegalAI is not a law firm. SafeLegalAI records findings made by courts, regulators and vendors' own published pages; it makes no findings of its own, and the linked official documents are the record. Editorial classifications (status labels, requirement codes, "documented yes/no/not disclosed") are opinions about documents, expressed in good faith; the document prevails. Where a row names a person or organisation, it does so as they appear in a public court document, official publication or their own published material — a fair and accurate report published in good faith and in the public interest; anyone named may reply or request a correction at https://safelegalai.com/report. Product, company, court and regulator names and marks belong to their owners and identify the product or body referred to; no affiliation or endorsement is implied. Full terms and notice-and-takedown: https://safelegalai.com/disclaimer.

## Related datasets

- [Legal AI Incident Tracker](https://huggingface.co/datasets/safelegalaidata/legal-ai-incidents) — canonical page https://safelegalai.com/tracker
- [Legal AI Regulation Documents (versioned)](https://huggingface.co/datasets/safelegalaidata/legal-ai-regulation-documents) — canonical page https://safelegalai.com/regulation/documents
- [Legal Tech Tools — governance facts](https://huggingface.co/datasets/safelegalaidata/legal-ai-tools) — canonical page https://safelegalai.com/tools
- [All datasets and what is in preparation](https://safelegalai.com/datasets)
- [Taxonomy — the 20 categories and 6 status values](https://safelegalai.com/regulation#categories)

## Manifest

```json
{
  "dataset": "SafeLegalAI Legal AI Regulation Map",
  "canonical": "https://safelegalai.com/regulation",
  "source": "https://safelegalai.com/regulation/map.json",
  "catalogue": "https://safelegalai.com/datasets",
  "publisher": "SafeLegalAI",
  "license": "CC BY 4.0",
  "licenseUrl": "https://creativecommons.org/licenses/by/4.0/",
  "lastChecked": "2026-09-16",
  "synced": "2026-10-05",
  "notice": "Provided as is, without warranty; not legal advice. SafeLegalAI records findings made by courts, regulators and vendors' own pages; the linked official documents are the record. Names and marks belong to their owners. Terms: https://safelegalai.com/disclaimer",
  "tables": {
    "countries": 130,
    "cells": 3299
  },
  "contentSha256": "6470ee7b0424df265ef24949dc852369d7d40e34e48b3a23c175c00c2dbe83b6"
}
```
