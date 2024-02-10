---
title: 2022.7-2023.11 Leveraging Multi-Stream Information Fusion for Trajectory Prediction
---

### Introduction

Trajectory prediction is a fundamental problem and
challenge for autonomous vehicles. Early works mainly focused
on designing complicated architectures for deep-learning-based
prediction models in normal-illumination environments, which
fail in dealing with low-light conditions. The paper proposes
a novel approach for trajectory prediction in low-illumination
scenarios by leveraging multi-stream information fusion, which
integrates image, optical flow, and object trajectory information.
This is achieved by applying Convolutional Neural Networkbased (CNN) Long Short-term Memory (LSTM) networks to
extract temporal information from the image channel, SpatialTemporal Graph Convolutional Network (ST-GCN) to model relative motion between adjacent camera frames through the optical
flow channel, and recognizing high-level interactions between
vehicles in the trajectory channel. Further, to investigate the
reliability of the model in low-illumination scenarios, epistemic
uncertainty estimation is conducted by applying Monte Carlo
Dropout. The proposed approach is validated on HEV-I and
newly generated Dark-HEV-I datasets focusing on graph-based
interaction understanding and low illumination conditions. The
experimental results show improved performance compared to
baselines in both standard and low-illumination scenarios. Importantly, our approach is generic and applicable to scenarios with
different types of perception data. 

### Framework Design

1. The Image channel : extract temporal information of the
camera (CNN+LSTM)
2. The Optical Flow Channel: capture the pattern of relative motion.(ST-GCN)
3. The Trajectory Channel: represent interactions between traffic participants.(ST-GCN)

[//]: # (![framwork]&#40;https://github.com/TommyGong08/tommygong08.github.io/blob/main/_includes/img/0_Multi_Stream.png&#41;)

<div class="card mb-3">
    <img class="card-img-top" src="https://raw.githubusercontent.com/TommyGong08/tommygong08.github.io/main/_includes/img/0_Multi_Stream.png"/>
    <div class="card-body bg-light">
        <div class="card-text">
            The proposed framework.
        </div>
    </div>
</div>


### Tech Stack
- Theory
  - Computer Vision
  - Machine Learning
- Programming
  - Python
  - Pytorch
  - OpenCV





