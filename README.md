# spotting-violence-in-news-nlp
This project uses a simple NLP supervised learning pipeline to identify several types of violence reports in news items.

The jupyter code https://github.com/hannesfelix/spotting-violence-in-news-nlp/ml_classifier_for_github.ipynb provides insights into the machine learning part of the article "How Big is the Media Multiplier? Evidence from Dyadic News Data" forthcoming in the Review of Economics and Statistics by Tim Besley, Thiemo Fetzer and Hannes Mueller. Please cite the paper if you use the code.

The code is designed to classify news articles based on violent content, focusing on Israel, Morocco, Tunisia, Turkey, and Egypt. The pipeline includes data preprocessing, model training, and out-of-sample testing with a case study on Sri Lanka. This overview serves as a guide through the various components of the code.

### Imports and Setup:
In this section we set up the needed packages and functions used for pre-processing and visualizing performance.
### Loading Data and Data Preprocessing:
We clean the text data. Importantly we exclude articles in which our destination countries condemn violence elsewhere as this would lead to measurement error in the output data.
### Apply Dictionary Method:
Dictionary methods are standard in economics. We apply different variants of dictionary methods and pick the best performing one to compare to the performance of the supervised machine learning pipeline.
### Model Training: 
Training of 3 classifiers for 3 labels. This is the longest part of the code. We conduct crossval gridsearches for all 9 classifiers. We then build one ensemble classifier for each label by doing simple average across the random forest, naive bayes and xgb classifier. For label_2 we train the entire pipeline, build the ensemble check the output and relabel manually as we realize some of the manual labeling is wrong. This makes the code somewhat cumbersome.
### Application of classifiers to larger corpus:
We have trained three ensemble classifiers on all available training labels. We now use the trained classifiers out-of-sample on over 500,000 article in our news corpus.
### Out-of-Sample Testing (Sri Lanka Case Study):


A version of the paper is also uploaded to the repository. It contains a detailed description of the pipeline and following code in appendix E. The latest version of the paper can be downloaded from Hannes Mueller's webpage here: https://www.hannesfelixmueller.com/projects/terror-and-tourism-the-economic-consequences-of-media-coverage
