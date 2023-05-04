# 3D Object Detection for Autonomous Driving: A Comprehensive Survey (IJCV 2023)

[![arXiv](https://img.shields.io/badge/arXiv-2206.09474-b31b1b.svg)](https://arxiv.org/abs/2206.09474)
[![Maintenance](https://img.shields.io/badge/Maintained%3F-yes-green.svg)](https://github.com/PointsCoder/Awesome-3D-Object-Detection-for-Autonomous-Driving/graphs/commit-activity)
[![GitHub issues](https://img.shields.io/github/issues/PointsCoder/Awesome-3D-Object-Detection-for-Autonomous-Driving)](https://github.com/PointsCoder/Awesome-3D-Object-Detection-for-Autonomous-Driving/issues/)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg?style=flat-square)](http://makeapullrequest.com)

![overview](Figs/overview.JPG)

This repository is with our [survey paper](https://arxiv.org/abs/2206.09474):

> **Title:** 3D Object Detection for Autonomous Driving: A Comprehensive Survey <br>
> **Authors:** Jiageng Mao, Shaoshuai Shi, Xiaogang Wang, Hongsheng Li<br>
> **Publication:** International Journal of Computer Vision (IJCV) <br>

a.k.a

> **Title:** 3D Object Detection for Autonomous Driving: A Review and New Outlooks <br>
> **Authors:** Jiageng Mao, Shaoshuai Shi, Xiaogang Wang, Hongsheng Li<br>
> arXiv preprint arXiv:2206.09474<br>

We also provide a paper collection on 3D object detection for autonomous driving at [Awesome 3D Object Detection for Autonomous Driving](Papers.md).

## Content

![taxonomy](Figs/tax.JPG)

<a name="0"></a>

- [1. LiDAR-based 3D Object Detection](#1)
    - [1.1 Data representations for LiDAR 3D object detection](#1.1)
        - [1.1.1 Point-based 3D object detection](#1.1)
        - [1.1.2 Grid-based 3D object detection](#1.2)
        - [1.1.3 Point-voxel based 3D object detection](#1.3)
        - [1.1.4 Range-based 3D object detection](#1.4)
    - [1.2 Learning objectives for LiDAR 3D object detection](#1.5)
        - [1.2.1 Anchor-based 3D object detection](#1.5)
        - [1.2.2 Anchor-free 3D object detection](#1.6)
        - [1.2.3 3D object detection with auxiliary tasks](#1.6)
- [2. Camera-based 3D Object Detection](#2)
    - [2.1 Monocular 3D object detection](#2)
        - [2.1.1 Image-only monocular 3D object detection](#2.1)
        - [2.1.2 Depth-assisted monocular 3D object detection](#2.2)
        - [2.1.3 Prior-guided monocular 3D object detection](#2.3)
    - [2.2 Stereo-based 3D object detection](#2.4)
    - [2.3 Multi-camera 3D object detection](#2.4)
- [3. Multi-Modal 3D Object Detection](#3)
    - [3.1 Multi-modal detection with LiDAR-camera fusion](#3.1)
        - [3.1.1 Early-fusion based 3D object detection](#3.1)
        - [3.1.2 Intermediate-fusion based 3D object detection](#3.2)
        - [3.1.3 Late-fusion based 3D object detection](#3.3)
    - [3.2 Multi-modal detection with radar signals](#3.3)
    - [3.3 Multi-modal detection with high-definition maps](#3.3)
- [4. Temporal 3D Object Detection](#4)
    - [4.1 3D object detection from LiDAR sequences](#4.1)
    - [4.2 3D object detection from streaming data](#4.2)
    - [4.3 3D object detection from videos](#4.2)
- [5. Label-Efficient 3D Object Detection](#5)
    - [5.1 Domain adaptation for 3D object detection](#5.1)
    - [5.2 Weakly-supervised 3D object detection](#5.2)
    - [5.3 Semi-supervised 3D object detection](#5.3)
    - [5.4 Self-supervised 3D object detection](#5.4)
- [6. 3D Object Detection in Driving Systems](#6)
    - [6.1 End-to-end learning for autonomous driving](#6.1)
    - [6.2 Simulation for 3D object detection](#6.1)
    - [6.3 Robustness for 3D object detection](#6.1)
    - [6.4 Collaborative 3D object detection](#6.2)

<a name="1"></a>

## LiDAR-based 3D Object Detection

![](Figs/lidarmap.JPG)

A chronological overview of the most prestigious LiDAR-based 3D object detection methods. [[Back to content]](#0)

<a name="1.1"></a>

### Point-based 3D object detection [[Papers]](Docs/Sensor/LiDAR/point_view.md)

![](Figs/point.JPG)

A general point-based detection framework contains a point-based backbone network and a prediction head. The point-based backbone consists of several blocks for point cloud
sampling and feature learning, and the prediction head directly estimates 3D bounding boxes from the candidate points. [[Back to content]](#0)

<a name="1.2"></a>

### Grid-based 3D object detection [[Papers]](Docs/Sensor/LiDAR/volumetric_view.md)

![](Figs/grid.JPG)

The grid-based approaches rasterize point cloud into
3 grid representations: voxels, pillars, and bird’s-eye view (BEV) feature maps. 2D convolutional neural networks or 3D
sparse neural networks are applied on grids for feature extraction. 3D objects are finally predicted from BEV grid cells. [[Back to content]](#0)

<a name="1.3"></a>

### Point-voxel based 3D object detection [[Papers]](Docs/Sensor/LiDAR/mixed_views.md)

![](Figs/pv.JPG)

Single-stage point-voxel detection framework fuses
point and voxel features in the backbone network. Two-stage point-voxel detection framework first generates 3D object
proposals with a voxel-based 3D detector, and then refines these proposals using keypoints sampled from point cloud. [[Back to content]](#0)

<a name="1.4"></a>

### Range-based 3D object detection [[Papers]](Docs/Sensor/LiDAR/range_view.md)

![](Figs/range.JPG)

The first category of range-based approaches directly predicts
3D objects from pixels in range images, with standard 2D
convolutions, or specialized convolutional/graph operators
for feature extraction. The second category transforms features
from range view into bird’s-eye view or point-view,
and then detects 3D objects from the transformed view. [[Back to content]](#0)

<a name="1.5"></a>

### Anchor-based 3D object detection

![](Figs/anchor.JPG)

3D anchor boxes are placed at each BEV grid cell. Those anchors
that have high IoUs with ground truths are selected as
positives. The sizes and centers of 3D objects are regressed
from the positive anchors, and the objects’ heading angles
are predicted by bin-based classification and regression. [[Back to content]](#0)

<a name="1.6"></a>

### Anchor-free 3D object detection

![](Figs/anchorfree.JPG)

The anchor-free
learning targets can be assigned to diverse views, including
the bird’s-eye view, point view, and range view. Object
parameters are predicted directly from the positive samples. [[Back to content]](#0)


<a name="2"></a>

## Camera-based 3D Object Detection

![](Figs/cameramap.JPG)

A chronological overview of the camera-based 3D object detection methods. [[Back to content]](#0)

<a name="2.1"></a>

### Image-only monocular 3D object detection [[Papers]](Docs/Sensor/Camera/monocular.md)

![](Figs/imageonly.JPG)

Single-stage anchor-based approaches
predict 3D object parameters leveraging both image features
and predefined 3D anchor boxes. Single-stage anchor-free
methods directly predict 3D object parameters from image
pixels. Two-stage approaches first generate 2D bounding
boxes from a 2D detector, and then lift up 2D detection to
the 3D space by predicting 3D object parameters from the
2D RoI features. [[Back to content]](#0)

<a name="2.2"></a>

### Depth-assisted monocular 3D object detection [[Papers]](Docs/Sensor/Camera/monocular.md)

![](Figs/depth.JPG)

Depth-image based approaches obtain
depth-aware image features by fusing information from both the RGB image and the depth image. Pseudo-LiDAR based
methods first transform the depth image into a 3D pseudo point cloud, and then apply LiDAR-based 3D detector on the
point cloud to detect 3D objects. Patch-based approaches transform the depth image into a 2D coordinate map, and then
apply a 2D neural network on the coordinate map for detection. [[Back to content]](#0)

<a name="2.3"></a>

### Prior-guided monocular 3D object detection [[Papers]](Docs/Sensor/Camera/monocular.md)

![](Figs/prior.JPG)

Prior-guided approaches leverage object shape priors, geometric priors, segmentation and temporal constrains to help detect 3D objects. [[Back to content]](#0)

<a name="2.4"></a>

### Stereo-based 3D object detection [[Papers]](Docs/Sensor/Camera/stereo.md)

![](Figs/stereo.JPG)

2D-detection based methods first generate a pair of 2D
proposals from the left and right image respectively, and then estimate 3D object parameters from the paired proposals.
Pseudo-LiDAR based approaches predict a disparity map by stereo matching, and then transform the disparity estimation
into depth and 3D point cloud subsequently, followed by a LiDAR-based detector for 3D detection. Volume-based methods
construct a 3D feature volume by view transform, and then a grid-based 3D object detector is applied on the 3D volume
for detection. [[Back to content]](#0)

<a name="3"></a>

## Multi-Modal 3D Object Detection

![](Figs/fusionmap.JPG)

A chronological overview of the most prestigious multi-modal 3D object detection methods. [[Back to content]](#0)

<a name="3.1"></a>

### Multi-modal detection with LiDAR-camera fusion (Early-Fusion) [[Papers]](Docs/Sensor/MultiModal/lidar_and_camera.md)

![](Figs/early.JPG)

Early-fusion approaches enhance point cloud
features with image information before they are passed through a LiDAR-based 3D object detector. In region-level
knowledge fusion, 2D detection is firstly employed on images to generate 2D bounding boxes. Then 2D boxes are
extruded into viewing frustums to select proper point cloud regions for the subsequent LiDAR-based 3D object detection.
In point-level knowledge fusion, semantic segmentation is firstly applied on images, and then the segmentation results are
transferred from the image pixels to points and used as an additional feature attached to each point. The augmented point
cloud is finally passed through a LiDAR detector for 3D object detection. [[Back to content]](#0)

<a name="3.2"></a>

### Multi-modal detection with LiDAR-camera fusion (Intermediate-Fusion) [[Papers]](Docs/Sensor/MultiModal/lidar_and_camera.md)

![](Figs/inter.JPG)

Intermediate fusion approaches aim to
conduct multi-modal fusion at the intermediate steps of a 3D object detection pipeline. In backbone networks, pixel-to-point
correspondences are firstly established by camera-to-LiDAR transform, and then with the correspondences, LiDAR features
are fused with image features through diverse fusion operators. The fusion can be conducted either at the intermediate
layers or only at the output feature maps. In the proposal generation and refinement stage, 3D object proposals are first
generated and then projected into the camera and LiDAR views to crop features of different modalities. The multi-view
features are finally fused to refine the 3D object proposals for detection. [[Back to content]](#0)

<a name="3.3"></a>

### Multi-modal detection with LiDAR-camera fusion (Late-Fusion) [[Papers]](Docs/Sensor/MultiModal/lidar_and_camera.md)

![](Figs/late.JPG)

Late-fusion based approaches operate on the
outputs, i.e. 3D and 2D bounding boxes, generated from a LiDAR-based 3D object detector and an image-based 2D object
detector respectively. 3D boxes and 2D boxes are combined together and fused to obtain the final detection results. [[Back to content]](#0)

<a name="4"></a>

## Temporal 3D Object Detection

![](Figs/temporalmap.JPG)

A chronological overview of the most prestigious temporal 3D object detection methods. [[Back to content]](#0)

<a name="4.1"></a>


### 3D object detection from LiDAR sequences [[Papers]](Docs/Sequential/sequential.md)


![](Figs/lidarseq.JPG)

In temporal 3D object detection from LiDAR sequences, diverse temporal aggregation modules
are employed to fuse features and object proposals from
multi-frame point clouds. [[Back to content]](#0)

<a name="4.2"></a>


### 3D object detection from streaming data [[Papers]](Docs/Sequential/sequential.md)

![](Figs/stream.JPG)

Detection from streaming data is conducted on each LiDAR
packet before the scanner produces a complete sweep. [[Back to content]](#0)

<a name="5"></a>

## Label-Efficient 3D Object Detection

<a name="5.1"></a>

### Domain adaptation for 3D object detection [[Papers]](Docs/Learning/domain_adaptation.md)

![](Figs/da.JPG)

In real-world applications, 3D object detectors suffer from severe domain gaps across different datasets, sensors, and weather conditions. [[Back to content]](#0)

<a name="5.2"></a>

### Weakly-supervised 3D object detection [[Papers]](Docs/Learning/weak_learning.md)

![](Figs/weak.JPG)

Weakly-supervised approaches learn to
detect 3D objects with weak supervisory signals. [[Back to content]](#0)

<a name="5.3"></a>

### Semi-supervised 3D object detection [[Papers]](Docs/Learning/semi_learning.md)

![](Figs/semi.JPG)

Semi-supervised approaches first pretrain
a 3D detector on the labeled data, and then use the
pre-trained detector to produce pseudo labels or leverage
teacher-student models for training on the unlabeled data
to further boost the detection performance. [[Back to content]](#0)

<a name="5.4"></a>

### Self-supervised 3D object detection [[Papers]](Docs/Learning/self_learning.md)

![](Figs/self.JPG)

Self-supervised approaches first pre-train
a 3D detector on the unlabeled data in a self-supervised
manner, and then fine-tune the detector on the labeled data. [[Back to content]](#0)

<a name="6"></a>

## 3D Object Detection in Driving Systems

<a name="6.1"></a>

### End-to-end learning for autonomous driving [[Papers]](Docs/Applications/system.md)

![](Figs/end.JPG)

End-to-end autonomous driving aims to integrate all
tasks in autonomous driving, e.g. perception, prediction, planning, control, mapping, localization, into a unified framework
and learn these tasks in an end-to-end manner. [[Back to content]](#0)

<a name="6.2"></a>

### Collaborative 3D object detection [[Papers]](Docs/Applications/cooperative_perception.md)

![](Figs/coopr.JPG)

In collaborative 3D object detection, different
vehicles can communicate with each other to obtain a more
reliable detection results. [[Back to content]](#0)
