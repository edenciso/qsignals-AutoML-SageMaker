# QSignals ML daily predictions with AWS SageMaker Auto-ML 
Swarmode's Qsignals are daily equities predicted trading signals.
In this experiment we are using AWS SageMaker Studio to build and run a Machine Learning model using the Auto-pilot feature to predict the number of good daily trading signals in an out-of-sample test dataset.

The ML model is trained using historical Qsignals data from 1/2/20 to 6/19/20.
The target attribute name in the train dataset for which SageMaker will make predictions is the column 'goodsignal'
Given the column values are 'y' (goodsignal) and 'n' (not good signal), we assume the Auto-pilot will suggest a Binary Classification type of problem to predict.

After running the Auto-pilot experiment, SageMaker created two Jupyter notebooks:
1. A list of ML candidates contained in the SageMakerAutopilotCandidateDefinitionNotebook
2. A Data Exploration notebook with stats on the train dataset contained in the SageMakerAutopilotDataExplorationNotebook

