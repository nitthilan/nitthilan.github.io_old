---
layout: post
title:  "Deep Learning Ian Goodfellow [Things to read] "
date:   2017-02-16 00:33:14 +0530
categories: Notes, Deep Learning
---

# Lesson 2: Linear Algebra
- Eigen Decomposition
- Singular Value Decomposition
- The Moore-Penrose Pseudoinverse
- Principal Component Analysis

# Lesson 3: Probability

- The notions of covariance and dependence are related, but are in fact distinct concepts. They are related because two variables that are independent have zero covariance, and two variables that have non-zero covariance are dependent. How- ever, independence is a distinct property from covariance. For two variables to have zero covariance, there must be no linear dependence between them. Independence is a stronger requirement than zero covariance, because independence also excludes nonlinear relationships. It is possible for two variables to be dependent but have zero covariance. For example, suppose we first sample a real number x from a uniform distribution over the interval [−1, 1]. We next sample a random variable s. With probability 1, we choose the value of s to be 1. Otherwise, we choose 2
the value of s to be −1. We can then generate a random variable y by assigning y = sx. Clearly, x and y are not independent, because x completely determines the magnitude of y. However, Cov(x, y) = 0.

- Conditional probability is simpler and can be calculated easily. This is used for calculating the probability of distribution over set of varialbles

- Chain rule of conditional probability

- Second, out of all possible probability distributions with the same variance, the normal distribution encodes the maximum amount of uncertainty over the real numbers. We can thus think of the normal distribution as being the one that inserts the least amount of prior knowledge into a model. Fully developing and justifying this idea requires more mathematical tools, and is postponed to Sec.
19.4.2.

- Mixtures of Distributions ???

- logistic sigmoid, softplus, positive part function
- Technical Details of Continuous Variables - measure theory???
- Kullback-Leibler (KL) divergence
- structured probabilistic model or graphical
model. - Directed models, Undirected models????

# Lesson 4: Numerical Computation 
- Constrained Optimization???? 

# Lesson Basic Machine Learning:
- Statistical learning theory provides various means of quantifying model capacity. Among these, the most well-known is the Vapnik-Chervonenkis dimension, or VC dimension. The VC dimension measures the capacity of a binary classifier. The VC dimension is defined as being the largest possible value of m for which there
exists a training set of m different x points that the classifier can label arbitrarily.

- Cross validation is used to compare two algorithms and decide which to use. It does not mandate which model to use. It is used when the training data set size is small


- Chapter 2:
- Gradient Bandit Algorithms: Derivation ????

- Chapter 5:
- Off-policy Prediction via Importance Sampling and later sections

- Chapter 6:
- Example 6.4 illustrates a general difference between the estimates found by batch TD(0) and batch Monte Carlo methods. Batch Monte Carlo methods always find the estimates that minimize mean-squared error on the training set, whereas batch TD(0) always finds the estimates that would be exactly correct for the maximum-likelihood model of the Markov process. In general, the maximum-likelihood estimate of a parameter is the parameter value whose probability of generating the data is greatest. In this case, the maximum-likelihood estimate is the model of the Markov process formed in the obvious way from the observed episodes: the estimated transition probability from i to j is the fraction of observed transitions from i that went to j, and the associated expected reward is the average of the rewards observed on those transitions. Given this model, we can compute the estimate of the value function that would be exactly correct if the model were exactly correct. This is called the certainty-equivalence estimate because it is equivalent to assuming that the estimate of the underlying process was known with certainty rather than being approximated. In general, batch TD(0) converges to the certainty-equivalence estimate. ??? 



Open Universe: 
- http://localhost:15901/viewer/?password=openai - VNC host address
- universe starter agent:
	- tmux attach -t a3c
	- tmux kill-session -t a3c
	- http://localhost:12345 - tensorflow logs

Turbo vnc
- python train.py --num-workers 2 --env-id gym-core.PongDeterministic-v3 --log-dir /tmp/vncpong
- open vnc://localhost:5900 password:openai



Jana Slides:
- Nonstationary policies are used when we are given a
finite planning horizon H
5 I.e. we are told how many actions we will be allowed to take
h Nonstationary policies are functions from states and
times to actions
5 π:S x T → A, where T is the non-negative integers
5 π(s,t) tells us what action to take at state s when there are t
stages-to-go (note that we are using the convention that t
represents stages/decisions to go, rather than the time step)

- Probability of going to state s’ after taking action a in state s
g How many parameters does it take to represent?
m*n*(n-1) - O(m*n^2)


David Silver Lectures
- try to optimise the future rewards. deoes past reward have any impact??
- can time based discounting used to assign rewards for states and actionds to achieve necessary goals?
- how is stwate represented using history of obser ationa? MDP, Pomdp

Things to understand
- Actor Critic algorithm
- REINFORCE algorithm (Williams, 1992) 
   - <http://www-anw.cs.umass.edu/~barto/courses/cs687/williams92simple.pdf>
- Gradient following solution for Belman equation
   - 
- Monte-Carlo Planning
- Classification of different type of solutions for MDP
   - Dynamic Programming
   - Monte Carlo method
   - SARSA
- Belman Expectation  Equation for 
   - Marcov Decision Process
   - Markov 

- Belman Optimality Equation
   - Markov Decision Process


- Policy Evaluation (only updating value function and not updating policy i.e. using always only one policy. However this leads to an optimal policy)
   - Policy Evaluation uses a policy and so uses Bellman equation for updation using the policy i.e. uses Expectation and not Max
- Policy Iteration (Evaluate a given policy to get a new value [Policy Evaluation]. Then use this value to evaluate a greedy policy usch that new policy is better than the older policy [Policy Improvement])
   - MDP has only one optimal policy
- Value Iteration (Update Values using Bellman Optimality equation i.e. it uses MAX)
   - There is no policy calculation and keeps updating only values

- Synchronous is updating all the states in one shot after updating all states in the before state
- Asynchronous is keep using the new values as and when a new value is calculated 

- Planning - when full model is known trying to get the optimal policy

- Prediction - Evaluating a value for a given policy for the given MDP
- Control - Finding the optimal value for a given MDP

- On-Policy vs Off-Policy Learning

- COntraction Mapping theorem???
- forward TD(lambda), backward TD(lambda) ???

- GLIE Monte-Carlo Control

- Problem with bias and variance
   - TD has low variance since it uses only one random variable i.e. the immediate result
   - MC has lot of variance since the estimate is sum of lot of 
   - MC has zero bias since the estimate is always right (since updates happen after end of episode)

- Write all the equations in a cheat sheet


18th March 2017

Mountain Car Linear SArsa

Deep Q network for atari games

chain walk example


# Study of Lambda and Baird's Counter Example and Parameter Divergence
# Why Gradient TD converges for non-linear approx while TD does not?
# Why Gradient Q-Learning converges for linear while Q-Learning linear does not converge?
# Why Gradient Q-Learning does not converge and TD converges for non-linear?

Batch Prediction:
- Gradient descent with experience replay and fixed Q-targets
- fixed q targets means weigths are not update frequently and are kept fixed for batch learning 
- Once batch learning stabilises to a particulat value then weights are updated

Linear Least Square Prediction

Least Squares Policy Iteration Algorithms


Score Function:
- http://blog.shakirm.com/2015/11/machine-learning-trick-of-the-day-5-log-derivative-trick/
- score function gradient estimation
Asynchronous Methods for Deep Reinforcement Learning
- a3c https://arxiv.org/pdf/1602.01783.pdf

- opengym problems