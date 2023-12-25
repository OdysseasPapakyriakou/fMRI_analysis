# Description
This repository is for the basic and advanced fMRI analysis courses
at Utrecht University, as part of the elective space for the 
MSc in Artificial Intelligence.

# Basic fMRI analysis
This study investigates the difference in BOLD signal for movement of the hands,
the feet, and the tongue, as compared to resting state BOLD signal. All analyses in this
study were performed with the SPM package in a MATLAB environment. A detailed explanation
is found in the report.

### Preprocessing pipeline
1. Realignment for motion correction
2. Slice timing correction the time difference with which an fMRI sequence acquires the scans.
3. Coregistration to align and register the functional scans with structural/anatomical brain images.
4. Normalization to map the fMRI data of different subjects to a common coordinate space.
5. Smoothing to account for the limited spatial overlap in activity between subjects after normalization.

### First-level statistical analysis (individual level)
Aimed at estimating the task related brain activity per voxel for each subject

### Second-level statistical analysis (group level)
Aimed at groupwise inference, for identifying statistically significant voxels per tasks at a group level.

# Advanced fMRI analysis
3 studies exploring different fields and tools in fMRI research. Again, a detailed explanation is
found in the report.

## Study 1: Connectivity analysis
This study investigates whether the extent of functional connectivity between areas might depend
on the different task conditions, also referred to as *psychophysical interaction*.
This involves a bilinear model of how condition A (the psychological context) changes the
influence of area B on area C, corresponding to differences in regression slopes for 
different conditions. 

Preprocessing of the fMRI scans was performed as described in the preprocessing pipeline
for the basic fMRI analysis course above. All further analyses were performed with 
the CONN toolbox in a MATLAB environment.

### Additional prepocessing
1. Segmentation and specification of nuisance factors: white matter, CSF, and motion parameters.
2. Denoising to filter out the confounding factors in connectivity.

### First-level statistical analysis (individual level)
Seed-based voxel analysis to identify differences in connectivity patterns between conditions
for each individual.

### Second-level statistical analysis (group level)
Explores whether there is an average difference in functional connectivity when considering
all subjects. Specifically, it tests for different seed based connectivity patterns
between the sensorimotor networks for the rest, feet, and tongue conditions.

## Study 2: Independent Component Analysis
Contrary to the aforementioned seed to voxel connectivity analysis,
Independent Component Analysis (ICA) is not hypothesis driven, but data driven.
It thus aims to uncover statistically independent components from the observed fMRI data.

The analysis was performed with the GIFT toolbox in a MATLAB environment for one subject,
using the normalized fMRI data, and setting the number of components to 20. The components 
represent anything that produces enough change in the signal, so this can be task-related,
or artefact from respiration, heartbeat, and so on.

The study performs ICA and examines whether each of the 20 components is a BOLD signal
or an artefact.

## Study 3: Surface-based analysis
This study maps the statistical fMRI results of a single subject from the tongue task 
to a surface representation of the brain. This entails changing the brain representation
from a volume to a surface, aka as a **polygon mesh**, which is a collection of vertices, 
edges, and faces (triangle), that collectively define the shape of a polyhedral object.
*Vertices* represent the coordinates in three-dimensional space, *edges* represent the
connections between the vertices, and *triangles* describe the interconnectedness
of the vertices.

Surface-based analysis has several advantages:
1. It improves intersubject alignment. In contrast, when doing volumetric-based normalization, 
a small error in the three-dimensional space may translate into a very large error
across the cortical surface. However, with surface-based normalization, the brain of all 
individuals is inflated and transformed into a spherical representation, thus allowing
to align the sulci and the gyri based on sulcal depth information. Any errors that may
occur with this process are found across the cortical surface, and not in the three-dimensional
space.
2. It improves smoothing, as volumetric-based smoothing smears the data across the sulci,
resulting in smoothing way further than the surface of the cortex. However, surface-based
smoothing is more effective as it only includes neighbouring grey matter.
3. It allows for more informative visualizations, while it is also better for
interpreting topographic activity

### Mapping the functional data to the surface
Mapping the functional data to the surface was done using the *Connectome Workbench* software
from the Human Connectome Project. The reconstruction of the surface in native space
had already been performed with the *FreeSurfer* software and had been converted to Gift 
format, so that it is compatible with the *Connectome Workbench*. For each hemisphere,
it included pial, white matter, and midgrey surfaces, Aparc labels, sulcal depth,
cortical thickness, curvature, as well as the T1-weighted image aligned with the
surface reconstruction.

