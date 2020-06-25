# QSignals ML daily predictions with AWS SageMaker Auto-ML 
Swarmode's Qsignals are daily predicted trading signals for US equities.
In this experiment we are using AWS SageMaker Studio to build and run a Machine Learning model using the Auto-pilot feature to predict the number of good daily trading signals in an out-of-sample test dataset.

The experiment has two parts:

1. Run the Auto-ML pilot job to train the model using an historical QSignals dataset from AWS Data Exchange, and deploy the model to a prediction SageMaker endpoint.

The ML model is trained using historical Qsignals data from 1/2/20 to 6/19/20. A train dataset sample is included in the Data Exploration notebook.
The target attribute name in the train dataset for which SageMaker will make predictions is the column 'goodsignal'. Based on the dataset features, we expect the Auto-ML determine the best ML pipeline and algorithms to predict how many daily Qsignals are good to trade.
Given the column values are 'y' (goodsignal) and 'n' (not good signal), is expected the Auto-pilot job will suggest a Binary Classification type of problem to predict.

After running the Auto-pilot experiment, SageMaker created two Jupyter notebooks:
* SageMakerAutopilotCandidateDefinitionNotebook: A list of ML candidates contained
* SageMakerAutopilotDataExplorationNotebook: A Data Exploration notebook with stats on the training dataset

As expected, after completing the Auto-ML job, SageMaker defined the problem as Binary Classification to maximize the Accuracy quality metric of the trained model. In this case, the Accuracy metric will provide the percentage of times the model predicted the correct class, which is 'y' values in the 'goodsignal' target column.
After the Auto-ML pilot job has analyzed the training dataset, SageMaker is building the pipeline with 10 ML models and two algorithms: Xgboost and Linear-learner.
The job takes aproximately 30 mins to complete all three stages: analyzing data, feature engineering, and model tunning so we can chose the best tuning job and deploy the model to the SageMaker endpoint.

2. Run the model with out-of-sample data to predict the number of accurately predicted QSignals

The test dataset included predicted trading signals for one day.
The code to upload the dataset, split the data, and call the prediction SageMaker endpoint is contained in the QStrades_test1 notebook.

Additionally, there's a couple of YouTube videos to demo the end-to-end experiment.

Demo Part 1: https://youtu.be/Ht1fHJL0qDw

Demo Part 2: https://youtu.be/Ln7JNw_vH4Q

# Results:
This are the out-of-sample observed results after calling the model endpoint with the test dataset with 2192 Qsignals.

Confusion Matrix

182  0

0  372 <- true positives, or number of good Qsignals predicted for the day

Accuracy = 1.0 or 100%

