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

