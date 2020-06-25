# QSignals ML daily predictions with AWS SageMaker Auto-ML 
Swarmode's Qsignals are daily equities predicted trading signals.
In this experiment we are using AWS SageMaker Studio to build and run a Machine Learning model using the Auto-pilot feature to predict the number of good daily trading signals in an out-of-sample test dataset.

The experiment has two parts:

1. Run the Auto-ML pilot to train the model and deply the prediction endpoint using historical QSignals dataset from AWS Data Exchange

The ML model is trained using historical Qsignals data from 1/2/20 to 6/19/20.
The target attribute name in the train dataset for which SageMaker will make predictions is the column 'goodsignal'
Given the column values are 'y' (goodsignal) and 'n' (not good signal), we assume the Auto-pilot will suggest a Binary Classification type of problem to predict.

After running the Auto-pilot experiment, SageMaker created two Jupyter notebooks:
* SageMakerAutopilotCandidateDefinitionNotebook: A list of ML candidates contained
* SageMakerAutopilotDataExplorationNotebook: A Data Exploration notebook with stats on the training dataset

2. Run the model with out-of-sample data to predict the number of accurately predicted QSignals

The test dataset included predicted trading signals for one day.
The code to upload the dataset, split the data, and call the prediction SageMaker endpoint is contained in the QStrades_test1 notebook.

Additionally, there's a couple of YouTube videos to demo the end-to-end experiment.

Demo Part 1: https://youtu.be/Ht1fHJL0qDw

Demo Part 2: https://youtu.be/Ln7JNw_vH4Q
