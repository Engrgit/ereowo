![alt](./logos/ereowo.jpg)
# Ereowo- Hands on Reinforcement Learning AI Agent Library
### Proudly brought by Applied Reinforcement Learning @Gamol Studio

- v0.1 - Ereowo beta-version is now released!

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Support Ukraine](https://img.shields.io/badge/Support-Ukraine-FFD500?style=flat&labelColor=005BBB)](https://opensource.fb.com/support-ukraine)

More details of the library at our official website: [Link](www.gamolstudio.com)

Our paper is ArXived at: [Link](www.gamolstudio.com)

## Overview
Ereowo is a new hand on Reinforcement Learning AI agent library open-sourced by the Applied Reinforcement Learning team at Gamol Studio. Furthering our efforts on open AI innovation, Ereowo enables researchers and practitioners to develop Reinforcement Learning AI agents. These AI agents prioritize cumulative long-term feedback over immediate feedback and can adapt to environments with limited observability, sparse feedback, and high stochasticity. We hope that Ereowo offers the community a means to build state-of-the-art Reinforcement Learning AI agents that can adapt to a wide range of complex production environments.

## Getting Started

### Installation
To install Ereowo, you can simply clone this repo and pip install
```
git clone https://github.com/Engrgit/Erewo.git
cd Ereowo
pip install -e .
```

### Quick Start
To kick off a Ereowo agent with a classic reinforcement learning environment, here's a quick example.
```
from ereowo.ereowo_agent import EreowoAgent
from ereowo.action_representation_modules.one_hot_action_representation_module import (
    OneHotActionTensorRepresentationModule,
)
from ereowo.policy_learners.sequential_decision_making.deep_q_learning import (
    DeepQLearning,
)
from ereowo.replay_buffers.sequential_decision_making.fifo_off_policy_replay_buffer import (
    FIFOOffPolicyReplayBuffer,
)
from ereowo.utils.instantiations.environments.gym_environment import GymEnvironment

env = GymEnvironment("CartPole-v1")

num_actions = env.action_space.n
agent = EreowoAgent(
    policy_learner=DeepQLearning(
        state_dim=env.observation_space.shape[0],
        action_space=env.action_space,
        hidden_dims=[64, 64],
        training_rounds=20,
        action_representation_module=OneHotActionTensorRepresentationModule(
            max_number_actions=num_actions
        ),
    ),
    replay_buffer=FIFOOffPolicyReplayBuffer(10_000),
)

observation, action_space = env.reset()
agent.reset(observation, action_space)
done = False
while not done:
    action = agent.act(exploit=False)
    action_result = env.step(action)
    agent.observe(action_result)
    agent.learn()
    done = action_result.done
```
 

## Design and Features
![alt](./logos/ereowo_banner.jpg)
Ereowo was built with a modular design so that industry practitioners or academic researchers can select any subset and flexibly combine features below to construct a Ereowo agent customized for their specific use cases. Ereowo offers a diverse set of unique features for production environments, including dynamic action spaces, offline learning, intelligent neural exploration, safe decision making, history summarization, and data augmentation.

You can find many Ereowo agent candidates with mix-and-match set of reinforcement learning features in utils/scripts/benchmark_config.py

## Adoption in Real-world Applications
Ereowo is in progress supporting real-world applications, including recommender systems, auction bidding system and creative selection. Each of them requires a subset of features offered by Pearl. To visualize the subset of features used by each of the applications above, see the table below.
<center>

|Pearl Features | Recommender Systems | Auction Bidding | Creative Selection |
|:-------------:|:-------------------:|:---------------:|:------------------:|
|Policy Learning| ✅ |✅|✅|
|Intelligent Exploration|✅|✅ |✅|
|Safety| | ✅ | |
|History Summarization| | ✅ | |
|Replay Buffer| ✅ |✅ |✅ |
|Contextual Bandit| | |✅|
|Offline RL|✅|✅||
|Dynamic Action Space|✅||✅|
|Large-scale Neural Network|✅|||

</center>

## Comparison to Other Libraries
<center>

|Pearl Features | Pearl  | ReAgent (Superseded by Pearl) | RLLib | SB3|Tianshou | Dopamine |
|:-------------:|:------:|:-----------------------------:|:-----:|:--:|:-----:|:-----|
|Modularity|✅|❌|❌|❌|❌|❌|
|Dynamic Action Space|✅|✅|❌|❌|❌|❌|
|Offline RL|✅|✅|✅|✅|✅|❌|
|Intelligent Exploration|✅|❌|❌|❌|⚪ (limited support)|❌|
|Contextual Bandit|✅|✅|⚪ (only linear support)|❌|❌|❌|
|Safe Decision Making|✅|❌|❌|❌|❌|❌|
|History Summarization|✅|❌|✅|❌|⚪ (requires modifying environment state)|❌|
|Data Augmented Replay Buffer|✅|❌|✅|✅|✅|❌|

</center>

## Cite Us
```
@misc{ereowo2023paper,
    title = {Ereowo - A Production-ready Reinforcement Learning AI Agent Library},
    author = {Ibrahim Gbdegesin},
    year = 2023,
    eprint = {arXiv}
}
```

## License
Ereowo is MIT licensed, as found in the LICENSE file.

