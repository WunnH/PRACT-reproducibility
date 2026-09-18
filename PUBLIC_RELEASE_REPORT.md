# PRACT Public Release Report

## Status

`READY_FOR_MANUAL_REVIEW`

This directory contains only the minimal aggregate reproducibility information requested by the reviewer. No source code, patient-level row, patient identifier, image, mask, target coordinate, entry coordinate, or trajectory is included. Nothing was uploaded or pushed to a remote service.

## Files

- `README.md`
- `imaging_parameters.csv`
- `method_parameters.md`
- `candidate_runtime_summary.csv`
- `PUBLIC_RELEASE_REPORT.md`

## Reviewer-requested information

| Requirement | Status | Result |
|---|---|---|
| Sequence voxel size and acquisition parameters | Completed | T1WI/T2WI/SWI protocol variants are reported from DICOM-derived JSON metadata and NIfTI headers |
| Spatial mapping | Completed | T1WI planning-space reference; existing NIfTI affine/header geometry; linear interpolation for intensities and nearest-neighbour interpolation for masks |
| Registration accuracy | Completed as unavailable | Registration accuracy was not independently quantified in the present cohort |
| Perturbation count and millimetre magnitude | Completed | 13 uncertainty evaluation scenarios for cases with all three risk structures available, comprising 1 nominal and 12 perturbed scenarios |
| Candidate trajectory generation | Completed | Target-to-cortical-surface sampling with sagittal, axial, and coronal-suture-based anatomical constraints |
| Candidate-set sizes and runtime | Completed | Candidate-stage and optimization-runtime statistics use all 30 hemispheres; preprocessing runtime uses 15 case records |

## Source audit

The release values were checked against the manuscript method specification, DICOM-derived JSON sidecars, NIfTI QC inventory, preprocessing summaries, saved optimizer summaries, and the final 30-hemisphere aggregate record. Patient-level sources were read locally only and were not copied into this directory.

The public summary uses the following manuscript-aligned method definitions and aggregate records:

- The 15-case SWI analysis comprised 30 hemisphere records.
- All 15 SWI-cohort planning grids used 1.0000 × 0.9375 × 0.9375 mm spacing.
- The perturbation procedure applied erosion and dilation to the sulcal and ventricular masks, one-voxel boundary broadening to the vascular risk regions, simultaneous dilation of all available risk structures, and six target shifts.
- Candidate trajectories were generated between predefined STN targets and cortical entry candidates under the stated angular and entry-zone constraints.
- Mapping used T1WI as reference, header/affine-based resampling for intensities, and nearest-neighbour resampling for masks.

## Aggregate 30-hemisphere record

| Item | Result |
|---|---:|
| Nominal-feasible candidates | 8,131 |
| Robust-feasible candidates | 5,940 |
| Candidates rejected by robust screening | 2,191 (26.9%) |
| Hemispheres with a robust solution at baseline T3 | 30/30 |
| Optimization runtime | 1.033 ± 0.074 s per hemisphere |
| Total preprocessing runtime | 159.676 ± 14.246 s per case |

## TODO_VERIFY and unavailable items

1. Candidate-generation-only runtime was not separately recorded.
2. Registration accuracy was not independently quantified; affine agreement and visual/QC labels are not reported as millimetre registration error.
3. The source QC inventory records two SWI volumes with a 256×256×9 matrix. This value is reported without alteration and should be checked against the original acquisition archive before manuscript submission.

## Privacy and release assessment

The final directory contains exactly five aggregate documentation files. A recursive scan found no patient naming pattern, local absolute path, credential, image, NIfTI file, JSON sidecar, source-code file, or case-level record.

`READY_FOR_MANUAL_REVIEW`

