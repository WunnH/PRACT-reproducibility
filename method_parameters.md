# PRACT Reproducibility Parameters

## Imaging and voxel size

Acquisition metadata and NIfTI grid dimensions are provided in `imaging_parameters.csv`. The cohort contained 20 T1WI and T2WI series and 15 available SWI series. The 15-case SWI planning cohort used a T1WI planning-grid spacing of 1.0000 × 0.9375 × 0.9375 mm in all recorded cases.

## Spatial mapping

PRACT used the patient-specific T1WI planning space as the unified anatomical reference. T2WI-derived STN and red-nucleus masks were mapped to the T1WI planning space, and SWI was mapped to the same planning grid when available.

Spatial mapping used the existing NIfTI affine/header geometry. Intensity images were resampled using linear interpolation, whereas binary masks were resampled using nearest-neighbour interpolation.

Registration accuracy was not independently quantified in the present cohort.

## Perturbation scenarios

For cases with all three risk structures available, the uncertainty set comprised 13 scenarios, including one nominal scenario and 12 perturbed scenarios. Morphological operations used a one-voxel magnitude. Physical morphology scale is axis-dependent because one grid voxel corresponds to 1.0000 mm on voxel axis 0 and 0.9375 mm on axes 1 and 2.

| Scenario | Operation | Voxel magnitude | Physical magnitude (mm) |
|---|---|---:|---|
| nominal | Unperturbed masks and target | 0 | 0 |
| vessel_dilate_1voxel | Vessel boundary broadening | 1 voxel | Axis-dependent: 1.0000 or 0.9375 |
| sulcus_erode_1voxel | Sulcus-mask erosion | 1 voxel | Axis-dependent: 1.0000 or 0.9375 |
| sulcus_dilate_1voxel | Sulcus-mask dilation | 1 voxel | Axis-dependent: 1.0000 or 0.9375 |
| ventricle_erode_1voxel | Ventricle-mask erosion | 1 voxel | Axis-dependent: 1.0000 or 0.9375 |
| ventricle_dilate_1voxel | Ventricle-mask dilation | 1 voxel | Axis-dependent: 1.0000 or 0.9375 |
| combined_conservative_mask_dilation | Simultaneous dilation of all available risk structures | 1 voxel per mask | Axis-dependent |
| target_shift_x_plus_1voxel | Target shift along +voxel axis 0 | 1 voxel | 1.0000 |
| target_shift_x_minus_1voxel | Target shift along −voxel axis 0 | 1 voxel | 1.0000 |
| target_shift_y_plus_1voxel | Target shift along +voxel axis 1 | 1 voxel | 0.9375 |
| target_shift_y_minus_1voxel | Target shift along −voxel axis 1 | 1 voxel | 0.9375 |
| target_shift_z_plus_1voxel | Target shift along +voxel axis 2 | 1 voxel | 0.9375 |
| target_shift_z_minus_1voxel | Target shift along −voxel axis 2 | 1 voxel | 0.9375 |

**For cases with all three risk structures available, the uncertainty set comprised 13 scenarios, including one nominal scenario and 12 perturbed scenarios.**

The perturbation configuration included erosion and dilation of the sulcal and ventricular masks, one-voxel boundary broadening of the vascular risk regions, simultaneous dilation of all available risk structures, and six target-position shifts.

## Candidate trajectory generation

For each predefined STN target, candidate directions were sampled outward toward the cortical surface in the patient-specific T1WI planning space. The intersections with the cortical surface defined the initial cortical entry candidates.

Candidate trajectories were retained when they satisfied the predefined angular constraints of 10°–25° relative to the sagittal plane and 50°–65° relative to the axial plane. A coronal-suture-based entry-zone constraint was subsequently applied, retaining cortical entry candidates located within 20 mm anterior to the estimated coronal-suture reference.

Each retained cortical entry point was connected to the predefined STN target to form a straight-line candidate trajectory.

## Candidate-set sizes

Aggregate results for the 15-case SWI analysis cohort (30 hemispheres), using the baseline vessel/sulcus/ventricle thresholds of 3.0/2.0/2.0 mm:

| Metric | Result |
|---|---:|
| Initial candidate trajectories | 15,000 |
| Nominal-feasible candidates | 8,131 |
| Robust-feasible candidates | 5,940 |
| Pareto non-dominated candidates | 241 |
| Candidates rejected after robust screening | 2,191 (26.9%) |
| Hemispheres retaining at least one robust-feasible trajectory | 30/30 |

The underlying release file contains aggregate statistics only; it does not contain hemisphere or patient identifiers.

## Runtime

- Optimization runtime: 1.033 ± 0.074 s per hemisphere.
- Total preprocessing runtime: 159.676 ± 14.246 s per case.
- Candidate-generation-only runtime was not separately recorded.

Full machine-readable aggregates are provided in `candidate_runtime_summary.csv`.

