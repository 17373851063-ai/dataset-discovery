---
name: bci-dataset-discovery
description: Discover, screen, and summarize BCI/neural datasets from dataset portals and literature. Use when Codex is asked to find datasets by topic, seed portals, or reference datasets, especially EEG/BCI motor imagery, motor execution, upper-limb, grasping, robotic hand, dexterous hand, neuroprosthetic, or rehabilitation-control datasets; classify public-download versus registration/application/restricted access; rank task relevance; and produce staged tables for human screening and later detailed dataset-dimension extraction.
---

# BCI Dataset Discovery

## Core Rule

Use a staged, provenance-first workflow:

1. Find candidate portals and dataset records.
2. Screen by task topic and relevance.
3. Audit access and download requirements.
4. Output a compact candidate table for human selection.
5. Only after the user approves candidates, extract detailed dataset dimensions from the dataset page and reference paper.
6. After the user reviews additions/deletions/changes, output the final table.

Do not jump straight to a final dimension table unless the user explicitly asks to skip review gates.

## Evidence Order

Prefer sources in this order:

1. Official dataset page or repository metadata.
2. Platform API or file manifest.
3. Paper Data Availability / Data Records section.
4. Official benchmark adapter docs such as MOABB, NEMAR, EEGDash.
5. Secondary lists only as search hints.

Mark important claims with evidence tags: [Data], [Paper], [Repo], [Index], [Inference], [Assumption], [Unknown].

## Workflow

### 1. Scope Intake

Extract from the user:

- Topic terms: e.g. motor imagery, motor execution, grasping, hand opening/closing, individual fingers, robotic hand control.
- Seed portals: e.g. OpenNeuro, Figshare, NEMAR, PhysioNet, Zenodo.
- Seed datasets: e.g. WBCIC-SHU, Ding robotic hand, EEGMMIDB.
- Inclusion constraints: modality, public only, patient/healthy, format, size, language, download region.
- Exclusion constraints: non-EEG, non-human, invasive-only, non-downloadable, synthetic-only.

If scope is ambiguous, make a conservative search and state assumptions.

### 2. Portal Sweep

Read references/portal-catalog.md before broad portal discovery or when choosing where to search.

Search both platform names and task terms. Use platform-native pages/APIs when available. Keep a portal table with:

portal, why_relevant, search_terms, access_pattern, download_pattern, notes.

Do not treat a portal as proof that a dataset matches the task; portal hits are only candidates.

### 3. Candidate Screening

For each candidate, capture only enough information for screening:

- dataset name and URL
- source portal
- DOI or paper
- modality and paradigm
- task labels/effectors
- rough subject/session scale
- robot/online feedback/control relevance
- access status
- relevance score

Score task relevance on 0-5:

- 5: exact match, e.g. EEG MI/ME plus real robotic hand/finger/dexterous control.
- 4: upper-limb or grasping MI/ME, good proxy for robotic hand control.
- 3: generic left/right hand MI or ME, useful baseline/pretraining.
- 2: adjacent BCI/neurofeedback/multimodal motor task.
- 1: weakly related EEG but not motor control.
- 0: out of scope.

### 4. Access Audit

Classify access as one of:

- public_direct: direct browser/API/wget/download button works, no account noted.
- public_cli: public but best retrieved through DataLad, git-annex, platform CLI, S3, or API.
- public_registration: public but requires login, terms checkbox, or platform account.
- application_required: explicit request form, data use agreement, institutional approval, or credentialed access.
- restricted: closed, private, embargoed, or no downloadable files.
- unknown: evidence insufficient.

Record whether the page mentions password/encryption, license, file size, file count, checksum, and resumable download support. If files are large, prefer manifest/API checks before downloading.

### 5. First Output: Human Screening Table

Use references/table-schemas.md for columns. Keep this table compact. Include enough evidence links for the user to accept/reject candidates.

End with a clear review request such as: "Please mark keep, delete, add, rename, or maybe; after approval I will extract core dimensions."

### 6. Approved Candidate Dimension Extraction

After the user approves candidates, extract detailed dimensions from the official data page and paper:

- subjects and demographics
- health condition
- modality and channels
- montage/reference/ground
- sampling rate
- task paradigm and labels
- trial/session/run design
- event markers and timing
- online feedback/robot/control details
- raw/preprocessed availability
- format and file organization
- license/access/download method
- dataset size/checksums if available
- known caveats, inconsistencies, or unknowns

Separate facts from assumptions. If a field is absent from official sources, write unknown, not a guess.

### 7. Final Review and CRUD

After producing the detailed table, support user-directed add/delete/change operations:

- Add a candidate and fill missing dimensions.
- Delete irrelevant candidates.
- Rename or merge duplicate dataset records.
- Update access status after testing download/API.
- Add columns requested by the user.

Only call the result final after the user's review pass is handled or the user explicitly says no review is needed.

## Output Discipline

- Prefer tables over long prose.
- Keep citations or source links next to the claim they support.
- Distinguish dataset host from paper host.
- Flag stale or secondary-source-only results.
- For domestic server downloads, include download method notes but do not start large downloads without confirmation.
- For human-subject data, respect license and do not recommend unofficial redistribution.

