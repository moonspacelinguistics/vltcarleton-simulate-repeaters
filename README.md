# Impact of repeat test-takers on difficulty estimates from online vocabulary testing platforms
This repo hosts the codes and data for the paper presented at Vocab-SIG 2026. This includes codes for data preprocessing pipeline for the human observations, simulation for a sparse dataframe with repeat test-takers, and estimated word difficulty logits to 2999 words. The same information is also available at [OSF](https://osf.io/8kxuy/overview). 

## 1. Data preprocessing pipeline
The human observations were extracted from a large online database from a vocabulary testing webside [VocabLevelTest](https://vlt.carleton.ca/). In order to convert the raw files into a usable format, the files had to be filtered for invalid responses and then concatenated into a large dataframe in .csv. The codes for the preprocessing process were written in R.

## 2. Simulation of sparse dataframe with repeat test-takers
The codes for simulating a sparse dataframe (~99% missingness) with known parameters and repeat test-takers that make up ~30% of all observations. 

## 3. L2 learner indices of word difficulty
As with any online databases, the data matrix was very sparsely populated (>90% missingness). To derive word difficulty estimates from human responses, IRT modelling was used to obtain the estimates. The codes were written in R and RMarkdown.
