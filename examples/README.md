# Examples

## Topic Search

User request:

Find datasets for EEG motor imagery, motor execution, and robotic hand control. Prefer public downloadable datasets. Include application-required datasets separately.

Expected agent flow:

1. Read local memory and prior registries.
2. Search general engines: Google Dataset Search, DataCite, OpenAIRE, re3data.
3. Search domain repositories: OpenNeuro, NEMAR, EEGDash, PhysioNet, DANDI, CRCNS, GIN/G-Node.
4. Search data hosts: Figshare, Zenodo, OSF, Dataverse, Dryad, GigaDB, Mendeley Data, Synapse.
5. Output candidate table with brief descriptions, access class, relevance score, and evidence links.
6. Wait for keep/delete/maybe/merge review.
7. For approved candidates, use the top-cited five relevant papers and official data pages to extract dimensions such as subjects, task type, labels, trial length, sessions, channels, sampling rate, file format, license, and download method.
8. Deduplicate mirrors and propose visualizations such as task type vs participant count, access status distribution, citation vs relevance scatter, and dataset relationship graph.

