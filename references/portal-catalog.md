# Portal Catalog

Use this as a search checklist. Verify each candidate on its official record and update memory or the project registry with reusable findings.

## Layer 1: General Dataset Search

| Portal | Use For | Query Pattern | Notes |
|---|---|---|---|
| Google Dataset Search | Topic-to-dataset discovery across many indexed repositories | topic + dataset, quoted task terms, site filters | Best first pass for unknown domains |
| DataCite Commons | DOI-based dataset and publication discovery | dataset title, author, DOI, keyword | Good for Figshare, Zenodo, Dataverse, Dryad DOI records |
| OpenAIRE Explore | Linked publications, datasets, software, organizations, grants | topic + research data filter | Useful for Europe-linked records and paper-data links |
| re3data | Repository discovery, not individual datasets | topic + repository, subject browse | Use to find domain repositories to add to Layer 2 |
| OpenAlex / Semantic Scholar / Crossref | Paper discovery and citation signals | topic + dataset/paper title | Use for top-cited paper selection and DOI verification |

## Layer 2: Domain-Specific Repositories

For EEG/BCI/neural topics:

| Portal | Use For | Access Pattern |
|---|---|---|
| OpenNeuro | BIDS MRI/MEG/EEG/iEEG/NIRS datasets | Public download/DataLad; check dataset license |
| NEMAR | Human EEG/MEG/iEEG/EMG BIDS mirrors and quality reports | Public zip/CLI/git-annex; follow source links |
| EEGDash | EEG metadata index and mirrors | Index/mirror; confirm authoritative host |
| PhysioNet | Physiological signal datasets, including EEGMMIDB | Open Access or credentialed access per dataset |
| DANDI | Neurophysiology and behavioral time-series, NWB | Public archive, DANDI CLI/API often useful |
| CRCNS | Computational neuroscience datasets | Often requires account or application; verify per dataset |
| GIN/G-Node | Neurophysiology repositories, git-annex data | Public but large files often need GIN/git-annex |
| MOABB | BCI benchmark adapters and metadata | Good index; confirm original host for download/licensing |
| BNCI Horizon / BCI Competition | Classic BCI competition datasets | Often public with terms/license; verify dataset page |

For other domains, add specialist repositories to the search log and memory when discovered.

## Layer 3: Scientific Data Hosts

| Host | Use For | Access Pattern |
|---|---|---|
| Figshare / Figshare+ | Data DOI records, Scientific Data datasets, file manifests | Direct download/API; check license, versions, MD5 |
| Institutional Figshare, e.g. KiltHub | University-hosted Figshare records | Same as Figshare; may use institutional branding |
| Zenodo | Versioned research data/code/model releases | Public download/API; DOI versions |
| OSF | Project repositories and competition data | Public or account/terms depending project |
| Harvard Dataverse and Dataverse nodes | Published datasets, file-level metadata | Public/API; may require terms acceptance |
| Dryad | Publication-linked data packages | Usually public; check license |
| GigaDB | GigaScience companion data | Public files; often many separate downloads |
| Mendeley Data | Publication-linked datasets | Usually public; check license |
| Synapse | Biomedical consortia datasets | Public, login, or controlled access depending project |
| Hugging Face Datasets | ML-ready mirrors or processed datasets | Treat as secondary unless official; verify provenance |
| Kaggle | Convenient mirrors and community datasets | Treat as secondary unless official; verify provenance |

## Query Templates

- "<topic>" dataset
- "<topic>" "Data availability"
- "<topic>" "Scientific Data"
- "<topic>" "Figshare"
- "<topic>" "Zenodo"
- "<topic>" "OpenNeuro"
- "<topic>" "NEMAR"
- "<paper title>" dataset DOI
- "<seed dataset>" similar dataset
- "<task label>" "<modality>" dataset
- site:nature.com/articles "<topic>" "Data Descriptor"
- site:figshare.com/articles/dataset "<topic>"
- site:zenodo.org "<topic>" dataset
- site:openneuro.org/datasets "<topic>"
- site:ww2.nemar.org/dataset "<topic>"

