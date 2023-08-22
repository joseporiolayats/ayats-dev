---
title: How to use CUDA with Docker in Ubuntu
date: 2023-08-22T15:20:08.946Z
description: Configure your docker app to access that juicy CUDA GPU power.
image: https://miro.medium.com/v2/resize:fit:720/format:webp/0*GGsKVOHdgXraeFbi.jpg
---
Assuming you already have your Nvidia drivers and CUDA drivers installed. 

I﻿ made a guide to help you through the process [here](https://ayats.dev/post/how-to-use-gpu-nvidia-on-ubuntu/).

## Installing CUDA with Docker on Ubuntu: A Comprehensive Guide

Docker has emerged as a powerful tool for encapsulating and deploying applications within isolated environments. When combined with CUDA, it opens the door to seamless GPU-accelerated computing for various tasks, from machine learning to scientific simulations.

In this guide, we'll walk you through the steps to set up CUDA using Docker on Ubuntu, providing a streamlined approach to harnessing the computational prowess of NVIDIA GPUs. 

Whether you're a developer, researcher, or enthusiast, this guide will equip you with the knowledge to efficiently tap into the world of GPU-accelerated computing through Docker and CUDA.

1. **I﻿nstall docker:**

   Use the package manager to install docker

   ```shell
   s﻿udo apt update
   s﻿udo apt install docker.io
   ```
2. **I﻿nstall nvidia-container-toolkit-base:**

   Use apt to install the specific package from Nvidia to handle containers

   ```shell
   sudo apt install nvidia-container-toolkit-base
   ```
3. **Generate CDI spec:**

   This should include the NVIDIA Container Toolkit CLI (nvidia-ctk) and the version can be confirmed by running:

   ```shell
   sudo nvidia-ctk cdi generate --output=/etc/cdi/nvidia.yaml
   ```
4. **Setup NVIDIA Container Toolkit:**

   Setup the package repository and the GPG key:

   ```shell
   curl -fsSL https://nvidia.github.io/libnvidia-container/gpgkey | sudo gpg --dearmor -o /usr/share/keyrings/nvidia-container-toolkit-keyring.gpg   
   curl -s -L https://nvidia.github.io/libnvidia-container/ubuntu22.04/libnvidia-container.list | sed 's#deb https://#deb [signed-by=/usr/share/keyrings/nvidia-container-toolkit-keyring.gpg] https://#g' | sudo tee /etc/apt/sources.list.d/nvidia-container-toolkit.list
   ```
5. **I﻿nstall nvidia-container-toolkit:**

     Install the `nvidia-container-toolkit package` (and dependencies) after updating the package listing:

   ```shell
   sudo apt update
   sudo apt install nvidia-container-toolkit
   ```
6. **Configure Docker to use Nvidia:**

   Configure the Docker daemon to recognize the NVIDIA Container Runtime:

   ```shell
   sudo nvidia-ctk runtime configure --runtime=docker  
   sudo systemctl restart docker
   ```
7. **Reboot now**
   ﻿  Reboot the computer
8. **Verify everything went well:**

      At this point, a working setup can be tested by running a base CUDA container:

   ```shell
   sudo docker run --rm --runtime=nvidia --gpus all nvidia/cuda:11.6.2-base-ubuntu20.04 nvidia-smi
   ```

      Which should output something like this:

   ```shell
   Unable to find image 'nvidia/cuda:11.6.2-base-ubuntu20.04' locally
   11.6.2-base-ubuntu20.04: Pulling from nvidia/cuda
   56e0351b9876: Pull complete 
   0e353182dfa4: Pull complete 
   63add13c711b: Pull complete 
   1210b79751b0: Pull complete 
   eb1e2ff09225: Pull complete 
   Digest: sha256:4b0c83c0f2e66dc97b52f28c7acf94c1461bfa746d56a6f63c0fef5035590429
   Status: Downloaded newer image for nvidia/cuda:11.6.2-base-ubuntu20.04
   Tue Aug 22 16:19:31 2023       
   +---------------------------------------------------------------------------------------+
   | NVIDIA-SMI 535.86.10              Driver Version: 535.86.10    CUDA Version: 12.2     |
   |-----------------------------------------+----------------------+----------------------+
   | GPU  Name                 Persistence-M | Bus-Id        Disp.A | Volatile Uncorr. ECC |
   | Fan  Temp   Perf          Pwr:Usage/Cap |         Memory-Usage | GPU-Util  Compute M. |
   |                                         |                      |               MIG M. |
   |=========================================+======================+======================|
   |   0  NVIDIA GeForce RTX 2070        On  | 00000000:01:00.0  On |                  N/A |
   | N/A   49C    P8              12W / 115W |    989MiB /  8192MiB |     19%      Default |
   |                                         |                      |                  N/A |
   +-----------------------------------------+----------------------+----------------------+
                                                                                            
   +---------------------------------------------------------------------------------------+
   | Processes:                                                                            |
   |  GPU   GI   CI        PID   Type   Process name                            GPU Memory |
   |        ID   ID                                                             Usage      |
   |=======================================================================================|
   +---------------------------------------------------------------------------------------+
   ```

N﻿ow you're ready to go!