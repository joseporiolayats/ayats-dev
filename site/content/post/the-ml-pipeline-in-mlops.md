---
title: The ML Pipeline in MLOps
date: 2023-07-25T09:43:27.837Z
description: |-
  Every real-world ML system is made of 3 programs (aka pipelines):

  → Feature pipeline
  → Training pipeline
  → Inference pipeline
image: img/694996d49c6f40ad8940255caccb8ae6.png
---
Every real-world ML system is made of 3 programs (aka pipelines):\
\
→ Feature pipeline\
→ Training pipeline\
→ Inference pipeline\
\
And this is how they work ↓\
\
1️⃣ 𝗧𝗵𝗲 𝗳𝗲𝗮𝘁𝘂𝗿𝗲 𝗽𝗶𝗽𝗲𝗹𝗶𝗻𝗲 fetches raw data, from\
\
- a data warehouse\
- an external API, or\
- a website, through scrapping\
\
and generate features, aka the inputs for your ML model, and stores them in a Feature Store so that the other 2 pipelines can later use these features.\
\
2️⃣ 𝗧𝗵𝗲 𝘁𝗿𝗮𝗶𝗻𝗶𝗻𝗴 𝗽𝗶𝗽𝗲𝗹𝗶𝗻𝗲 takes the features from the store and outputs a trained ML model.\
\
These are (in general) the best models for each domain:\
\
- Tabular data → XGBoost\
- Computer Vision → Fine-tune a Convolutional Neural Net\
- NLP → Fine-tune a Transformer net.\
\
3️⃣ 𝗧𝗵𝗲 𝗶𝗻𝗳𝗲𝗿𝗲𝗻𝗰𝗲 𝗽𝗶𝗽𝗲𝗹𝗶𝗻𝗲 takes recent features and a trained model, and outputs predictions that are consumed by a downstream service or client.\
\
This pipeline can run\
- on a schedule -> batch-scoring system\
- on-demand -> online prediction, like a REST API or Stream app.