---
layout: post
title:  "Artificial General Intelligence"
date:   2017-04-23 00:33:14 +0530
categories: AGI, Artificial General Intelligence, GoodAi, 
---

#### Task
- Try listing down the various modules involved in a brain - Deepmind video had a slide
- Try fitting module for each and start developing code solving the problem at hand
- 
#### Reference
- General AI challenge:
	- [GoodAi: General AI Challenge - Round 1 (gh)](https://github.com/general-ai-challenge/Round1)
		- [Specification](https://mirror.general-ai-challenge.org/challenge_first_round_specifications.pdf)
		- [](https://drive.google.com/file/d/0B820uHFOHp0mODQ3SFpzV01JTnc/view)
	- [Facebook: CommAI-env (gh)](https://github.com/facebookresearch/CommAI-env)
		- [A Roadmap towards Machine Intelligence](https://arxiv.org/abs/1511.08130)
- [General Video Game AI Competition](http://gvgai.net/index.php)
- Faster Reinforcement Learning Algorithms [Using human experience replays]:
	- [Prioritized Experience Replay](https://arxiv.org/abs/1511.05952) - framework for prioritizing experience, so as to replay important transitions more frequently, and therefore learn more efficiently
	- [Deep Exploration via Bootstrapped DQN](https://arxiv.org/abs/1602.04621)
	- [Playing Atari Games with Deep Reinforcement Learning and Human Checkpoint Replay](https://arxiv.org/abs/1607.05077)
- GoodAI:
	- [GoodAI Bibliography](https://www.goodai.com/research-inspirations)
	- [Framework for searching AGI](https://arxiv.org/pdf/1611.00685.pdf)
	- [GOOD version 1 AI AGENT DEVELOPMENT ROADMAP](https://media.wix.com/ugd/2f0a43_091d76d2b0354b0db4d88c3a57fdf76d.pdf)
- [Curriculum Learning](http://www.machinelearning.org/archive/icml2009/papers/119.pdf)
	- [Baby AI School](http://www.iro.umontreal.ca/~lisa/twiki/bin/view.cgi/Public/BabyAISchool)
    - [Deep Architectures for Baby AI](http://www.cs.toronto.edu/~amnih/cifar/talks/bengio_tutorial.pdf) - Yoshua Bengio

#### Random Tools:
- RNN - Serial processing
- Memory - To store and retrive information
- Neural Turing machine - ability to programatically access and write and learn what to store and how to process
- Progressive learning i.e. using what I learnt earlier to learn learn new things
- Teacher - Student relation to learn things better
- A evaluation metric to check whether the things has been learnt or not
- Embeddings or vector representation are the way thought are stored 
- Trigger from vectors can spark a series of outputs that is imagination
- A learning system where there is a input, there is a output
- The system feels through the input like touch, 
- The system tries to learn what it sees by mimicing the same through its output
- The evaluation system makes sure it gets a proper representation or embedding i.e. can it consistently produce the same or simillar output for a particular input
- I see a apple and hear a apple then I try recreating the apple (in my mind) aided by trying to mimic the apple by drawing or pronouncing it by mouth
- So next time I want to learn to see about apple I can either imagine it or draw it 
or when I want to learn to hear about apple I can imagine the sound of apple or pronounce it
- Then the evaluation system can say whether my imagination is right or wrong
- Different embedding mechanisms - RNN char embedding, encoder-decode for machine translation, Auto Encoders, GAN
- Why was GAN found?
- The major concepts in mind
	- Memory
		- Heirarchcal memory systems. Direct storage of data, a representation of data and information stored as linked information like a graph i.e. bility to see simillar data together and distance data further away
		- Direct storate is fast to access and give you direct answers like a hash map
		- Work like a cache store frequently accessed or nearby (spatial) correlated of accessed data
		- Slower memory go through steps to get you to the actual output. Once accessed they probably go into cache
		- Probably slower memory are embedded representation of data
	- An embedded representation of data i.e. data is continously tried to be compressed by making them embedded representation continously
		- Ability to imagine by triggering and reconstructing it by 
	- Using a teacher - student kind of approach to learn
	- Ability to extend what is learnt earlier to newer things or generalise what it learnt earlier based on what it is learning new. So how does it do it
		- reimagines the earlier task to reproduce the outputs and tries to optimise the same or a extended network 
		- Probably use the imagine i.e. using embedding to trigger expected outputs for the previously learnt tasks and generate the required supervised learning data set to optimise along with the current learning task
		- Transfer learning approaches: 
			- [PathNet](https://medium.com/@thoszymkowiak/deepmind-just-published-a-mind-blowing-paper-pathnet-f72b1ed38d46)
			- [Evolution Statergies](https://blog.openai.com/evolution-strategies/)
		- [Elastic Weight Consolidation](http://www.wired.co.uk/article/deepmind-atari-learning-sequential-memory-ewc)
	- 
#### Other research labs:
- Facebook AI Research:
	- [Blog](https://research.fb.com/)
	- [caffe2](https://caffe2.ai/blog/2017/04/18/caffe2-open-source-announcement.html)
	- [Building an effective dialog system](https://research.fb.com/the-long-game-towards-understanding-dialog/) - Looks important for involves details about AommAI Env
	- [FastText](https://github.com/facebookresearch/fastText) - Word Embeddings and Text classification - Probable use for RNN
- Deepmind:
	- [Github](https://github.com/deepmind)
	- [Blog](https://deepmind.com/)
	- [Deepmind Lab](https://deepmind.com/blog/open-sourcing-deepmind-lab/)
- OpenAi:
	- [](https://blog.openai.com/evolution-strategies/)
- [Journal of Artificial General Intelligence](https://www.degruyter.com/view/j/jagi)