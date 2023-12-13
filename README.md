# spotting-violence-in-news-nlp
This project uses a simple NLP, supervised learning pipeline to identify several types of violence reports in news items.

The Jupyter code [https://github.com/hannesfelixs/potting-violence-in-news-nlp/ml_classifier_for_github.ipynb](https://github.com/hannesfelix/spotting-violence-in-news-nlp/blob/main/ml_classifier_for_github.ipynb) provides insights into the machine learning part of the article "How Big is the Media Multiplier? Evidence from Dyadic News Data" forthcoming in the Review of Economics and Statistics by Tim Besley, Thiemo Fetzer and Hannes Mueller. Please cite the paper if you use the code.

The code is designed to classify news articles based on violent content, focusing on Israel, Morocco, Tunisia, Turkey, and Egypt. The pipeline includes data preprocessing, model training, and out-of-sample testing with a case study on Sri Lanka. This overview serves as a guide through the various components of the code.

### Imports and Setup:
In this section we set up the needed packages and functions used for pre-processing and visualizing performance.

### Loading Data and Data Preprocessing:
We clean the text data and pre-process it minimally tokenizing and lowercasing. Importantly we exclude articles in which our destination countries condemn violence elsewhere as this would lead to measurement error in the output data. Part of pre-processing is to add the title tokens four times to the text tokens when producing the document term matrix for supervised learning. This idea is taken from the pipeline in Cage et al (2019) The Production of Information in an Online World.

### Apply Dictionary Method:
Dictionary methods are standard in economics. We apply different variants of dictionaries and their interactions pick the best performing one to compare to the performance of the supervised machine learning pipeline.

### Model Training: 
Training of 3 classifiers for 3 labels. This is the longest part of the code. We conduct crossval grid searches for all 9 classifiers. We then build one ensemble classifier for each label by doing a simple average across the random forest, naive Bayes, and XGB classifier. For label_2 we train the entire pipeline, build the ensemble check the output, and relabel manually as we realize some of the manual labeling is wrong. This makes the code somewhat cumbersome.

### Application of Classifiers to Larger Corpus:
We have trained three ensemble classifiers on all available training labels. We now use the trained classifiers out-of-sample on our corpus of over 500,000 news articles. The result is 9 continuous scores (three for each label) which we carry to the post-processing. As in the pipeline, we take the average of the three classifiers to produce a score in post-processing.

### Out-of-Sample Testing (Sri Lanka Case Study):
Given the supervised learning set-up here, we do not expect the trained algorithm to detect violence against tourists well in other countries. If we were to train a generalizing algorithm we would, for example, filter out country- and location-specific vocabulary first. A simple Tf-idf at the country level would be an attractive and simple way to do this. 

However, it is interesting to see whether our ensembles generalize somewhat. Sri Lanka is a good country to check our algorithm because it is far away from the training sample and had a vicious, out-of-the-blue, terror attack on tourists in April 2019. The pipeline below applies our three classifiers to news text from Sri Lanka. The average ensemble score for each month is shown in the paper. The algorithm picks up the attack remarkably well with scores shooting up in the month of the attack and then decreasing again as the discussion of the attack declines again. 

Questions and suggestions please to h.mueller.uni@gmail.com


A version of the paper is also uploaded to the repository. It contains a detailed description of the pipeline and the following code in appendix E. The latest version of the paper can be downloaded from Hannes Mueller's webpage here: https://www.hannesfelixmueller.com/projects/terror-and-tourism-the-economic-consequences-of-media-coverage
