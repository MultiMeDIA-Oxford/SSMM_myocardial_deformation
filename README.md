# Statistical Shape and Motion Model for Myocardial Deformation from Tagged Magnetic Resonance Imaging

## Overview

This repository will implement a principal component analysis (PCA)-based statistical shape and motion model (SSMM) for analysing myocardial deformation from tagged MRI data. The framework will capture high-dimensional spatial and temporal variation in myocardial geometry across the cardiac cycle and will be applied to downstream tasks such as myocardial infarction (MI) prediction. It will leverage tagged MRI-derived motion fields to model myocardial material motion beyond anatomical shape changes, enabling interpretable analysis of regional cardiac function and supporting applications in precision cardiology.

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

### Myocardial Tracking Validation
We manually tracked the tags for all 3 slices in 6 randomly selected subjects. We plot both the manual tags and the nearest tag from our preprocessing method on the tagged plane over a full cycle. Below is an example of 3 slices for 1 subject, with the remaining plots available [here](https://github.com/MultiMeDIA-Oxford/SSMM_myocardial_deformation/tree/main/figures/manual_tracking_validation).

<p align="center">
  <img alt="Manual vs automatic tags for basal slice." src="https://github.com/MultiMeDIA-Oxford/SSMM_myocardial_deformation/blob/main/figures/manual_tracking_validation/1286305/b1s_tracking.gif" width="30%">
&nbsp; &nbsp; &nbsp; &nbsp;
  <img alt="Manual vs automatic tags for midcavity slice." src="https://github.com/MultiMeDIA-Oxford/SSMM_myocardial_deformation/blob/main/figures/manual_tracking_validation/1286305/b2s_tracking.gif" width="30%">
&nbsp; &nbsp; &nbsp; &nbsp;
  <img alt="Manual vs automatic tags for apical slice." src="https://github.com/MultiMeDIA-Oxford/SSMM_myocardial_deformation/blob/main/figures/manual_tracking_validation/1286305/b3s_tracking.gif" width="30%">
</p>

# References

[1] G. Farnebäck, “Two-frame motion estimation based on polynomial expansion,” in Image Analysis, Lecture Notes in Computer Science, vol. 2749, 2003, pp. 363–370.
