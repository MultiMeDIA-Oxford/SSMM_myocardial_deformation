# Statistical Shape and Motion Model for Myocardial Deformation from Tagged Magnetic Resonance Imaging

## Overview

This repository will implement a principal component analysis (PCA)-based statistical shape and motion model (SSMM) for analysing myocardial deformation from tagged MRI data. The framework will capture high-dimensional spatial and temporal variation in myocardial geometry across the cardiac cycle and will be applied to downstream tasks such as myocardial infarction (MI) prediction. It will leverage tagged MRI-derived motion fields to model myocardial material motion beyond anatomical shape changes, enabling interpretable analysis of regional cardiac function and supporting applications in precision cardiology.

```bibtex
@unpublished{seale_myocardial_shape_motion,
  author  = {Seale, Thalia Eleni and Grau, Vicente and Banerjee, Abhirup},
  title   = {Statistical Shape and Motion Model for Myocardial Deformation from Tagged Magnetic Resonance Imaging},
  note    = {Manuscript in preparation / under review},
  year    = {2026}
}
```

## Supplementary Figures

### Myocardial Point Cloud Preprocessing

**Registering the tagged images into point cloud space.** We use the point clouds representing the anatomy derived from cine MRI to estimate a segmentation on the tagged MRI images. This is achieved by registering the tagged images into the point cloud space, and selecting points in the cloud close to the image plane. (The blue arrows signify the optical optical flow calculated at that time point.)
                                                                                             
<p align="center">
  <img alt="Registering the tagged images into point cloud space." src="https://github.com/MultiMeDIA-Oxford/SSMM_myocardial_deformation/blob/main/figures/3720320_b1s_pc_space_quiver.png" width="45%">
&nbsp; &nbsp; &nbsp; &nbsp;
  <img alt="Registering the tagged images into point cloud space." src="https://github.com/MultiMeDIA-Oxford/SSMM_myocardial_deformation/blob/main/figures/3720320_b1s_pc_space_quiver_xy.png" width="45%">
</p>

**Optical flow (Eulerian Field).** We calculate the optical flow between each frame using the Farnebäck algorithm [1]. The red arrows represent the direction and magnitude (x6) of the optical flow for the pixel at the base of each arrow at each frame. The Eulerian field can be interpreted as the flow through the pixel at that time point.

<p align="center">
  <img alt="Optical flow for basal slice." src="https://github.com/MultiMeDIA-Oxford/SSMM_myocardial_deformation/blob/main/figures/optical_flow/b1s_flow_diag.gif" width="30%">
&nbsp; &nbsp; &nbsp; &nbsp;
  <img alt="Optical flow for midcavity slice." src="https://github.com/MultiMeDIA-Oxford/SSMM_myocardial_deformation/blob/main/figures/optical_flow/b2s_flow_diag.gif" width="30%">
&nbsp; &nbsp; &nbsp; &nbsp;
  <img alt="Optical flow for apical slice." src="https://github.com/MultiMeDIA-Oxford/SSMM_myocardial_deformation/blob/main/figures/optical_flow/b3s_flow_diag.gif" width="30%">
</p>

