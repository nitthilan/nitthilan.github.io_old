---
layout: post
title:  "GEM5 GPU Simulator Installation"
date:   2017-04-19 11:33:14 +0530
categories: GEM5, GPU, Installation, Simulator
---

#### Gem5 GPU Important Pages
- [GEM5 Installation](http://gem5.org/Dependencies)
- [GEM5-GPU Installation](https://gem5-gpu.cs.wisc.edu/wiki/start)
- [Version Information Excel](https://docs.google.com/spreadsheets/d/1dPpw6M7U71SIo94wOY9axlAA6FCt4_I76NW2foZsfi4/edit#gid=3)
- [Cuda 3.2 driver and toolkit](https://developer.nvidia.com/cuda-toolkit-32-downloads#MacOS)

#### Virtual Machine Setup
- Install virtual box and install ubuntu
- [ssh enabling](https://coderwall.com/p/yx23qw/access-your-virtualbox-guest-localhost-from-your-host-os)
- [enabling host access](https://emmanuelbernard.com/blog/2012/02/28/configuring-virtualbox-guests-to-access-the-internet-and-be-accessible-from-the-host/)

#### Docker Setup
- docker run -it ubuntu:14.04 /bin/bash
- sudo docker commit -m "Message" d29ef4fc461a nitthilan/ubuntu_gem5gpu
- docker cp gpucomputingsdk_3.2.16_linux.run d29ef4fc461a:/root/nitthilan
- docker checkpoint --image-dir=/Volumes/series/Docker/checkpoint --leave-running=true d29ef4fc461a
- sudo docker exec -i -t 665b4a1e17b6 /bin/bash => attaching to already running container [https://askubuntu.com/questions/505506/how-to-get-bash-or-ssh-into-a-running-container-in-background-mode]
- Things to understand:
    - docker export, docker save and docker checkpoint(experimental feature)

#### Gem5 Dependencies
- [Gem5](http://gem5.org/Dependencies)
- Installing g++ versions:
    - sudo apt-get install g++-4.7 gcc-4.7
    - sudo apt-get install g++-4.6 gcc-4.6
    - sudo apt-get install gcc-4.4 cpp-4.4 gcc-4.4 gcc-4.4-base
    - sudo update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-4.8 50
    - sudo update-alternatives --install /usr/bin/g++ g++ /usr/bin/g++-4.8 50
    - sudo update-alternatives --config gcc
    - sudo apt-get purge gcc-4.8
    - arm cross compiler:
        - sudo apt-get install gcc-4.6-arm-linux-gnueabihf-base cpp-4.6-arm-linux-gnueabihf g++-4.6-arm-linux-gnueabihf binutils-arm-linux-gnueabihf

- [Python 2.7](https://tecadmin.net/install-python-2-7-on-ubuntu-and-linuxmint/)
    - sudo apt-get install python-dev [incase only python is installed earlier out of the box]
- Scons: sudo apt-get install scons
- SWIG: sudo apt-get install swig
- zlib:
   - https://geeksww.com/tutorials/libraries/zlib/installation/installing_zlib_on_ubuntu_linux.php
   - http://www.zlib.net/
   - https://askubuntu.com/questions/660694/need-help-getting-and-intalling-zlib1g-dev-on-ubuntu-14-04-error-couldnt-find
- m4 : sudo apt-get install m4
- pydot : sudo apt-get install python-pydot
- git : sudo apt-get install git
- protobuf: https://github.com/google/protobuf/tree/master/src
    - git clone https://github.com/google/protobuf
- Installing mercurial and adding patch
    - sudo apt-get install mercurial
    - http://stackoverflow.com/questions/8360471/how-to-enable-mercurial-extensions-such-as-mq
    - http://stackoverflow.com/questions/1401803/how-do-you-set-the-username-that-mercurial-uses-for-commits/1401819

#### Installing cuda 3.2:
- https://developer.nvidia.com/cuda-toolkit-32-downloads
    - Toolkit: http://www.nvidia.com/object/thankyou.html?url=/compute/cuda/3_2_prod/toolkit/cudatoolkit_3.2.16_linux_64_ubuntu10.04.run
    - SDK path: http://developer.download.nvidia.com/compute/cuda/3_2_prod/sdk/gpucomputingsdk_3.2.16_linux.run
    - Driver [Not required]: http://developer.download.nvidia.com/compute/cuda/3_2_prod/drivers/devdriver_3.2_linux_64_260.19.26.run
- Download locally and copy to docker container [use scp]
    - Copy froom local to docker: http://stackoverflow.com/questions/22907231/copying-files-from-host-to-docker-container
export CUDAHOME=/usr/local/cuda
export PATH=$PATH:/usr/local/cuda/bin
export LD_LIBRARY_PATH=/usr/local/cuda/lib64:/usr/local/cuda/lib
- Installing SDK:
    - export NVIDIA_CUDA_SDK_LOCATION=/home/nitthilan/NVIDIA_GPU_Computing_SDK/C
    - after executing the run file go to When you have not compiled the SDK, the library might not yet have been created. To create this lib, go to path_to_sdk/NVIDIA_GPU_Computing_SDK/C/common and type "make".
    - cannot find lcutil_x86_64 error solution
    - https://devtalk.nvidia.com/default/topic/465678/-usr-bin-ld-cannot-find-lcutil_x86_64/

- Follow the steps in [https://gem5-gpu.cs.wisc.edu/wiki/start]
    - revision no. 11061

- There are two versions of gem5.opt
    - Arm variation is built into: build/VI_hammer/gem5.opt 
    - x86 variation is built into: build/X86_VI_hammer_GPU/gem5.opt
- There are two version of system simulation
    - se_fusion.py constructs a simulated system with CPU and GPU cores, and the benchmark runs on the “bare metal” simulated hardware.
        - Somehow se is not supported
    - full-system simulation, which allows for booting an operating system and running multiprocess and multithreaded workloads.
- Running Commands:
    - se_fusion does not run properly for cuda: System Emulation mode does not support many CUDA syscall functions. So does not work for both arm and x86
    - Gem5-gpu currently does not support full-system simulation for Arm ISA
    - The only mode that works is Full sytem for x86 ISA.
    - The Disk images are available at http://www.m5sim.org/dist/current/x86/x86-system.tar.bz2 [http://gem5.org/Download]
    - Untar and then rename the ./disks/xxx.img to ./disks/x86root.img.
    - Then in the common/config folder find "FSconfig.py" and modify the linux-bigswap2.img value to x86root.img at all occurance [Looks like there can be only one img file], [http://thread.gmane.org/gmane.comp.emulators.m5.users/19238]
    - Simillarly SysPaths.py modify the M5_PATH to the base folder of disk images or export the M5_PATH variable [export M5_PATH=/root/nitthilan/fullsystem_disk_images/x86/]
    - copy the backprop file into the .img and then run full system simulation
    - /build/X86_VI_hammer_GPU/gem5.opt ../gem5-gpu/configs/fs_fusion.py

- Copying and running executable within fs
    - Some probably useful youtube videos: https://www.youtube.com/watch?v=Oh3NK12fnbg, https://www.youtube.com/watch?v=OXH1oxQbuHA#t=46.908424
    - gem5 tutorial - https://www.youtube.com/watch?v=fD3hhNnfL6k

#### Errors Faced and Possible fix:
- If you get errors from that complaining that 'PROTOBUF_INLINE_NOT_IN_HEADERS' is not defined in an '#if !PRO…' expression, change the '#if !' to an '#ifndef'.
    - Open SConstruct and remove -Wall option for build
- vim build/X86_VI_hammer_GPU/gpgpu-sim/cuda-sim/instructions.cc
    - isnan to std::isnan
- vim build/X86_VI_hammer_GPU/proto/packet.pb.cc
    - 
    - Add namespace protobuf_inst_2eproto {
       void AddDescriptorsImpl();

- Not installed gpgpu-sim-complete . 
fatal: unable to connect to dev.ece.ubc.ca:
dev.ece.ubc.ca[0: 137.82.52.240]: errno=Connection refused

#### Building Benchmark examples:

- arm cross compiler for version 4.6 not available
    - version 4.6 arm cross compiler is not suported on ubuntu 14.04(trusty) and is supported only on 12.04 (precise) [http://packages.ubuntu.com/precise/devel/gcc-4.6-arm-linux-gnueabi], Also of the 4 variation of repositories [https://askubuntu.com/questions/58364/whats-the-difference-between-multiverse-universe-restricted-and-main] it is present in universe. So the repository info file /etc/apt/sources.list has to be updated by copying the universe version of trusty and replacing it with precise. Then so sudo apt-get update and then try building. It should work
- Installing SDK:
    - https://groups.google.com/forum/#!topic/gem5-gpu-dev/p9lS-bbApAk

    - Download and copy it into the ubuntu system
    - after executing the run file go to When you have not compiled the SDK, the library might not yet have been created. To create this lib, go to path_to_sdk/NVIDIA_GPU_Computing_SDK/C/common and type "make".
        - cannot find lcutil_x86_64 error solution
    - https://devtalk.nvidia.com/default/topic/465678/-usr-bin-ld-cannot-find-lcutil_x86_64/
- rm *.c_o *.cu_o gem5_fusion_backprop

#### GEM5 GPU Other links
- [mail list](https://groups.google.com/forum/#!forum/gem5-gpu-dev)
- [GEM5 GPU Simulator](https://gem5-gpu.cs.wisc.edu/wiki/Main_Page)
    - [gem5-gpu: A Heterogeneous CPU-GPU Simulator](http://research.cs.wisc.edu/multifacet/papers/cal14_gem5gpu.pdf)
    - [Sim Wiki](http://gem5.org/Main_Page)
    - [Mail list](https://groups.google.com/forum/#!forum/gem5-gpu-dev)
- [GPU Ocelot](http://gpuocelot.gatech.edu/about/)
    - [Installation](https://github.com/gtcasl/gpuocelot/wiki/Installation)
- [BARRA SIM](https://code.google.com/archive/p/barra-sim/)
- GEM5 - multicore full system simulator for CPU, ISA (Instruction System Architecture), 
- http://research.cs.wisc.edu/multifacet/papers/cal14_gem5gpu.pdf

#### To Be Deleted

#### Building RNNLIB library - Not working presently. Put on hold
- Install Boost:
    - [Install MacPorts and XCode](https://guide.macports.org/#installing.xcode)
- Install netcdf:
    - brew install homebrew/science/netcdf --with-cxx-compat
        - Installs with hdf5 compatibility
        - Installs with netcdfcpp.h header file
    - [Get the latest](http://www.unidata.ucar.edu/downloads/netcdf/index.jsp)
    - cd into the folder, ./configure, make, make install, make check
    - used ./configure --disable-netcdf-4 to remove hdf5 dependency

#### Commands
- http://gem5.org/Dependencies
- https://www.mercurial-scm.org/wiki/Download#Mac_OS_X - brew install mercurial
- https://github.com/google/protobuf/blob/master/src/README.md
- sudo brew install homebrew/dupes/m4
- 

- http://stackoverflow.com/questions/14153725/installing-gcc-4-7-1-on-os-x
- http://stackoverflow.com/questions/2477781/mercurial-abort-no-username-supplied-see-hg-help-config
- http://jamesreubenknowles.com/how-to-install-gcc-4-7-on-mac-os-x-1774
    - The below are not require. Just install gcc47
    - http://stackoverflow.com/questions/2944251/changing-default-c-compiler-in-linux-using-scons
    - http://stackoverflow.com/questions/32578106/how-to-install-python-devel-in-mac-os
- Exporting CUDA toolkit path
    - export CUDAHOME=/usr/local/cuda/
- If you get errors from that complaining that 'PROTOBUF_INLINE_NOT_IN_HEADERS' is not defined in an '#if !PRO…' expression, change the '#if !' to an '#ifndef'.
    -<http://qa.gem5.org/1545/mac-os-x-10-10-libraries-problem-dl-deprecated>
- USe this to fix _MSC_VER not defined
    - http://qa.gem5.org/1905/compiling-problem-gem5-mac-os-10-11-6-scons-build-arm-gem5-opt
- vim build/X86_VI_hammer_GPU/src/gpu/copy_engine.cc
    - ULONG_LONG_MAX = 9223372036854775807LL
- vim build/X86_VI_hammer_GPU/gpgpu-sim/cuda-sim/instructions.cc
    - isnan to std::isnan
- https://groups.google.com/forum/#!topic/gem5-gpu-dev/j_LRJNrf-Lk - Router to Router_gpgpu2