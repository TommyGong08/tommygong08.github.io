---
title: 2021.12-2022.6 **(Research)** Improvement and Realization of Stochastic Contextual Bandit Problem
---

* **Graduation Thesis Project**, supervised by [Dr. Zhengyang Liu](https://lozycs.github.io/)

### Main Work
1. Focused on the stochastic contextual bandit problem, the NeuralUCB algorithm improves the ε-Greedy Algorithm by 
utilizing upper confidence bound (UCB) based exploration to optimize stochastic multi-armed bandit.
2. Proposed a novel model with a Long Short Term Memory (LSTM) network to extract temporal data of the
reward function.
3. Experimented on the synthetic datasets to verify how agent selected action and compared the ETC, UCB,
and ε-Greedy using the accumulated regret and the ratio of selecting optimal action as the performance
metric in the stochastic multi-armed bandit problem.
4. Compared the LinUCB, NeuralEpsilonGreedy, LstmUCB and NeuralUCB using the accumulated reward
and ratio of selecting optimal action in the stabilization stage based on the synthetic dataset of the nonlinear
reward function.
5. Experimental results showed that LstmUCB Algorithm outperformed the NeuralUCB algorithm in periodic
reward function, and NeuralEpsilonGreedy-based exploration outperformed NeuralUCB on certain datasets,
thus verifying the validity of the proposed improvement method.

<div class="card mb-3">
    <img class="card-img-top" src="https://numberly.com/2021/07/9ZABndg0-image-bandit-manchot.png"/>
    <div class="card-body bg-light">
        <div class="card-text">
            Bandit Problem (Pic from Internet)
        </div>
    </div>
</div>


### Tech Stack
- Theory
  - Bandit Theory(ε-greedy & UCB)
  - Reinforcement Learning
- Programming
  - Python
  - Pytorch










