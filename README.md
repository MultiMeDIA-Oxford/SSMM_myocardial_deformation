# Statistical Shape and Motion Model (SSMM) for Myocardial Function

## Overview

This repository will implement a principal component analysis (PCA)-based statistical shape and motion model (SSMM) for analysing myocardial deformation from tagged MRI data. The framework will capture high-dimensional spatial and temporal variation in myocardial geometry across the cardiac cycle and will be applied to downstream tasks such as myocardial infarction (MI) prediction. It will leverage tagged MRI-derived motion fields to model myocardial material motion beyond anatomical shape changes, enabling interpretable analysis of regional cardiac function and supporting applications in precision cardiology.

## Supplementary Figures

### Myocardial Point Cloud Preprocessing

**Registering the tagged images into point cloud space.** We use the point clouds representing the anatomy derived from cine MRI to estimate a segmentation on the tagged MRI images. This is achieved by registering the tagged images into the point cloud space, and selecting points in the cloud close to the image plane.

                                                                                                          |                                                                                                                                                                                            
:-----------------------------------------------------------------------------------------------------------------------:|:---------------------------------------------------------------------------------------------------------------------------------------------------------------------------:
![](https://github.com/MultiMeDIA-Oxford/SSMM_myocardial_deformation/blob/main/figures/3720320_b1s_pc_space_quiver.png)  |  ![](https://github.com/MultiMeDIA-Oxford/SSMM_myocardial_deformation/blob/main/figures/3720320_b1s_pc_space_quiver_xy.png)



