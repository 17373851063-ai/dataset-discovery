# Dataset Research Skill

Codex skill for staged dataset discovery and screening.

## Workflow

1. Read local memory and prior dataset registries.
2. Search Layer 1 general dataset engines, such as Google Dataset Search, DataCite Commons, OpenAIRE, and re3data.
3. Search Layer 2 domain repositories, such as OpenNeuro, NEMAR, EEGDash, PhysioNet, DANDI, CRCNS, GIN/G-Node, MOABB, or BNCI when relevant.
4. Search Layer 3 scientific data hosts, such as Figshare, Zenodo, OSF, Dataverse, Dryad, GigaDB, Mendeley Data, Synapse, Hugging Face Datasets, and Kaggle.
5. Use Layer 4 literature and citation validation to identify high-value papers and extract core dataset dimensions.
6. Audit access status: public direct, public CLI, public registration, application required, restricted, or unknown.
7. Produce a candidate table for human review.
8. After approval, extract detailed dimensions, deduplicate records, maintain the table, and propose visualizations.

## Review Gates

- Candidate table before deep extraction.
- Access audit before download planning.
- Detailed dimension table before deduplication finalization.
- Visualization plan before chart generation.

## Example Prompt

Use $dataset-research to find public datasets for motor imagery and motor execution robotic hand control, audit whether each dataset is downloadable or requires application, extract dimensions from the top-cited five relevant papers, deduplicate mirrors, and propose visualizations.

