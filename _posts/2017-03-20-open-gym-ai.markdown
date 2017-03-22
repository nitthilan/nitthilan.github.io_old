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
        - https://gym.openai.com/users/avalcarce
        - https://github.com/avalcarce/gym-learn
        	- Prioritized Experience Replay
- Policy Gradient
    - Monte-Carlo Policy Gradient (REINFORCE)
        - https://gym.openai.com/evaluations/eval_LIdRc2cMTt6xHGpSs7DLdQ
    - Q Actor Critic
    - Advantage Actor Critic Action Value (A3C)
        - 
    - TD Actor Critic
    - TD lambda Actor Critic

- Discrete State space with discrete action space
    - Monte-Carlo Tree Search
        - Text based, board games
        - https://gym.openai.com/evaluations/eval_9ZnTspgvSYK6O0PCkEFYQ
- Cross Entropy Method:
    - Create a Linear Policy Evaluation function, which is a weighted product of the observation vector resulting in a action
    - Initialise the weights based on a gaussian mean and std deviation for each weight vector in a batch
    - Run a batch for evaluating each weight vector performance
    - Chooses the top 20-30% of runs which gave a better performance than the other runs
    - USe the weights of these top 20-30% weight vectors to evaluate the new mean and std deviation
    - Use this to initialise the next batch of weights
    - Repeat the procedure to choose the top 20-30% runs 
    - Ideally you should observe the std deviation reducing with each iteration and weights moving towards a particular mean 
    - https://gym.openai.com/evaluations/eval_i00byoG8SQSlWo0fxOPAqg
    - Not read fully:
        - https://gym.openai.com/algorithms/alg_nDvFTLrXQ8mYPe5aEGeWCw
        - https://gym.openai.com/algorithms/alg_ZIW1ntx0RQ2LZpw309n7A
- Advantage Actor Critic Action Value (A3C)
    - [Using Keras and Deep Deterministic Policy Gradient to play TORCS](https://yanpanlau.github.io/2016/10/11/Torcs-Keras.html)
        - https://github.com/yanpanlau/DDPG-Keras-Torcs
    - [Asynchronous Methods for Deep Reinforcement Learning](https://arxiv.org/abs/1602.01783)
    - [Talk on RL - Faster Deep Reinforcement Learning for Playing Atari](https://skillsmatter.com/skillscasts/8550-faster-deep-reinforcement-learning-for-playing-atari)
    - https://github.com/coreylynch/async-rl
- [PGQ: COMBINING POLICY GRADIENT AND Q-LEARNING](https://arxiv.org/pdf/1611.01626v1.pdf)
- Experience Replay
    - [Asynchronous Methods for Deep Reinforcement Learning](https://arxiv.org/abs/1602.01783)
    - 

- Algorithms implemented
    - 

### Queries

- Parameter Divergence in Baird’s Counterexample??