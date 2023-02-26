---
title: Recommender Systems using Nvidia Merlin
date: 2023-02-26T12:19:11.460Z
description: We're going to explore Recommender Systems using Nvidia's
  opensource framework for recsys Merlin.
image: https://avatars.githubusercontent.com/u/81591093?s=280&v=4
---


We need to install all the dependencies.

As we're going to experiment, we'll keep this build setup "big" and unoptimised.

First of all, we'll be doing CUDA computations so we're going to use anaconda for virtual development setup.

We install Pytorch with the official guidelines from [pytorch.org](pytorch.org)

```shell
conda install pytorch torchvision torchaudio pytorch-cuda=11.7 -c pytorch -c nvidia
```

O﻿nce this is done, we should proceed installing usual dev dependencies.

```shell
conda install jupyter pandas matplotlib
```

A﻿nd finally we install the Merlin library packages, with the instructions from [Nvidia Merlin Github](https://github.com/NVIDIA-Merlin/core)

```shell
conda install -c nvidia -c rapidsai -c numba -c conda-forge merlin-core python=3.7 cudatoolkit=11.2
```

Will continue afterwards