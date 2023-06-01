# spotting-violence-in-news-nlp
This project uses a simple NLP supervised learning pipeline to identify several types of violence reports in news items.

The jupyter code https://github.com/hannesfelix/spotting-violence-in-news-nlp/blob/main/ml_classifier_vs_2022_11.ipynb provides insights into the machine learning part of the article "How Big is the Media Multiplier? Evidence from Dyadic News Data" by Tim Besley, Thiemo Fetzer and Hannes Mueller. Please cite the paper if you use the code.

The structure of the code is as follows: 
1. The first cell loads packages and defines functions.
2. The second cell pre-processes the one part of the text data using these functions and the third cell pre-processes another part of the data (the data cannot be shared due to copyright restrictions)
3. The code then first proposes a dictionary method for identifying harm of tourists and fatal violence. Performance statistics here can be calculated easily with the existing labels.
4. The code then goes through a supervised learning method in which cross-validation is used to search for optimal hyperparameters and then performance measures are produced. This is implemented for three labels (label_0 is violence, label_1 is fatal violence, label_2 is tourist harm) and three models per label. 
5. One complication here is that we check labels for label_2 for those articles that produce very high fitted values in the cross-fitting. We do this because this is an extremely unbalanced class and it is therefore crucial to get the labels right as much as possible. The label_2 models are then retrained with the same hyperparameters.
6. Finally the code uses the model with the best hyperparameters and applies this to the unlabeled and labelled data.

A version of the paper is also uploaded to the repository. It contains a detailed description of the pipeline and following code in appendix E. The latest version of the paper can be downloaded from Hannes Mueller's webpage here: https://www.hannesfelixmueller.com/projects/terror-and-tourism-the-economic-consequences-of-media-coverage
