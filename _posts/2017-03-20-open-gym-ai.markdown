---
layout: post
title:  "OpenGym AI Basics "
date:   2017-02-16 00:33:14 +0530
categories: Notes, Reinforcement Learning
---


### Understanding Environment

- https://gym.openai.com/docs - Good introduction
    - Space - object that describes a valid action and observation
    - Discrete Space - Fixed range of non-negative numbers
    - Box Space - Continous N Dimensional box 

```python
import gym
from gym import envs
env = gym.make('CartPole-v0')
```
- Returns the type and size of the space
    - print(env.action_space)
- Incase of discrete returns the max size
    - print(env.action_space.n)
- Returns the type and dimension of the space
    - print(env.observation_space)
- Min and max value for each of the dimensions in the continous space
    - print(env.observation_space.high)
    - print(env.observation_space.low)

- Find the range of all the environments
    - https://github.com/openai/gym/wiki/Table-of-environments
    - https://github.com/openai/gym/issues/106
    - https://docs.google.com/document/d/1bCDna95FRfvFA850qwqqLqZxENdU70psiqaOGob9oLI/edit
- [Environment Interfaces](https://github.com/openai/gym/blob/master/gym/core.py)

- Some hacks to make the episodes run longer
    - https://github.com/openai/gym/wiki/FAQ

### Algorithms to try

- Value function approximation
    - Linear Action-Value function approximation using e-greedy 
    - Deep Q Networks
        - Experience Replay
        - fixed Q-Targets
- Policy Gradient
    - Monte-Carlo Policy Gradient (REINFORCE)
    - Q Actor Critic
    - Advantage Actor Critic
    - TD Actor Critic
    - TD lambda Actor Critic

- Algorithms implemented
    - 

### Queries

- Parameter Divergence in Baird’s Counterexample??