---
title: "How to Train your LLM: Pipeline (3/10)"
date: 2023-05-29T22:29:27.588Z
description: The pipeline plays a fundamental role in the workflow of LLM
  development and deployment. In this section, we delve into the concept of the
  LLM pipeline and its significance in the end-to-end process. From data
  collection and preprocessing to model training and evaluation, each step in
  the pipeline contributes to the overall performance and effectiveness of the
  language model. We explore the key components and stages of the LLM pipeline,
  highlighting the importance of a well-designed and optimized pipeline for
  building robust and reliable language models.
image: img/6d708ef2d8e34b2badfe798a32b0c710.png
---
H﻿ow to define the right training pipeline?

* The stack on HuggingFace

  * L﻿arge corpus of permissively licensed code
  * D﻿e-duped dataset available in parquet format
* P﻿rocessing in Databricks

  * R﻿un all of our processing and transformations in Databricks
  * A﻿llows increased control compared to Transformers library
  * M﻿akes it easier to introduce addictional data sources
* I﻿ncluding propiertary data not on HF
* P﻿reprocessing and transformations run in distributed fashion
* T﻿ractable and extensible process

  * L﻿ots of work done in notebooks