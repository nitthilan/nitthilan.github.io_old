---
layout: post
title:  "3d NoC Core Placement Optimisation"
date:   2017-04-25 00:33:14 +0530
categories:  
---

#### List of Queries
- How is graph created for a 3D world problem?
- How are successive points choosen i.e design space decided based on the next predicted point?
- Emperical Confidence Level?

#### GP Scikit Learning
- They lose efficiency in high dimensional spaces – namely when the number of features exceeds a few dozens.
- The prior mean is assumed to be constant and zero (for normalize_y=False) or the training data’s mean (for normalize_y=True)
- Kernal Object - Prior's covariance
- Optimizer - The hyperparameters of the kernel are optimized during fitting of GaussianProcessRegressor by maximizing the log-marginal-likelihood (LML) based on the passed
- n_restarts_optimizer - As the LML may have multiple local optima, the optimizer can be started repeatedly by specifying 
- noise level: The noise level in the targets can be specified by passing it via the parameter alpha
- hyperparameter optimization using gradient ascent on the log-marginal-likelihood.

#### References
- [Bayesian Optimization](https://www.cs.ox.ac.uk/people/nando.defreitas/publications/BayesOptLoop.pdf)
- Gaussian Process
	- http://mlss2011.comp.nus.edu.sg/uploads/Site/lect1gp.pdf
	- http://mlg.eng.cam.ac.uk/tutorials/06/es.pdf
	- http://www.cs.toronto.edu/~urtasun/tutorials/GP_tutorial.html
	- https://www.robots.ox.ac.uk/~mebden/reports/GPtutorial.pdf
- Graph Kernels
	- http://people.cs.uchicago.edu/~risi/papers/VishwanathanGraphKernelsJMLR.pdf (an overview of concepts)
	- http://www.jmlr.org/papers/volume12/shervashidze11a/shervashidze11a.pdf (this is important for this project)
	- https://www.cs.ucsb.edu/~xyan/tutorial/GraphKernels.pdf
- [STAGE algorithm](https://mail.google.com/mail/u/0/?ui=2&ik=ff424d53fe&view=att&th=15b9cbcbb9030b72&attid=0.1&disp=inline&realattid=f_j1v7nxkr0&safe=1&zw)
- [Small-world Design Space and 3D Network-on-Chip](https://arxiv.org/ftp/arxiv/papers/1608/1608.06972.pdf)
- [private link](https://mail.google.com/mail/u/0/?ui=2&ik=ff424d53fe&view=att&th=15b9b699433ae895&attid=0.1&disp=inline&realattid=f_j1uuemq40&safe=1&zw)

#### Reference 2
- optimizing combinatorial structured spaces
	- [Preference Learning with Gaussian Processes](http://mlg.eng.cam.ac.uk/zoubin/papers/icml05chuwei-pl.pdf)
	- [Extensions of Gaussian Processes for Ranking: Semi-supervised and Active Learning](https://pdfs.semanticscholar.org/af25/75ccaa688890a11f78a58c061ece7ca7399c.pdf)
	- [Semi-supervised Gaussian Process Classifiers](http://vikas.sindhwani.org/ssgp.pdf)
	- [Gaussian Process Preference Elicitation](http://users.cecs.anu.edu.au/~sguo/gppe.pdf) - paper is indirectly relevant. We need to see if we can map and/or leverage some of the insights from this paper.
- [Bayes Optimisation 2016](https://bayesopt.github.io/accepted.html)
	- [Bayesian Optimisation with Pairwise Preferential Returns](https://bayesopt.github.io/papers/2016/Gonzalez.pdf)
- [NEURAL ARCHITECTURE SEARCH WITH REINFORCEMENT LEARNING](https://openreview.net/forum?id=r1Ue8Hcxg&noteId=r1Ue8Hcxg)


#### Reference 3
- [Scikit Implementation](http://scikit-learn.org/stable/modules/gaussian_process.html)
	- [Tutorial](https://blog.dominodatalab.com/fitting-gaussian-process-models-python/)
- [GraphKernals](https://github.com/eghisu/GraphKernels)
	- [PyKernal](https://github.com/gmum/pykernels) - Does not seem to support WL Kernals
- [In-Datacenter Performance Analysis of a Tensor Processing Unit](https://arxiv.org/pdf/1704.04760.pdf)

#### Reference 4
- [NEURAL ARCHITECTURE SEARCH WITH REINFORCEMENT LEARNING](https://openreview.net/pdf?id=r1Ue8Hcxg) - [link1](https://openreview.net/forum?id=r1Ue8Hcxg&noteId=r1Ue8Hcxg)
- [COMPOSITIONAL KERNEL MACHINES](http://homes.cs.washington.edu/~pedrod/papers/iclr17.pdf)
- [In-Datacenter Performance Analysis of a Tensor Processing Unit](https://arxiv.org/pdf/1704.04760.pdf) - ISCA 2017 paper detailing their TPUs (ASIC for deep learning inference). In particular the performance, energy, and other considerations
- [Imitation Learning for Dynamic VFI Control in Large-Scale Manycore Systems](https://mail.google.com/mail/u/0/?ui=2&ik=ff424d53fe&view=att&th=15bbb8c817ab73f3&attid=0.2&disp=inline&realattid=f_j1zlobao1&safe=1&zw) - TVLSI paper where we looked at the dynamic optimization problem. we can develop a more efficient approach building on the work we are doing for optimizing structured spaces
- [Machine Learning and Manycore Systems: A Serendipitous Symbiosis - Read](https://mail.google.com/mail/u/0/?ui=2&ik=ff424d53fe&view=att&th=15bbb8965bd15ab4&attid=0.1&disp=inline&realattid=f_iz0e9zdm0&safe=1&zw) - IEEE computer paper (under review) may be useful to get a broader perspective about the problem space

#### Reference 5
- [Probabiistic Graphical Models](https://ermongroup.github.io/cs228-notes/)
	- [Structure Learning](https://hazyresearch.github.io/snorkel/blog/structure_learning.html)
- http://www.offconvex.org/2017/03/30/GANs2/
#### Reference 6
- [Hyperband: A Novel Bandit-Based Approach to Hyperparameter Optimization](https://arxiv.org/pdf/1603.06560.pdf)
- [Hyper Band : Embracing the Random](http://www.argmin.net/2016/06/23/hyperband/)
- [HyperTuning : The News on Auto-tuning](http://www.argmin.net/2016/06/20/hypertuning/)
- [Machine Learning with World Knowledge: The Position and Survey](https://arxiv.org/pdf/1705.02908.pdf)
- [Unbounded Bayesian Optimization via Regularization](https://arxiv.org/pdf/1508.03666.pdf)

#### Gaussian Process
- [Nando Feritas Lectures](http://www.cs.ubc.ca/~nando/540-2013/lectures.html)
- [GP tutorial - Toronto](http://www.cs.toronto.edu/~urtasun/tutorials/GP_tutorial.html)
- [Gaussian Processes for Machine Learning - Book](http://www.gaussianprocess.org/gpml/chapters/)
- [Gaussian Process for dummies](http://katbailey.github.io/post/gaussian-processes-for-dummies/) - Looks interesting
	- [Linear Regression - A Probabilistic Approach](http://katbailey.github.io/post/from-both-sides-now-the-math-of-linear-regression/)


#### Gaussian Processes Probably Interesting
- http://www.gaussianprocess.org/
- http://cs229.stanford.edu/section/cs229-gaussian_processes.pdf
- http://scikit-learn.org/stable/modules/gaussian_process.html

- [A Tutorial on Bayesian Optimization of Expensive Cost Functions, with Application to Active User Modeling and Hierarchical Reinforcement Learning](https://arxiv.org/pdf/1012.2599.pdf)

#### Understanding
- Desing Space Exploration and Optimisation of an Energy-Efficient and Reliable 3D Small-world Network-on-Chip
- Optimizing Structured Spaces via Expensive Experiments: Algorithms and Application to Manycore Systems Design

- Learning Evaluation Functions to Improve Optimization by Local Search [STAGE]

- Taking the Human Out of the Loop: A Review of Bayesian Optimization
- Weisfeiler-Lehman Graph Kernels
- 


- Maximum Liklihood Estimation
	- Given some points the maximumliklihood of those points are from a particular probability distribution is given by assuming the mean to be average of all the values and std deviation equal to the std calculated by the data observed i.e. the mean and std of the probability is equivalent to the mean and std seen from the data.
- Linear Regression: Applying Maxlikelihood to linear regression is that each data point observered is assumed to be a random variable picked from a gaussian distribution. So Linear Regression is a function which tries to maximise probability of each data point (random variable) having a particular mean (given by X*Theta) and same std deviation for all the points given by the (Y - theta*X)'*(Y - theta*X)
- It is basically assuming each data point to be a independent gaussian variable and MaxLiklihood tries to maximise the prbability of occurance of all these data points together (Joint Probability) which is given be by product of individual probabilities of each data point. 
- Trying to maximise the Joint probability and thus the product is basically.
	- MLE is defined as arg max theta Product
- Law of large numbers:
	- Mean of a sample given by average of N numbers tends to integration(x*P(x)*dx) when N tends to infinity i.e. the actual expectation of a distribution can be approximated by averaging the observed data values. 
- Introducing regularization which tries to reduce the inverse matrix error going to infinity which can be reduced by adding a small value to diagonal. This maps to regulariser which tries to make many theta values zero or small and only features which have real impact are kept - This approximation is called ridge regression
- The next approximation is for non-linear regression approximation using polynomial approximation. However we can go one step further and try to approximate every point to be a kernal (since it is hard to estimate how many kernals are required) or radial basis function. Then try to learn the parameters of each kernal at each point i.e. the scale factor (theta).
- Assuming a basis function to be a gaussian and assuming that every point in the data to have the gaussian kernal, the offset is given by the data position and the kernal width is a free parameter to be estimated. 
- Here gausian is a kernal and so should not use meand ad std deviation but it should be offset and kernal width
- Here like the regularisation parameter delta   we assume the kernal width lambda to be same for all the gaussian kernals and they too are estimated (or approximated using cross validation)
- Either use K-Fold Cross validation or use a min of the max error between test and train error to decide on the lambda or delta
- Bayes rule: P(Theta/Data)[Posterior] = P(Data/Theta)[Liklihood]*P(theta)/P(Data)[prior]
- Since denominator term is a combinatorial problem i.e. something that does not have a simple solution and requires search,  it is generally assumed to be a constant.
- However, if we assume the distribution of Theta P(Theta) is a Gaussian, then by conjugate analysis we assume the P(theta/Data) also to be gaussian and So we can solve for the denominator assuming the integral of a gaussian is one and solving for the constant.
- Conjugate analysis is we assume that given a prior has a gaussian distribution the Posterior is also assumed to be a gaussian
- symetric positive definite means the covar matrix should be symmetric (across the diagonal i.e. covar(x1,x2) == covar(x2,x1) nad the variance should be positive )
- Cholesky decomposition - Mean + B*N(0,1)


#### Doubts to be clarified
- combinatorial problems
- http://www.sls-book.net/Slides/Chapter-1/ch1-slides-2p.pdf
- https://en.wikipedia.org/wiki/Combinatorial_optimization

- Graph Kernal
- https://en.wikipedia.org/wiki/Graph_kernel
- http://people.cs.uchicago.edu/~risi/papers/VishwanathanGraphKernelsJMLR.pdf
- https://www.ethz.ch/content/dam/ethz/special-interest/bsse/borgwardt-lab/documents/slides/CA10_GraphKernels_intro.pdf
- https://www.cs.ucsb.edu/~xyan/tutorial/GraphKernels.pdf


- Hilbert Spaces:
- https://en.wikipedia.org/wiki/Hilbert_space
- https://www.quora.com/What-are-Hilbert-Spaces-in-laymens-terms

- Reproducing Kernal Hilbert Spaces: 
- https://en.wikipedia.org/wiki/Reproducing_kernel_Hilbert_space
- https://people.eecs.berkeley.edu/~bartlett/courses/281b-sp08/7.pdf

- NP Completeness
- http://www.geeksforgeeks.org/np-completeness-set-1/
- https://www.quora.com/What-are-P-NP-NP-complete-and-NP-hard
- 

- Local Search Algorithms:
- https://www.cs.unc.edu/~lazebnik/fall10/lec06_local_search.pdf
- https://courses.cs.washington.edu/courses/csep573/11wi/lectures/04-lsearch.pdf
- Discretization of optimising continous functions uses hil-climbing approaches

- Positive semidefinite: In the last lecture a positive semidefinite matrix was defined as a symmetric matrix with non-negative eigenvalues.
- https://www.cse.iitk.ac.in/users/rmittal/prev_course/s14/notes/lec11.pdf

- Beta Distribution: https://en.wikipedia.org/wiki/Beta_distribution
- [genfromtext](https://docs.scipy.org/doc/numpy/reference/generated/numpy.genfromtxt.html)
- [lil_matrix](https://docs.scipy.org/doc/scipy/reference/generated/scipy.sparse.lil_matrix.html)

#### Understanding Gaussian Process
- ??? combinatorial structured objects, combinatorial spaces, Multi-armed bandit experiments
- T-distribution instead of gaussian kernals
- Linear Regression solution 
	- Theta = (XX')^-1 X'y
		- If X has lot of features, there could be certain features which would go to zero and so can make the matrix go to infinity. To avoid this a small error is added
	- Theta = (XX' + delta^2 Id)^-1 X'y
		- This is ridge regression and is a solution to the constrained problem (y - X*Theta)'(y - x*Theta) + delta^2*theta'*theta
		- This forces certain value of thetas to go to zero compared to others and thus helps in identifying what are the prominent features in a relation
		- The other approximation is called lasso constraint where they use abs(theta) instead of Theta'*theta. this forces the feature to go to zero directly. How?????
	- To use the same linear regression approximation, the x features could be replaced with non-linear features like x^2, x^3 called polynomial approximations.
	- Further this could be extended to other non-linear approximation like kernals Radial Basis etc and one such aprroximation is Gaussian functions.
	- Here to reduce the complexity of determining where you should have gaussian , we represent the gaussian at each X position and allowing the minimisation problem to zero it out if not required. So the mean value is the X value. The width or lambda can be different for each gaussian since it would be very complicated we assume a single lambda for all the gaussians.
	- Now the estimation of delta and lambda together becomes a combinatorial problem ????? to solve and is not feasible. If is just one we could use cross-validation (or K folds approximation) to solve for the parameters 

#### Understanding the problem statement
- The Core placement on a chip is considered as a graph with links as edges and cores are node
- 


#### General Understanding
- Small-world design space for 3D NoC:
	- 
- UCB and EI acquision function using the learned GP model.
- STAGE and/or RLS to optimize the acquision function 
