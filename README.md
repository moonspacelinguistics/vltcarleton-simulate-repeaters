# Using machine learning techniques to solve data sparsity issues for deriving L2 word learnability estimates
This repo hosts all the codes and data for my dissertation, including codes for data preprocessing pipeline for the human observations, word difficulty logit estimation, neural network model, and analyses outcome. This will also be linked to OSF once the project is complete. 
## 1. Data preprocessing pipeline
The human observations are extracted from a large online database from a vocabulary testing webside (https://vlt.carleton.ca/). In order to convert the raw files into a usable format, the files have to be filtered for invalid responses and then concatenated into a large dataframe in .csv. The codes for preprocessing is written in R and RMarkdown.
## 2. L2 learner indices of word difficulty
As with any online databases, the data matrix tends to be very sparsely populated (>50% missingness). To derive word difficulty estimates from human responses, IRT modelling is used to obtain the estimates. The codes are written in R and RMarkdown.
## 3. Neural network 
The model is a simple supervised neural network that is written in base Python without packages. Since machine learning techniques tend to function as "blackboxes" aimed at prediction, the goal here is to produce a model that is as interpretable as possible. Thus, the input patterns are the GloVe word embeddings (which uses weighted least squares regression to derive word vectors that capture a word's global co-occurence likelihood), and the teaching pattern are the word difficulty bands extracted from the human observations. 
## 4. Results & analyses
The machine learning outcomes, training and cross-validation pipelines, as well as the final results are presented using data visualisation. Both Python and R are used for this purpose.
