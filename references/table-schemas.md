# Table Schemas

## Search Log

Use this to make the search reproducible and memory-friendly.

| Column | Meaning |
|---|---|
| layer | 1 general, 2 domain, 3 host, 4 literature |
| source | Search engine, repository, host, or paper index |
| query | Exact query or API endpoint |
| result_count | Number of plausible hits |
| new_portals | New reusable portals found |
| new_candidates | New dataset names found |
| action | keep searching, verify, reject, add to memory |
| memory_update | Stable facts to persist |

## Candidate Screening Table

Use before human selection.

| Column | Meaning |
|---|---|
| rank | Relevance order or priority |
| dataset_name | Official dataset name |
| primary_url | Official dataset URL |
| host_or_index | Dataset host, mirror, or index |
| paper_or_doi | Paper DOI or data DOI |
| modality | EEG, MEG, ECoG, fNIRS, images, text, tabular, etc. |
| topic_match | How it matches the user topic |
| brief_description | 1-2 sentence summary |
| access_status | public_direct, public_cli, public_registration, application_required, restricted, unknown |
| download_notes | Size, file count, API/CLI, checksum, password notes |
| citation_signal | Citation count or ranking basis |
| relevance_score | 0-5 score |
| evidence | [Data], [Paper], [Repo], [Index] links or notes |
| review_decision | keep/delete/maybe/merge/rename |

## Access Audit Table

| Column | Meaning |
|---|---|
| dataset_name | Candidate name |
| access_status | Controlled vocabulary from SKILL.md |
| evidence_url | Dataset page or policy page |
| requires_login | yes/no/unknown |
| requires_application | yes/no/unknown |
| license | License if visible |
| file_visibility | files listed/downloadable/hidden/unknown |
| download_method | browser/API/wget/CLI/DataLad/git-annex/S3/request |
| file_size | Total size if known |
| checksum | MD5/SHA if available |
| password_or_encryption | no/yes/unknown |
| notes | Caveats |

## Top-Cited Paper Table

| Column | Meaning |
|---|---|
| rank | Citation/relevance rank |
| paper_title | Paper title |
| citation_count | Count and source, or unknown |
| source | Google Scholar/OpenAlex/Semantic Scholar/Crossref/publisher |
| dataset_name | Linked dataset |
| paper_url | Paper URL or DOI |
| data_url | Dataset URL |
| why_relevant | Why this paper supports dimension extraction |
| evidence | [Paper], [Index], [Data] |

## Detailed Dataset Dimension Table

Use only after candidate approval or explicit user instruction.

| Column | Meaning |
|---|---|
| dataset_name | Official name |
| canonical_url | Official data page |
| mirrors_or_indexes | OpenNeuro/NEMAR/EEGDash/HF/etc. mirrors |
| paper_reference | Paper title/DOI |
| evidence_grade | Paper/Data/Repo/Index mix |
| participants | N, demographics, health condition |
| modality | EEG/MEG/ECoG/fNIRS/etc. |
| task_type | MI, ME, online control, classification, regression, etc. |
| task_labels | Class labels/effectors/actions |
| sessions_runs_trials | Session/run/trial counts and split units |
| trial_length_timing | Trial length, cue/rest/task windows, epoch interval |
| channels | Channel count/names/auxiliary channels |
| montage_reference | Montage, reference, ground |
| sampling_rate | Hz and downsampling |
| hardware | Amplifier, cap, sensor |
| raw_preprocessed | Raw data, processed data, trial tensors |
| event_annotations | Marker names/codes/timestamps |
| file_format | EDF/BDF/MAT/CSV/NWB/BIDS/etc. |
| file_organization | Subject/session/run path layout |
| size_files_checksums | Total size, file count, hashes |
| access_license | Access class and license |
| download_method | wget/API/CLI/DataLad/git-annex/S3/browser/request |
| task_relevance | 0-5 plus short reason |
| caveats | Contradictions, missing fields, limitations |
| decision | keep/delete/merge/defer |

## Deduplication Registry

| Column | Meaning |
|---|---|
| canonical_dataset_id | Preferred stable ID, DOI if available |
| canonical_name | Preferred official name |
| duplicate_names | Alternate names |
| duplicate_urls | Mirrors and indexes |
| merge_reason | DOI match, file manifest match, paper match, title/author match |
| retained_record | URL/name kept in final table |
| notes | Important differences among mirrors |

## Visualization Plan Table

| Column | Meaning |
|---|---|
| chart_id | Stable ID |
| chart_type | Pie, bar, heatmap, scatter, bubble, timeline, network |
| question_answered | What decision the chart supports |
| data_fields | Required table columns |
| aggregation | Count, sum participants, mean trials, etc. |
| caveats | Missing data or bias |
| approved | yes/no/pending |

