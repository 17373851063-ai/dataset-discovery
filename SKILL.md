---
name: dataset-research
description: Research, discover, screen, and maintain datasets for a user-specified topic using a four-layer discovery network. Use when Codex is asked to find datasets from public websites, dataset collections, or research papers; search general dataset engines, domain-specific repositories, and scientific data hosts; prioritize local memory before web search; audit public-download versus registration/application/restricted access; rank relevance; use the top-cited relevant papers to extract dataset dimensions such as subjects, tasks, trials, channels, sampling rate, labels, file formats, and access; deduplicate and maintain tables; and propose or generate approved visualization charts.
---

# Dataset Research

## Core Rule

Run dataset research as a staged, review-gated workflow:

1. Read local memory and previous dataset registries before searching.
2. Search a four-layer discovery network.
3. Produce a candidate dataset table with brief descriptions.
4. Audit public availability and access requirements.
5. Rank relevance and identify the top-cited relevant papers.
6. Extract core dataset dimensions only for approved or high-priority candidates.
7. Deduplicate, apply user add/delete/update decisions, and maintain a clean table.
8. Propose visualizations; generate charts only after the user approves the chart plan.

Do not skip the human review gates unless the user explicitly asks for a one-pass final table.

## Memory-First Behavior

Before web search, inspect available local memory or project artifacts:

- Codex memory surfaced in context.
- Existing project files such as state/dataset_registry.csv, state/dataset_memory.*, docs/resource_audit.*, or prior candidate tables.
- Skill references in references/portal-catalog.md and references/table-schemas.md.

After each search pass, record new reusable knowledge when a memory mechanism is available. If direct memory writing is not available, include a short "memory_update" block in the response or update the project dataset registry if the user asked for persistent files.

Record only stable facts in memory: useful portals, exact dataset names, canonical URLs, DOI, access class, and caveats. Do not store unsupported guesses.

## Four-Layer Discovery Network

Read references/portal-catalog.md before broad searches.

### Layer 1: General Dataset Search

Use broad dataset search engines to map the search space:

- Google Dataset Search
- DataCite Commons
- OpenAIRE Explore
- re3data for repository discovery
- OpenAlex, Semantic Scholar, or Crossref for paper/data links when available

Goal: find candidate dataset names, DOI records, host repositories, and high-citation papers.

### Layer 2: Domain-Specific Data Repositories

Search repositories specific to the topic. For EEG/BCI/neural data, prioritize:

- OpenNeuro
- NEMAR
- EEGDash
- PhysioNet
- DANDI
- CRCNS
- GIN/G-Node
- MOABB and BNCI when they have not already been searched by the user

For other domains, infer the appropriate specialist repositories and add them to the search log.

### Layer 3: Scientific Data Hosting Sites

Search general scientific data hosts and institutional repositories:

- Figshare, Figshare+, and institutional Figshare instances such as KiltHub
- Zenodo
- OSF
- Harvard Dataverse and other Dataverse instances
- Dryad
- GigaDB
- Mendeley Data
- Synapse
- Hugging Face Datasets and Kaggle only as secondary or mirror leads unless they are the official host

Goal: verify actual files, licenses, size, download methods, versions, and checksums when available.

### Layer 4: Literature and Citation Validation

For the filtered candidate set, find the most relevant and highest-cited papers. Prefer official paper pages, Crossref/OpenAlex/Semantic Scholar, publisher pages, or dataset citations.

Use the top five relevant high-citation papers to extract core data dimensions. If citation counts are unavailable or inconsistent, rank by topic relevance, official data availability, publication venue, and reuse evidence, then mark the ranking basis.

## Screening and Review Gates

### Candidate Table Gate

Before deep extraction, output a compact candidate table with dataset name, URL, source portal, topic match, brief description, access class, relevance score, citation/paper signal, and keep/delete/maybe.

Ask the user to approve, delete, merge, rename, or add candidates.

### Access Audit Gate

Classify access as:

- public_direct: direct download/API/wget/browser download, no account noted.
- public_cli: public but best via DataLad, git-annex, platform CLI, S3, or API.
- public_registration: public but requires login, terms checkbox, or platform account.
- application_required: explicit application, data use agreement, credentialing, IRB/institutional approval, or manual access request.
- restricted: closed, private, embargoed, or no files.
- unknown: insufficient evidence.

Do not label a dataset as public just because a paper exists; verify the dataset host.

### Dimension Extraction Gate

After approval, extract core dimensions from official data pages and reference papers. Use unknown for missing fields. Separate evidence from inference.

Core dimensions include subjects, demographics, modality, task type, labels, session/run/trial design, trial length, event timing, channels, sampling rate, hardware, file format, raw/preprocessed availability, access/license, and download method.

### Deduplication and Table Maintenance Gate

Deduplicate by DOI, canonical dataset URL, title variants, authors, repository IDs, and file manifests. Merge duplicates instead of listing the same dataset from OpenNeuro/NEMAR/EEGDash/Figshare multiple times unless mirrors differ materially.

Support CRUD operations:

- Add missing datasets.
- Delete out-of-scope entries.
- Update dimensions or access class.
- Merge duplicates.
- Split entries when one paper contains multiple distinct datasets.

## Visualization Planning

After the maintained table passes user review, propose visualizations before generating them.

Good default charts:

- Task type vs participant count: bar chart or pie chart.
- Access status distribution: donut or stacked bar.
- Modality by task type: heatmap.
- Dataset source portal by relevance score: bar chart.
- Citation count vs relevance score: scatter plot.
- Participant count vs trial count: bubble chart.
- Dataset-year timeline: timeline or line chart.
- Dataset relationship graph: nodes for papers, repositories, datasets, mirrors, and task types.

Generate visualizations only after the user approves the chart list and data fields.

## Output Discipline

- Prefer structured tables over prose.
- Keep source links close to claims.
- Mark evidence with [Data], [Paper], [Repo], [Index], [Inference], [Assumption], or [Unknown].
- Distinguish primary dataset hosts from mirrors and indexes.
- For large downloads, stop at manifest/API validation unless the user confirms downloading.
- For human-subject datasets, preserve license and access constraints; do not suggest unofficial redistribution.