**Myocardial material point tracking.** We apply the optical flow fields to the fitted meshes at ED via advection, giving points tracking the position of the myocardial material at each frame. We show an example for 3 slices for one subject, with additional examples available [here](https://github.com/MultiMeDIA-Oxford/SSMM_myocardial_deformation/tree/main/figures/lagrangian_motion_meshes/1286305).

<p align="center">
  <img alt="Lagrangian motion for basal slice." src="https://github.com/MultiMeDIA-Oxford/SSMM_myocardial_deformation/blob/main/figures/lagrangian_motion_meshes/1286305/b1s_mesh_motion.gif" width="30%">
&nbsp; &nbsp; &nbsp; &nbsp;
  <img alt="Lagrangian motion for midcavity slice." src="https://github.com/MultiMeDIA-Oxford/SSMM_myocardial_deformation/blob/main/figures/lagrangian_motion_meshes/1286305/b2s_mesh_motion.gif" width="30%">
&nbsp; &nbsp; &nbsp; &nbsp;
  <img alt="Lagrangian motion for apical slice." src="https://github.com/MultiMeDIA-Oxford/SSMM_myocardial_deformation/blob/main/figures/lagrangian_motion_meshes/1286305/b3s_mesh_motion.gif" width="30%">
</p>

**Myocardial mesh.** We transform the tracked material points back into the coordinate system of the cine-derived point clouds. We show 3 examples with the cine-derived biventricular reconstruction as a reference.

<p align="center">
  <img alt="Myocardial point cloud motion for subject 1169306." src="https://github.com/MultiMeDIA-Oxford/SSMM_myocardial_deformation/blob/main/figures/myocardial_point_cloud/1169306_combined_mesh_motion_pc_space.gif" width="45%">
&nbsp; &nbsp;
  <img alt="Myocardial point cloud motion for subject 1409794." src="https://github.com/MultiMeDIA-Oxford/SSMM_myocardial_deformation/blob/main/figures/myocardial_point_cloud/1409794_combined_mesh_motion_pc_space.gif" width="45%">
</p>

<p align="center">
  <img alt="Myocardial point cloud motion for subject 1459356." src="https://github.com/MultiMeDIA-Oxford/SSMM_myocardial_deformation/blob/main/figures/myocardial_point_cloud/1459356_combined_mesh_motion_pc_space.gif" width="45%">
&nbsp; &nbsp;
  <img alt="Myocardial point cloud motion for subject 4069206." src="https://github.com/MultiMeDIA-Oxford/SSMM_myocardial_deformation/blob/main/figures/myocardial_point_cloud/4069206_combined_mesh_motion_pc_space.gif" width="45%">
</p>

### Myocardial Tracking Validation
We manually tracked the tags for all 3 slices in 6 randomly selected subjects. We plot both the manual tags and the nearest tag from our preprocessing method on the tagged plane over a full cycle. Below is an example of 3 slices for 1 subject, with the remaining plots available [here](https://github.com/MultiMeDIA-Oxford/SSMM_myocardial_deformation/tree/main/figures/manual_tracking_validation).

<p align="center">
  <img alt="Manual vs automatic tags for basal slice." src="https://github.com/MultiMeDIA-Oxford/SSMM_myocardial_deformation/blob/main/figures/manual_tracking_validation/1286305/b1s_tracking.gif" width="30%">
&nbsp; &nbsp; &nbsp; &nbsp;
  <img alt="Manual vs automatic tags for midcavity slice." src="https://github.com/MultiMeDIA-Oxford/SSMM_myocardial_deformation/blob/main/figures/manual_tracking_validation/1286305/b2s_tracking.gif" width="30%">
&nbsp; &nbsp; &nbsp; &nbsp;
  <img alt="Manual vs automatic tags for apical slice." src="https://github.com/MultiMeDIA-Oxford/SSMM_myocardial_deformation/blob/main/figures/manual_tracking_validation/1286305/b3s_tracking.gif" width="30%">
</p>

### Latent Traversal

**Shape modes.** We vary each shape mode from -2 to 2 standard deviations (SD) to visualise the effect of each shape mode on the output shape. We show the two modes presented in the paper below, and include visualisations of al the modes [here](https://github.com/MultiMeDIA-Oxford/SSMM_myocardial_deformation/tree/main/figures/shape_modes).

<p align="center">
  <img alt="Shape mode component 8"
       src="https://raw.githubusercontent.com/MultiMeDIA-Oxford/SSMM_myocardial_deformation/main/figures/shape_modes/component_8.gif"
       width="45%">
&nbsp; &nbsp; &nbsp; &nbsp;
  <img alt="Shape mode component 28"
       src="https://raw.githubusercontent.com/MultiMeDIA-Oxford/SSMM_myocardial_deformation/main/figures/shape_modes/component_28.gif"
       width="45%">
</p>

# References

[1] G. Farnebäck, “Two-frame motion estimation based on polynomial expansion,” in Image Analysis, Lecture Notes in Computer Science, vol. 2749, 2003, pp. 363–370.
