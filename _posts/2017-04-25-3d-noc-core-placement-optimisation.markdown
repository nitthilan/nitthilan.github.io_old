---
layout: post
title:  "3d NoC Core Placement Optimisation"
date:   2017-04-25 00:33:14 +0530
categories:  
---

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
- [STAGE algorithm](https://mail.google.com/mail/u/0/?ui=2&ik=ff424d53fe&view=att&th=15b9cbcbb9030b72&attid=0.1&disp=inline&realattid=f_j1v7nxkr0&safe=1&zw)
- [Small-world Design Space and 3D Network-on-Chip](https://arxiv.org/ftp/arxiv/papers/1608/1608.06972.pdf)
- [private link](https://mail.google.com/mail/u/0/?ui=2&ik=ff424d53fe&view=att&th=15b9b699433ae895&attid=0.1&disp=inline&realattid=f_j1uuemq40&safe=1&zw)

#### Reference 2
- [Bayes Optimisation 2016](https://bayesopt.github.io/accepted.html)
- [Gaussian Process Preference Elicitation](http://users.cecs.anu.edu.au/~sguo/gppe.pdf)
- [Machine Learning and Manycore Systems: A Serendipitous Symbiosis - Read](https://mail-attachment.googleusercontent.com/attachment/u/0/?ui=2&ik=ff424d53fe&view=att&th=15bbb8965bd15ab4&attid=0.1&disp=inline&realattid=f_iz0e9zdm0&safe=1&zw&saddbat=ANGjdJ9E8QKU9s-wFPAWNgNb1cGRVDBuswoomRVPuE4E_OiQbXaEuGFj7om3kjkZWTIIvyP9GdQXfii_aKtGryNHGZCu7bzKLDnnhmtxTV4hJJ71OVfIYSazMvIocnkU-D99kTrHWmWlf9QI340i5pQNZIU7LD30BaYe4-goS0K6Y7exbvj7kpdeTSqy4cFw2pOjhO_i3txedKt1BUuC_TgxPJ-K-XX-A1_AfOAopHhFiHB3sFQIBWie3VjALMMVcT9vUG69LJyqcBb1QQb6K0mDVtjPNTz5KJH0_whNy89W3z-_z60G1DN8uzsNJEsJwB_CCA7Xd6dr0EC6gS5c8wZKUhXmBydKbG21LFbYTCBVpH6tv0Db3LDVe6lnbhZQQOpLlOxP8hjzEQeduEUAxv1Tylp69Mz3DjjsVwLN1pY8Tr-RZQl2hwtw5CzdwPJl1XHAYKbsF8Mnit-pothCvuyNdshyUjDsad9oCIHOrmLBzjN0a87J4ijOxthG2Tn_NiFStmfYSLcPUOu3H4l3T5DTwQRUVUsESNjHhkf91Iiv6VDKxJ4l3EEeuFGuyeFsoQ9cldAFuhDmNFUvOehX1V9Ni7jFxhb27TDrdSfsT4oQqw5sBehzvIQbaq_uFTz5rMM2RP3zmnwsxwi_RQBIhttps://mail-attachment.googleusercontent.com/attachment/u/0/?ui=2&ik=ff424d53fe&view=att&th=15bbb8965bd15ab4&attid=0.1&disp=inline&realattid=f_iz0e9zdm0&safe=1&zw&saddbat=ANGjdJ9E8QKU9s-wFPAWNgNb1cGRVDBuswoomRVPuE4E_OiQbXaEuGFj7om3kjkZWTIIvyP9GdQXfii_aKtGryNHGZCu7bzKLDnnhmtxTV4hJJ71OVfIYSazMvIocnkU-D99kTrHWmWlf9QI340i5pQNZIU7LD30BaYe4-goS0K6Y7exbvj7kpdeTSqy4cFw2pOjhO_i3txedKt1BUuC_TgxPJ-K-XX-A1_AfOAopHhFiHB3sFQIBWie3VjALMMVcT9vUG69LJyqcBb1QQb6K0mDVtjPNTz5KJH0_whNy89W3z-_z60G1DN8uzsNJEsJwB_CCA7Xd6dr0EC6gS5c8wZKUhXmBydKbG21LFbYTCBVpH6tv0Db3LDVe6lnbhZQQOpLlOxP8hjzEQeduEUAxv1Tylp69Mz3DjjsVwLN1pY8Tr-RZQl2hwtw5CzdwPJl1XHAYKbsF8Mnit-pothCvuyNdshyUjDsad9oCIHOrmLBzjN0a87J4ijOxthG2Tn_NiFStmfYSLcPUOu3H4l3T5DTwQRUVUsESNjHhkf91Iiv6VDKxJ4l3EEeuFGuyeFsoQ9cldAFuhDmNFUvOehX1V9Ni7jFxhb27TDrdSfsT4oQqw5sBehzvIQbaq_uFTz5rMM2RP3zmnwsxwi_RQBI)

#### Reference 3
- [Scikit Implementation](http://scikit-learn.org/stable/modules/gaussian_process.html)
- [GraphKernals](https://github.com/eghisu/GraphKernels)
- [In-Datacenter Performance Analysis of a Tensor Processing Unit](https://arxiv.org/pdf/1704.04760.pdf)

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
