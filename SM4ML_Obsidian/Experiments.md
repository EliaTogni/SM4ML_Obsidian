Due to the limitation of the chosen environment, which made nearly impossible to run an algorithm like Grid Search, I chose to list the hyperparameters of interest and then apply a **Nested Cross Validation** algorithm in a sequential fashion.
# Nested Cross Validation
==Evaluating a model means assessing its performance in order to understand if it will perform well: this ”performance” of a model corresponds intuitively to the expected risk, and what we want to calculate is an estimate of this risk. This estimation can be carried out through a procedure known as $K$-fold Cross Validation.==

The algorithms takes the dataset and split it in **train** and **test** set. Then, for each provided value of the hyper-parameter, performs a **five fold cross validation** to estimate the average performance of the model. The algorithm, then, memorize the hyperparameter value that led to the lowest zero-one loss. ==The selected value is then employed in the retraining of the model, and the result is evaluated on the test partition. This process is repeated fivr times over different splits of the dataset in order to avoid bias of a ”lucky” partition. The result is an estimation of the error for each $\theta$ (if selected by the five fold cross validation as a good values for a particular split, otherwise the error estimate is $\infty$).

The internal procedure of five fold cross validation performs the training of the model five times over different splits of the dataset provided as argument. These trained models are evaluated on the current validation partition and the errors are summed together. The result is the mean of the error as an estimation of the risk of the model with that particular hyperparameter value.

==(capire dove posizionare)During training, we decided to use the Binary Cross Entropy (or Log Loss) as training loss function. This loss function increases when the prediction diverges from the target label.==

## MLNN
==La scelta dell'architettura MLNN che verrà sottoposta al tuning degli iperparametri si è basata sul valore della zero-one loss per ciascuna di esse. Per evitare che il risultato di questo valore sia compromesso da scelte infelici di partizioni, ho performato la 5 fold cross validation 5 volte per ogni architettura. I risultati sono osservabili nel grafico sottostante.==

grafico

==Come già anticipato nella sezione precedente, l'architettura scelta per il tuning degli iperparametri è l'architettura ...== Recalling that the strategy for the hyperparameter tuning is conditioned by the Colab limitations, I started from the basic setting and I applied the Nested Cross Validation on the parameters sequentially, using 10 epochs for each training phase. We also highlight the fact that the hyperparameter tuning has been done only looking at the Zero-One loss. Here are shown the results:

-----

## InceptionV3

-----

## TogNet


-----

# Hyperparameters Tuning
A key feature of the machine learning process is the model's ability to adjust its internal parameters autonomously, based on the data it receives. During the training phase of a Neural Network, the model modifies its internal weights in response to the provided data. However, a model's effectiveness is not solely defined by these weights; it is also influenced by a set of parameters known as hyperparameters. These hyperparameters, which include the network's topology, activation functions for each layer, the number of output neurons per layer, and the optimizer guiding the training, shape the learning process without being directly modified by it.

Hyperparameters are fundamental for achieving high model accuracy. The process of selecting the optimal hyperparameters, called **hyperparameter tuning**, involves repeatedly training the model while altering these hyperparameters. The objective is to explore various combinations to identify the configuration that yields the best performance.

==Once the hyper-parameters have been defined, we proceeded with the choice of the tuning
technique: there are several algorithms to fulfill this task but, again, here we got the limitation of our environment which made us nearly impossible to run an algorithm like Grid Search. We preferred to rank our hyper parameters and then apply a Nested Cross Validation algorithm sequentially.==

==Different techniques have emerged to explore the hyperparameters’ combinations space, the most naive being GridSearch: the whole search space is divided in discretized sets of values which the hyperparametrs are allowed to take, and the model is tested on these values only, provid1ing a sort of sampling of the search space. A variant for GridSearch is RandomSearch, where instead of a regular grid over the hyperparameters, a random extraction is done each time. Both of these techniques often prove unhelpful due to the sheer size of the hyperparameters space: a model with only two hyperparameters, each of which may assume 4 different values, will need 4 × 4 = 16 runs to cover the whole search space, and adding another hyperparameter again with 4 values brings the amount
of required runs to 64; this without considering parameters that may assume continuous values, as opposed to discrete ones==

-----

# General Settings 

\[[0.18922705314009663, 0.23652173913043475], [0.15038647342995168, 0.2088888888888889], [0.031207729468599045, 0.10376811594202898], [0.04275362318840579, 0.12193236714975844], [0.06265700483091788, 0.13217391304347828], [0.07019323671497583, 0.15845410628019324]]

binary cross-entropy is used during training to guide the optimization process, while zero-one loss is used for evaluation to assess the model's performance in terms of classification accuracy.

- **BinaryAccuracy**: this metric calculates the accuracy of the model, which is the proportion of correctly classified samples out of the total number of samples. It's calculated as (true positives + true negatives) / (true positives + true negatives + false positives + false negatives);
- **TruePositives**: the number of samples that are correctly classified as positive by the model;
- **TrueNegatives**: the number of samples that are correctly classified as negative by the model;
- **FalsePositives**: the number of negative samples that are incorrectly classified as positive by the model;
- **FalseNegatives**: the number of positive samples that are incorrectly classified as negative by the model;
- **Precision**: Precision measures the proportion of true positive predictions out of all positive predictions made by the model. It's calculated as true positives / (true positives + false positives). Precision is a measure of the model's ability to avoid false positives;
- **Recall (Sensitivity)**: Recall measures the proportion of true positive predictions out of all actual positive samples in the dataset. It's calculated as true positives / (true positives + false negatives). Recall is a measure of the model's ability to identify all positive samples;
- **AUC (Area Under the ROC Curve)**: AUC measures the area under the Receiver Operating Characteristic (ROC) curve, which plots the true positive rate (recall) against the false positive rate (FPR). AUC provides an aggregate measure of the model's performance across all possible classification thresholds.  AUC explains how much the model can distinguish between the two classes. The higher the AUC, the better the model is at predicting the corresponding class.


One way to discover overfitting is to plot the training and validation accuracy at each epoch during training.