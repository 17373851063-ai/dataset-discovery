# Portal Catalog

Use this as a search checklist, not as a fixed truth table. Verify each candidate on its official record.

## High-Value BCI/EEG Data Portals

| Portal | Use For | Search Pattern | Access Pattern |
|---|---|---|---|
| OpenNeuro | BIDS EEG/MEG/iEEG datasets; general neuroimaging discovery | site:openneuro.org EEG "motor imagery"; OpenNeuro search filters | Usually public; DataLad/download; check dataset license |
| NEMAR | EEG/MEG/iEEG BIDS mirrors, compute-ready datasets | NEMAR search by motor imagery, BCI, hand, grasp | Usually public; zip for small datasets, CLI/git-annex for large |
| EEGDash | Metadata index over EEG datasets, often with HF/OpenNeuro/NeMAR links | EEGDash dataset pages and keywords | Index/mirror; follow source links for authoritative download |
| Figshare / Figshare+ | Scientific Data and institutional datasets; DOI records; file manifests | Figshare search/API with motor imagery EEG, robotic hand EEG, finger BCI | Usually direct public download; use API for file IDs, size, MD5 |
| KiltHub | CMU Figshare instance; robotic hand/finger BCI data | KiltHub search by DOI/title/authors | Direct public download unless record states otherwise |
| Zenodo | Open research archives and code/data releases | site:zenodo.org "motor imagery" EEG | Public download; API available; versioned DOI |
| GigaDB | GigaScience companion data such as Cho2017/OpenBMI | GigaDB dataset ID or paper DOI | Public download; may have many files |
| PhysioNet | Physiological signal datasets; classic EEGMMIDB | PhysioNet search by EEG motor imagery | Open Access or credentialed access depending dataset |
| GIN/G-Node | Neurophysiology data with git-annex, e.g. High-Gamma Dataset | GIN search or known repository URL | Public but large files may need git-annex/GIN tooling |
| OSF | Project repositories, competitions, upper-limb BCI data | site:osf.io EEG motor imagery grasp | Usually public; sometimes account/terms for bulk |
| Harvard Dataverse | Scientific Data companion archives | Dataverse DOI or paper data citation | Usually public; API supports file manifests |
| Dryad | Published data packages | site:datadryad.org EEG motor imagery | Usually public; check license and file links |
| CRCNS | Computational neuroscience datasets | CRCNS EEG BCI motor | Often account or application; verify per dataset |
| IEEE DataPort | Engineering datasets | IEEE DataPort EEG motor imagery | Often requires subscription or institutional access |

## Useful Query Templates

- "<seed dataset>" dataset download
- "<paper title>" "Data availability"
- "motor imagery" EEG "Figshare"
- "motor execution" EEG "upper limb" dataset
- "robotic hand" EEG BCI dataset
- "finger motor imagery" EEG dataset
- "grasping" "motor imagery" EEG dataset
- site:nature.com/articles "motor imagery" "Scientific Data" EEG
- site:figshare.com/articles/dataset "motor imagery" EEG
- site:openneuro.org/datasets EEG "motor"
- site:ww2.nemar.org/dataset "motor imagery"

