# QSignals ML daily predictions with AWS SageMaker Auto-ML 
Swarmode's [Qsignals](https://www.swarmode.ai/products/qsignals/) are daily predicted trading signals for US equities.
In this experiment we are using AWS SageMaker Studio to build and run a Machine Learning model using the Auto-pilot feature to predict the number of good daily trading signals in an out-of-sample test dataset.

The experiment has two parts:

1. Run the Auto-ML pilot job to train the model using the QSignals historical dataset in [AWS Data Exchange](https://aws.amazon.com/marketplace/pp/prodview-ausl6zaqiknve?ref_=srh_res_product_title), and deploy the model to a prediction SageMaker endpoint.

The ML model is trained using historical Qsignals data from 1/2/20 to 6/19/20. A train dataset sample is included in the Data Exploration notebook.
The target attribute name in the train dataset for which SageMaker will make predictions is the column 'goodsignal'. Based on the dataset features, we expect the Auto-ML determine the best ML pipeline and algorithms to predict how many daily Qsignals are good to trade.
Given the column values are binary: 'y' (goodsignal) and 'n' (not good signal), it is expected SageMaker will suggest a Binary Classification type of problem to model.

After running the Auto-ML pilot experiment, SageMaker created two Jupyter notebooks:
* SageMakerAutopilotCandidateDefinitionNotebook: A list of ML pipeline candidates, algorithms, hyperparameter tuning, model selection and deployent.
* SageMakerAutopilotDataExplorationNotebook: contains dataset analysis, data split in training amnd validation, column analysis, and descriptive statistics.

As expected, after completing the Auto-ML job, SageMaker defined the problem as Binary Classification to maximize the Accuracy quality metric of the trained model. In this case, the Accuracy metric will provide the percentage of times the model predicted the correct class, which is 'y' values in the 'goodsignal' target column.
After the Auto-ML pilot job has analyzed the training dataset, SageMaker is building the pipeline with 10 ML models and two algorithms: Xgboost and Linear-learner.
The job takes aproximately 30 mins to complete all three stages: analyzing data, feature engineering, and model tunning so we can chose the best tuning job and deploy the model to the SageMaker endpoint.

2. Run the model with out-of-sample data to predict the number of accurately predicted QSignals

The test dataset included predicted trading signals for one day.
The Python code to upload the dataset, execute the SageMaker client and call the prediction SageMaker endpoint is contained in the QStrades_test1 Jupyter notebook.

Additionally, there's a couple of YouTube videos to demo the end-to-end experiment.

Demo Part 1: https://youtu.be/Ht1fHJL0qDw

Demo Part 2: https://youtu.be/Ln7JNw_vH4Q

# Results
These are the observed out-of-sample test results after calling the model endpoint with a 2,192 Qsignals dataset.

Confusion Matrix

1820 | 0

0 | 372 <- true positives, or number of good Qsignals predicted for the day

Classification Accuracy = 1.0

