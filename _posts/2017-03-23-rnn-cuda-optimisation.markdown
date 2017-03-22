---
layout: post
title:  "RNN Cuda Optimisation "
date:   2017-03-23 00:33:14 +0530
categories: Notes, RNN, CUDA, OPTIMISATION
---

### RNN

- [Awesome rnn resource](https://github.com/kjw0612/awesome-rnn)
- [LSTM TUT](http://lstm.iupr.com/home)
- [RNN From Scratch](https://github.com/pangolulu/rnn-from-scratch)
- [RNN Effectiveness]( http://karpathy.github.io/2015/05/21/rnn-effectiveness/)
- WILDML Tutorials : [Part1](http://www.wildml.com/2015/09/recurrent-neural-networks-tutorial-part-1-introduction-to-rnns/), [Part2](http://www.wildml.com/2015/09/recurrent-neural-networks-tutorial-part-2-implementing-a-language-model-rnn-with-python-numpy-and-theano/)

### CUDA

#### Simulator

- [GEM5 GPU Simulator](https://gem5-gpu.cs.wisc.edu/wiki/Main_Page)
    - [gem5-gpu: A Heterogeneous CPU-GPU Simulator](http://research.cs.wisc.edu/multifacet/papers/cal14_gem5gpu.pdf)
    - [Sim Wiki](http://gem5.org/Main_Page)
    - [Mail list](https://groups.google.com/forum/#!forum/gem5-gpu-dev)
- [GPU Ocelot](http://gpuocelot.gatech.edu/about/)
    - [Installation](https://github.com/gtcasl/gpuocelot/wiki/Installation)
- [BARRA SIM](https://code.google.com/archive/p/barra-sim/)

#### Libraries

- [RNNLIB C++](https://sourceforge.net/projects/rnnl/)
- [RNNLM C++](https://github.com/yandex/faster-rnnlm)
- [CuBLAS](http://moss.csc.ncsu.edu/~mueller/cluster/nvidia/0.8/NVIDIA_CUBLAS_Library_0.8.pdf)
- [ConvNet](http://conv-net.sourceforge.net/doc/)
- OCR Implementation:
    - Looks like old implementation but could be a good reference
    - [CLSTM](https://github.com/tmbdev/clstm)
    - [OCROPUS](https://github.com/tmbdev/ocropy)

#### 3D GPU Architectures
- [Hybrid Network-on-Chip Architectures for Accelerating Deep Learning Kernels on Heterogeneous Manycore Platforms ](http://www.ece.cmu.edu/news/story/2016/09/PID4360211.pdf)
- [Design-Space Exploration and Optimization of an Energy-Efficient and Reliable 3D Small-world Network-on-Chip](https://arxiv.org/ftp/arxiv/papers/1608/1608.06972.pdf)
- [Optimizing Structured Spaces via Expensive Experiments: Algorithms and Application to Manycore Systems Design - private link](https://mail-attachment.googleusercontent.com/attachment/u/0/?ui=2&ik=ff424d53fe&view=att&th=15abad78c436112a&attid=0.1&disp=inline&realattid=f_j04j9d2i0&safe=1&zw&saddbat=ANGjdJ9wi1VFVQBXh8iLQmPIHLMiviQCxhIYGQ6_pOs4Bbrw3atjOhgnxB8OjyR5Rrob0hFTl1ojPM2P-VPl6P0SQLbbb0Z6rhVqXMHD7ErgptOexFOlCsr5V5Qd5JKWkdye16lWLoU5sLptHlQxjCRjqLMIORNxd0YkR0ZZVUAOh46FtOggGjWeBTTkSfvAWs8rE6W4yMbmLAD4RCpfm-IuSjhnqm4q6KUbTkqwrV3zmg0bfjp5Z-pUMF84pZNzaZtk8K_-AAScE5DBaND2lRS2JW9GSjq7oh6XAvnOO9dIyQCIXZn4R8gEXrKlWOkctFd_IRGByJkOKyFJs4yQI2QxDKfuKGOry5K31QehaUh-lXFqEwgiJETQpsf6sv_HcsS46ZGaixeTSOgdFi26Zv3LOj-h7dKXpu0ybPZdbXj3pgG2kZKWboBdh1pdXuBdO06frbZ9rkMbUlkXQt_h0MWndldq5qwhYGrVhmal__USDKZL0SoO2vq-rPgOopF-T12WBJADtzdko_xlHtz9Hrd78wtMb8eck4GzxfFldnE-Utxn3r07ySxWJfbeN_pyvFOCb0L3yMq_wH42_9qUA61xlqkvqUuMG76h0zNisdzsb_EOvLdfM3hXtYZMFHOvE3qylWnyC3U315logFnl-X0zN4DJom-mCAS065Ndsg)

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

#### Things to learn

- Understand coding in Cuda, CuBLAS implementation, 
