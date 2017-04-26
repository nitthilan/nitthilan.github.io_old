---
layout: post
title:  "Machine Learning Basics"
date:   2017-04-25 00:33:14 +0530
categories: What, How, Why, 
---

#### List of topics
- Try to understand the current understanding of Machine Learning and Artificial Intelligence in the group
- Define Machine Learning:
	- Given a set of X, Y find Y1 given a new X1 - Supervised Learning
	- Given a set of X find possible Y i.e. patterns in the Y - Unsupervised
		- Clustering
		- Auto Encoders
	- <S,A,R,S',A'> - State (Partial/Fully Observable)-Action-Reward - Reinforcement Learning
		- Board Games/Video Games
		- Self Driving Cars
- Understanding the Machine Learning Algorithm
	- [Example using Supervised Learning - Linear Regression](http://www.cs.ubc.ca/~nando/540-2013/lectures/l2.pdf)
	- [Gradient Decent/Newton's Method](http://www.cs.ubc.ca/~nando/540-2013/lectures/l10.pdf)
	- [Chapter 1 deepneural networks book](http://neuralnetworksanddeeplearning.com/chap1.html)
- General Procedure for approaching a Machine Learning Problem
	- [Kaggle Location Localisation](https://github.com/nitthilan/kaggle_location_localisation_challenge)
- Demo of Interesting applications
- Moving from tradition Data Science approach to Deep Neural Network based approaches
	- Tree based classification solutions
		- Tree Based and Random Forest Solutions
		- Average of multiple models
	- Linear Approximation:
		- Linear Regression, Linear Classification
		- Basis function based Radial Basis, Support Vector Machines
	- Classification/Clustering
		- K-Means clustering we do not know
	- Hand coded features Vs Auto matic feature generation
		- Data science and feature engineering
	- Small data size vs Huge availability of data
	- Training using huge GPU and parallel systems using generic data
	- Success of backpropagation algorithm
- How Deep Neural Networks are good at approximating data?
	- [BackPropagation](http://neuralnetworksanddeeplearning.com/chap2.html)
	- [How Neural Network approx. different fn?](http://neuralnetworksanddeeplearning.com/chap4.html)

- Type of networks: [Use ConvnetJS and Playground Demo pages] 
	- Fully Connected networks
	- Convolutional NN
	- Recursive NN
- Narrow and General Artificial Intelligence

#### Interesting Demos
- [ImageNet Identification](https://www.clarifai.com/demo)
- [Colorize Photos](http://richzhang.github.io/colorization/)
- [Automatic Caption Generation](http://www.cs.toronto.edu/~nitish/nips2014demo/index.html)
	- [Live Demo](http://deeplearning.cs.toronto.edu/i2t)
- [DQN Playing Breakout](https://www.youtube.com/watch?v=V1eYniJ0Rnk)
- [AlphGo](https://www.youtube.com/watch?v=uvtRWWzuybo)
- [Roomba - Automatice Vaccum machine](https://www.irobot.com/For-the-Home/Vacuuming/Roomba.aspx)
- [Self Driving Car](https://waymo.com/)
- [F8 conference](https://www.youtube.com/watch?v=wDTs51XLeQs)
- Echo, Google Now, Siri etc ..
- [GAN Demo](http://cs.stanford.edu/people/karpathy/gan/)

#### List of Software:
- Python (2.7 Preferable/ 3.0 should also be fine)
- Scikit Learn
- Keras
- Numpy, Mathplotlib, 

#### Good References
- Very Basic Courses:
	- [Andrew Ng Coursera](https://www.coursera.org/learn/machine-learning)
	- [Artificial Intelligence](https://www.udacity.com/course/intro-to-artificial-intelligence--cs271)
- Nando Feritas Lecture Series
	- [Oxford Lecture Series Youtube](https://www.youtube.com/playlist?list=PLE6Wd9FR--EfW8dtjAuPoTuPcqmOV53Fu)
	- [Lecture Notes](http://www.cs.ubc.ca/~nando/540-2013/lectures.html)
- [neuralnetwork and deeplearning book](http://neuralnetworksanddeeplearning.com/)
- [Kaggle competition](https://www.kaggle.com/competitions)
	- Checkout the forums of each competition to learn new approaches and methods
	- Start with the tutorial competitions
- [Scikit learn](http://scikit-learn.org/stable/)
- [Deep Learning Ian Goodfellow book](http://www.deeplearningbook.org/)
- [Google playground (tensorflow)](http://playground.tensorflow.org/)
- [ConvnetJS](http://cs.stanford.edu/people/karpathy/convnetjs/)
	- [Mnist Demo](http://cs.stanford.edu/people/karpathy/convnetjs/demo/mnist.html)