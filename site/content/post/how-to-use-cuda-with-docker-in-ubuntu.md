---
title: How to use CUDA with Docker in Ubuntu
date: 2023-08-22T15:20:08.946Z
description: Configure your docker app to access that juicy CUDA GPU power.
image: https://miro.medium.com/v2/resize:fit:720/format:webp/0*GGsKVOHdgXraeFbi.jpg
---
Assuming you already have your Nvidia drivers and CUDA drivers installed. 

I﻿ made a guide to help you through the process [here](https://ayats.dev/post/how-to-use-gpu-nvidia-on-ubuntu/).


```shell
sudo apt update
sudo apt install -y nvidia-container-toolkit-base
```