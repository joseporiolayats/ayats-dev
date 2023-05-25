---
title: How to train your LLM (part 1)
date: 2023-05-26T19:07:27.883Z
description: In the first part of this guide, we'll focus on the essential step
  of preprocessing your data for training a Language Learning Model (LLM) in
  Python. Preprocessing involves transforming raw text data into a suitable
  format, including cleaning, tokenization, normalization, and feature
  extraction. Follow along as we explore practical techniques to prepare your
  data effectively for LLM training, setting the foundation for subsequent parts
  of the series.
---
* D﻿ownloading the dataset 
* M﻿erging all the datasets
* A﻿nonymize the data by removing emails, IP addresses, secret keys
* R﻿emove auto-generated code

  * D﻿etected using standard regex and other heuristics
* R﻿emove code that doesn't compile or is not parseable

  * O﻿nly possible for a subset of languages
* F﻿ilters based on average line length, maximum line length, pct alphanumeric chars
* M﻿etrics of quality (number of gh issues, stars, etc) for removing bugs