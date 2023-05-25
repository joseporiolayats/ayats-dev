---
title: "How to Train your LLM: Deployment (7/10)"
date: 2023-05-25T22:08:13.230Z
description: Deployment is a critical phase in the software development
  lifecycle that involves releasing a solution into a live environment where it
  can be accessed and used by end-users. This article explores the significance
  of deployment and provides insights into effective deployment strategies,
  considerations, and best practices. From selecting the right deployment
  approach to ensuring scalability and monitoring, we delve into the key aspects
  of successful deployment, empowering organizations to seamlessly deliver their
  solutions to production.
image: img/eb626d49c77043feacd7d99a707cd97a.png
---
# D﻿eployment for inference

* F﻿asterTransformer and Triton server

  * H﻿ighly optimized layer between the transformer and the GPUs
  * M﻿ultiple model instances, batching, and other features
* A﻿uto-scaling infrastructure using k8s

  * U﻿nique challenges like model size and GPU requirements
  * D﻿ealing with GPU shortages in individual zones