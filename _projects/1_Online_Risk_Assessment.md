---
title: 2023.3-2023.9 Online Risk Assessment for Human-robot Interaction
---

### Introduction

As human-robot interaction scenarios are anticipated to constitute a considerable proportion in the ensuing decades, the provision of safety during human-robot interaction is of paramount significance, and risk assessment plays an indispensable role in this regard. However, conventional risk assessment techniques reliant upon the Hamilton-Jacobi-Isaacs (HJI) method necessitate offline calculation and suffer from computational onus. Although data-driven methods serve as a feasible solution to address the resultant computational complexities, it is critical to extract the full value of emerging datasets and adequately validate the efficacy of these pioneering models. To solve these problems, this research presents the implementation of an online data-driven risk assessment methodology designed to cater to human-robot interaction scenarios. The proposed method involves offline training of neural networks for predicting the control actions of agents. The augmented dynamic model, constrained by the control action, is then constructed and used to predict the Forward Reachable Set (FRS) utilizing the HJI method. The high dimensionality of the states results in the difficulty of solving PDEs, which prompts the introduction of a value approximator utilizing state-of-the-art neural networks. Both the pre-trained motion prediction model and value approximator are aggregated to enable online precise FRS inference. The effectiveness of the proposed approach is validated through testing with different motion prediction models and under various dynamic models. Furthermore, the feasibility of this data-driven methodology is demonstrated through an online risk assessment of a robot in an intersection scenario. 
<br>


<div class="card mb-3">
    <img class="card-img-top" src="https://raw.githubusercontent.com/TommyGong08/tommygong08.github.io/main/_includes/img/1_Online_Risk.png"/>
    <div class="card-body bg-light">
        <div class="card-text">
           The schematic diagram of the proposed framework. From top to
bottom are the data-driven period, NN-PDE solver, and risk assessment
process. The data-driven period consists of the interaction motion prediction
which is used for control action prediction for the agents in the interaction
scenarios, while the off-line pre-trained value approximator considers the
agent’s dynamic and the state-of-the-art high-dimensional value approximate
methods. Next, both pre-trained models are used online during the FRS
inference. ultimately, the predicted FRS is utilized for risk assessment.
        </div>
    </div>
</div>


### Tech Stack
- Theory
  - Artificial Intelligence
  - Deep Learning
  - PDE
  - Robotics
  - Probability
- Programming
  - Python