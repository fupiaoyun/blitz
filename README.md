[![Build Status](https://travis-ci.org/PAA-NCIC/blitz.svg?branch=master)](https://travis-ci.org/PAA-NCIC/blitz)

# Blitz

*Blitz* is a cross platform library for deep learning computations. It aims to provide simple, portable, and efficient interfaces for neural network developers. Unlike deep learning frameworks such as *Caffe*, *Torch*, and *Tensorflow*, it could be quickly deployed on different platforms separately. And thus users could fast instanitiate and extend neural network computations with high performance.

## Requirements

#### Common

- linux systems
- boost
- glog

#### CPU backend

- x86-64 processors
- g++/icc
- openblas/atlas/mkl

#### GPU backend

- NVIDIA GPUs

#### Whole networks (only for testing)

- yaml-cpp

## Features

#### CPU backend

For convolution networks, we support *NCHW* and *NHWC* data layouts for the convolution and pooling computations in forward, backward and update phases. Besides, we devise a feature for automatic data transformation. It is designed for tunning the performance on the network level. For instance, if some layers performs well on *NCHW* layouts while others are best for *NHWC* layouts, we could specify the output formats of the convolution layer. The internal transformation does not require extra copies. 

#### GPU backend (not stable)

Our GPU backend supports *NCHW*, *NHWC*, and *CHWN* data layouts. Currently we use *CUBLAS* for the first two layouts, and the *CHWN* layouts is fir for our assembly implementations on Kepler GPU, which outperforms *CUDNN*'s GEMM algorithm in several configurations.

## Interfaces

A convenient feature of blitz is that CPU, GPU and MIC share common interfaces. We use a contiguous tensor to manage data on different devices, and a template to instanitiate algorithms. A more compherensive guide is presented as following.

- [Convolution](https://github.com/PAA-NCIC/blitz/blob/master/doc/convolution.md)

## Build

#### CPU backend


    make AVX=0/1/2/3 BLAS=openblas/atlas/mkl


#### GPU backend

    make USE_GPU=1 CUDA_ARCH=<according to specific GPU generation>


#### MIC backend

    make AVX=512

