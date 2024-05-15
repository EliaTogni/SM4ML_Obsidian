binary cross-entropy is used during training to guide the optimization process, while zero-one loss is used for evaluation to assess the model's performance in terms of classification accuracy.

- **BinaryAccuracy**: this metric calculates the accuracy of the model, which is the proportion of correctly classified samples out of the total number of samples. It's calculated as (true positives + true negatives) / (true positives + true negatives + false positives + false negatives);
- **Precision**: Precision measures the proportion of true positive predictions out of all positive predictions made by the model. It's calculated as true positives / (true positives + false positives). Precision is a measure of the model's ability to avoid false positives. 
- **Recall (Sensitivity)**: Recall measures the proportion of true positive predictions out of all actual positive samples in the dataset. It's calculated as true positives / (true positives + false negatives). Recall is a measure of the model's ability to identify all positive samples;
- **AUC (Area Under the ROC Curve)**: AUC measures the area under the Receiver Operating Characteristic (ROC) curve, which plots the true positive rate (recall) against the false positive rate (FPR). AUC provides an aggregate measure of the model's performance across all possible classification thresholds. A higher AUC indicates better overall performance;
- **TruePositives**: the number of samples that are correctly classified as positive by the model;
- **TrueNegatives**: the number of samples that are correctly classified as negative by the model;
- **FalsePositives**: the number of negative samples that are incorrectly classified as positive by the model;
- **FalseNegatives**: the number of positive samples that are incorrectly classified as negative by the model.


- **Zero_One_Loss_Function**: this is a loss function rather than a metric. Zero-one loss (classification error) is a measure of misclassification rate. It calculates the proportion of misclassified samples out of the total number of samples. In binary classification, it's typically calculated as (false positives + false negatives) / (true positives + true negatives + false positives + false negatives). It's often used during evaluation rather than training


One way to discover overfitting is to plot the training and validation accuracy at each epoch during training.