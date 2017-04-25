---
layout: post
title:  "RNN LM Implementation "
date:   2017-04-12 00:33:14 +0530
categories: Notes, RNN, CUDA, OPTIMISATION
---

#### Things to do
- Implement a rnn library on the simulator
    - Assuming only a simple rnn is required
    - No LSTM or GRU
    - Functionality is just language modelling i.e. predicting the next word given the previous set of words


#### Understanding Rnn
- [Awesome rnn resource](https://github.com/kjw0612/awesome-rnn)
- RNN theory:
    - [RNN From Scratch](https://github.com/pangolulu/rnn-from-scratch)
    - [RNN Effectiveness](http://karpathy.github.io/2015/05/21/rnn-effectiveness/)
    - WILDML Tutorials : [Part1](http://www.wildml.com/2015/09/recurrent-neural-networks-tutorial-part-1-introduction-to-rnns/), [Part2](http://www.wildml.com/2015/09/recurrent-neural-networks-tutorial-part-2-implementing-a-language-model-rnn-with-python-numpy-and-theano/)
- Simple RNN Implementation for Language Modeling
    - Libraries:
        - [RNNLM C++ Base Code](http://www.fit.vutbr.cz/~imikolov/rnnlm/)
        - [Faster RNNLM C++](https://github.com/yandex/faster-rnnlm)
        - [RNNLIB C++](https://sourceforge.net/projects/rnnl/) - Not used
    - Understanding RNN:
        - [RNNLM - Recurrent Neural Network Language Modeling Toolkit](http://www.fit.vutbr.cz/~imikolov/rnnlm/rnnlm-demo.pdf) - Understanding codebase
        - [Understaning BPTT](https://pdfs.semanticscholar.org/4b7a/0ba426690b08489a86038db161846ffcfaa9.pdf)
        - [Extensions of recurrent neural network language model](https://github.com/yihui-he/Natural-Language-Process/blob/master/Extensions%20of%20recurrent%20neural%20network%20language%20model.pdf) - Understanding Class based optimisation
            - Reduces the 
        - Direct Connection - Tries to use the last word value to estimate the next word directly if the word is pretty frequent usng a direct connection threshold
        - [Faster Recurrent Neural Network Language Modeling Toolkit-Youtube](https://www.youtube.com/watch?v=GRpIy33yFZE)
            - Language Model - LM - assigning probablity to a list of word or a sentence
            - Motly used in Spell correction, Machine transalation after a lattice tool i.e. getting the probably phrases from a speech to text engine etc
    - Understanding Language Modeling:
        - [Word Embedding](http://sebastianruder.com/word-embeddings-1/index.html)
        - [SoftMax Optimisations](http://sebastianruder.com/word-embeddings-softmax/)
        - [Preplexity](https://en.wikipedia.org/wiki/Perplexity) - A low perplexity indicates the probability distribution is good at predicting the sample.
        - Softmax Optimisation:
            - Class based softmax (O(sqrt(V)/h))
            - Heirarchical Softmax log2(V)*h - faster-rnnlm
            - Noise Contrative Estimation (O(kh)) k~20
        - Hierarchical SoftMax - [Youtube video](https://www.youtube.com/watch?v=B95LTf2rVWM)[Quora Post](https://www.quora.com/What-is-hierarchical-softmax) of the same
            - Though HS gives gain for training (since we calculate only logN calculations) it does not help in actual prediction since all the N words probability has to be calculated
        - Noise Contrastive Estimation (Not fully understood)
            - [Tutorial](https://gt-deepnet.limsi.fr/lib/exe/fetch.php?media=matthieulabeaunce_16_10_2014.pdf)
            - [Notes on Noise Contrastive Estimation and Negative Sampling](https://arxiv.org/pdf/1410.8251.pdf)
            - [Emperical Distribution](http://math.stackexchange.com/questions/74394/what-does-an-empirical-distribution-represent)
            - [Unigram Language Model](http://stackoverflow.com/questions/16225667/what-is-word-count-in-unigram-language-model)

    - Pitfalls:
        - http://stackoverflow.com/questions/10327939/error-no-such-instruction-while-assembling-project-on-mac-os-x

- Things to understand:
    - Evaluations done by n-best list reordering, Maximum Entropy model
    - direct_size, class_size, vocab_size, bptt_block, anti_k, Dioganal Initialisation, RMSProp, Lock Free Multithreading, GRU and its variations, SCRN (Structurally Constrained Recurrent Network)
    - http://www.fit.vutbr.cz/~imikolov/rnnlm/google.pdf - To be read
    - http://www.speech.sri.com/projects/srilm/download.html
    - http://www.speech.sri.com/projects/srilm/papers/asru2011-srilm.pdf
    - http://www.cs.brandeis.edu/~cs114/CS114_docs/SRILM_Tutorial_20080512.pdf

#### Understanding Cuda and BLAS
- [Basic Linear Algebra Subprogram](https://en.wikipedia.org/wiki/Basic_Linear_Algebra_Subprograms)
    - Three levels. (1) takes linear time (2) takes quadratic (3) takes cubic time
    - Level 1: Basic vector operations y <- ax+y
    - Level 2: Matrix Vector Multiplication y <- alpha * A * x + beta*y
    - Level 3: Matrix Matirx operations C <- alpha*A*B + beta*C
- [BLAS Documentation](http://www.netlib.org/blas/#_documentation)
- Blas libraries:
    - [Intel Math Kernal Lib](https://software.intel.com/en-us/mkl-reference-manual-for-c-pdf)
    - [Netlib](http://netlib.org/blas/)
    - [OpenBLAS](http://www.openblas.net/)
- [CUDA C Programming Guide](http://docs.nvidia.com/cuda/cuda-c-programming-guide/index.html#hardware-implementation)
- [CUDA C Programming Tutorial](http://www.nvidia.com/docs/IO/116711/sc11-cuda-c-basics.pdf)
- [CUDA C Best Practices](http://docs.nvidia.com/cuda/cuda-c-best-practices-guide/index.html#axzz4dstT0MHa)

#### 3D GPU Architectures (Hetrogeneous Processor Architectures)
- [On-Chip Communication Network for Efficient Training of Deep Convolutional Networks on Heterogeneous Manycore Systems](https://mail-attachment.googleusercontent.com/attachment/u/0/?ui=2&ik=ff424d53fe&view=att&th=15b1052fda7a1f8c&attid=0.1&disp=inline&realattid=794149265f706335_0.1&safe=1&zw&sadnir=1&saddbat=ANGjdJ_dehdOnTqsRk4F5EiJxrX6wjjm0s5TFbL8YyMNPKATnGtOHEHhz4DJZQNSCG4THeIr2v_ya2htTh8lC1y8nZ7hn6AMFCjM7wsZD2Tf04KeQzp4k70yg11-TAgTP0Vm66CPN59ZRzaYw06GXx6BCvQ653NOWsicm8Kfi0yB1cW8hM3jIT67AUfu7SYL6Ml_lTJoW3P26MusweuoZn6Ff5mMjFFSA3zOVLc9oMQTIgTrJf5TPu0gLEmUNlOvUhVo15Gbl8YuH6kt7aHWDlw58K30ghkauZeR8iD_it0js6whJmCDQd8_1Uvnwf_tiM-1fMpoRVR7WAw6CWULzWqSRTQLH-PpHPqhuUjPdj-6jJLtNoIHhQS_cTogiZHcIdK_FJkeWr5LUyEyjLvxuZuiCRBVlv7fT2SqtPSUuBNPMsBVv9vCN7-7FGCw7RR7WsJkLl_WXWYgMAK-Vhx37DB8jEE4VmQ0GZBhN-bhMQLmpdJ9bbDssFBr2Fno3MNxxn2B64SwDtbMqB23EdqZuIct0SpWBAIzbkDBAiAvh8HXDVfHvs8ukL7Xx8Usm_Pw2R-mJKL1TcwNWUmkRrWcyB3igBCUlKHuQAkQLLRXmo0wk3x5X4y18d_IQdWvYkHdDZb3dEfsUENYVdxFIj0gmLTxaA-Cuud3fLkYkTScLQ) 
    - Good paper to understand the NoC and Simulator charateristics and the problem boundary
- [Hybrid Network-on-Chip Architectures for Accelerating Deep Learning Kernels on Heterogeneous Manycore Platforms ](http://www.ece.cmu.edu/news/story/2016/09/PID4360211.pdf)
- [Design-Space Exploration and Optimization of an Energy-Efficient and Reliable 3D Small-world Network-on-Chip](https://arxiv.org/ftp/arxiv/papers/1608/1608.06972.pdf)
- [private link](https://mail-attachment.googleusercontent.com/attachment/u/0/?ui=2&ik=ff424d53fe&view=att&th=15abad78c436112a&attid=0.1&disp=inline&realattid=f_j04j9d2i0&safe=1&zw&saddbat=ANGjdJ9wi1VFVQBXh8iLQmPIHLMiviQCxhIYGQ6_pOs4Bbrw3atjOhgnxB8OjyR5Rrob0hFTl1ojPM2P-VPl6P0SQLbbb0Z6rhVqXMHD7ErgptOexFOlCsr5V5Qd5JKWkdye16lWLoU5sLptHlQxjCRjqLMIORNxd0YkR0ZZVUAOh46FtOggGjWeBTTkSfvAWs8rE6W4yMbmLAD4RCpfm-IuSjhnqm4q6KUbTkqwrV3zmg0bfjp5Z-pUMF84pZNzaZtk8K_-AAScE5DBaND2lRS2JW9GSjq7oh6XAvnOO9dIyQCIXZn4R8gEXrKlWOkctFd_IRGByJkOKyFJs4yQI2QxDKfuKGOry5K31QehaUh-lXFqEwgiJETQpsf6sv_HcsS46ZGaixeTSOgdFi26Zv3LOj-h7dKXpu0ybPZdbXj3pgG2kZKWboBdh1pdXuBdO06frbZ9rkMbUlkXQt_h0MWndldq5qwhYGrVhmal__USDKZL0SoO2vq-rPgOopF-T12WBJADtzdko_xlHtz9Hrd78wtMb8eck4GzxfFldnE-Utxn3r07ySxWJfbeN_pyvFOCb0L3yMq_wH42_9qUA61xlqkvqUuMG76h0zNisdzsb_EOvLdfM3hXtYZMFHOvE3qylWnyC3U315logFnl-X0zN4DJom-mCAS065Ndsg)


#### Not used reference
- [LSTM TUT](http://lstm.iupr.com/home)
- [CuBLAS](http://moss.csc.ncsu.edu/~mueller/cluster/nvidia/0.8/NVIDIA_CUBLAS_Library_0.8.pdf)
- [ConvNet](http://conv-net.sourceforge.net/doc/)
- OCR Implementation:
    - Looks like old implementation but could be a good reference
    - [CLSTM](https://github.com/tmbdev/clstm)
    - [OCROPUS](https://github.com/tmbdev/ocropy)

#### Optimisation suggestions
- [NVIDIA RNN optimisation - To be read](https://devblogs.nvidia.com/parallelforall/optimizing-recurrent-neural-networks-cudnn-5/)
- [Optimizing RNN performance - to be read](https://svail.github.io/rnn_perf/)
- [LSTM theory Nvidia](https://devblogs.nvidia.com/parallelforall/deep-learning-nutshell-sequence-learning/)
- cuBLAS - Basic Linear Algebra Subprograms:
    - [](https://solarianprogrammer.com/2012/05/31/matrix-multiplication-cuda-cublas-curand-thrust/)
        - [CUDA by Example: An Introduction to General-Purpose GPU Programming](https://www.amazon.com/exec/obidos/ASIN/0131387685/solarianprogr-20/)
        - [Thrust - easier interface for STL using CUDA](http://thrust.github.io/)
    - [GEneral Matrix to Matrix Multiplication - GEMM](https://petewarden.com/2015/04/20/why-gemm-is-at-the-heart-of-deep-learning/)
        - [cuDNN: Efficient Primitives for Deep Learning ](https://arxiv.org/pdf/1410.0759.pdf) - I think it is CNN so may not be useful
        - []()
#### Understanding GEM5 GPU Simulator
