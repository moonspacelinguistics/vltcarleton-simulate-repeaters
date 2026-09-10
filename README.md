# Impact of repeat test-takers on difficulty estimates from online vocabulary testing platforms
This repo hosts the codes and data for the paper presented at Vocab-SIG 2026. This includes codes for data preprocessing pipeline for the human observations, simulation of a sparse dataframe with known parameters, and estimated word difficulty logits for 2999 words. The same set of codes and the resulting wordlist are also available at [OSF](https://osf.io/8kxuy/overview). 

## 1. Data preprocessing pipeline
The human observations were extracted from a large online database from a vocabulary testing webside [VocabLevelTest](https://vlt.carleton.ca/). In order to convert the raw files into a usable format, the files had to be filtered for invalid responses and then concatenated into a large dataframe in .csv. The codes for the preprocessing process are in RMarkdown.

## 2. Simulation of sparse dataframe with repeat test-takers
The codes in RMarkdown for simulating a sparse dataframe (~99% missingness) with known parameters and repeat test-takers making up ~30% of all observations.

## 3. Deriving L2 word difficulty indices using bigIRT package 
The bigIRT package was used to derive the word difficulty indices, and the codes are in RMarkdown.

## 4. Flemma list with Japanese EFL word difficulty indices
The list of 2999 flemma along with their difficulty estimates for L1 Japanese EFL learners are available in .xlxs format and [Google Sheets](https://docs.google.com/spreadsheets/d/1R6-LhHi5JdgMjFsqLMe_Gp9CBoKmrA_yOj7-SHZG-fM/edit?gid=0#gid=0).
