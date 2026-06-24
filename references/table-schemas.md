# Table Schemas

## Candidate Screening Table

Use before human selection.

| Column | Meaning |
|---|---|
| rank | Relevance order or priority |
| dataset_name | Official dataset name |
| portal | Dataset host or index |
| primary_url | Official dataset URL |
| paper_or_doi | Paper DOI or data DOI |
| modality | EEG, MEG, ECoG, fNIRS, multimodal |
| task_match | MI, ME, upper limb, grasp, finger, robotic control |
| brief_description | 1-2 sentence summary |
| access_status | public_direct, public_cli, public_registration, application_required, restricted, unknown |
| download_notes | Size, file count, API/CLI, checksum, password notes |
| license | License if visible |
| relevance_score | 0-5 score |
| evidence | [Data], [Paper], [Repo], [Index] links or notes |
| keep_for_review | yes/no/maybe |

## Detailed Dataset Dimension Table

Use only after human screening approval unless the user asks to skip review.

| Column | Meaning |
|---|---|
| dataset_name | Official name |
| canonical_url | Official data page |
| paper_reference | Paper title/DOI |
| evidence_grade | Paper/Data/Repo/Index mix |
| modality | EEG/MEG/ECoG/fNIRS/etc. |
| participants | N, demographics, health condition |
| paradigm | MI, ME, online BCI, feedback, robot control |
| effectors_labels | left/right hand, feet, tongue, hand open/close, fingers, grasp types |
| sessions_runs_trials | session/run/trial counts and split units |
| timing | cue/rest/task windows and epoch interval |
| channels | count, names if important, auxiliary channels |
| montage_reference | montage, reference, ground |
| sampling_rate | Hz and any downsampling |
| hardware | amplifier/cap/sensor |
| raw_preprocessed | raw data, processed data, trial tensors |
| event_annotations | marker names/codes/timestamps |
| file_format | EDF/BDF/MAT/CSV/BIDS/etc. |
| file_organization | subject/session/run path layout |
| size_files_checksums | total size, file count, MD5/SHA if available |
| access_license | access class and license |
| download_method | wget/API/CLI/DataLad/git-annex/S3/browser |
| robot_control | robotic hand/arm/device, online prediction fields, control rate |
| caveats | contradictions, missing fields, limitations |
| decision | keep/delete/merge/defer |

