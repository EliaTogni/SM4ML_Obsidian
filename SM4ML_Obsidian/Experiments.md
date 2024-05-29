# Hyperparameters Tuning
A key feature of the machine learning process is the model's ability to adjust its internal parameters autonomously, based on the data it receives. During the training phase of a Neural Network, the model modifies its internal weights in response to the provided data. However, a model's effectiveness is not solely defined by these weights; it is also influenced by a set of parameters known as hyperparameters. These hyperparameters, which include the network's topology, activation functions for each layer, the number of output neurons per layer, and the optimizer guiding the training, shape the learning process without being directly modified by it.

Hyperparameters are fundamental for achieving high model accuracy. The process of selecting the optimal hyperparameters, called **hyperparameter tuning**, involves repeatedly training the model while altering these hyperparameters. The objective is to explore various combinations to identify the configuration that yields the best performance.

Different techniques have emerged to explore the hyperparameters’ combinations space. GridSearch involves exhaustively searching through a predefined set of hyperparameters, evaluating all possible combinations. While thorough, it can be computationally expensive. Random Search, on the other hand, samples hyperparameters randomly within specified ranges, often finding good combinations more efficiently than GridSearch.

However, due to the limitations of the chosen environment, which made running an algorithm like GridSearch nearly impossible, I decided to run sequentially the $5$ fold cross validation, using $15$ epochs for each training phase. For each provided value of the hyper-parameter (which can be observed in the table below ==link tabella==), I performed a $5$ fold cross validation to estimate the average performance and I saved the hyperparameter value that led to the lowest Zero-One loss. The selected values are then employed in the retraining of the model, and the result is evaluated on the test partition. This process is repeated three times using different seeds to split the dataset in order to avoid bias of a peculiar partition.

| Learning Rate | 0.001   | 0.01    | 0.1     |
| ------------- | ------- | ------- | ------- |
| **Dropout**   | **0.1** | **0.2** | **0.4** |

-----

# Nested Cross Validation
 Estimating the performance of a machine learning model accurately is crucial for ensuring its effectiveness in real-world applications. One common technique used for this purpose is **$k$-fold cross-validation**. In $k$-fold cross-validation, the dataset is divided into $k$ subsets or folds of approximately equal size. The model is then trained and evaluated $k$ times, each time using a different fold as the test set and the remaining folds as the training set. This allows the model to be tested on different portions of the data, providing a more reliable estimate of its performance.

However, when hyperparameter tuning is involved, simply using $k$-fold cross-validation may lead to overfitting to the validation set, as the hyperparameters may be selected based on their performance on this specific subset of data. This is where nested cross-validation comes into play. Nested cross-validation adds an outer loop to the process in which the dataset is still divided into $k$ folds, but each fold is used as a separate validation set exactly once. Within each iteration of the outer loop, an inner loop of $k$-fold cross-validation ($k = 5$ in our case) is performed to tune the hyperparameters of the model. The hyperparameters are selected based on their performance on the inner cross-validation loop, ensuring that they are optimized without leaking information from the test set.

By using nested cross-validation, a more unbiased estimate of the model's performance is obtained because the hyperparameters are tuned based on their performance on unseen data. Additionally, by averaging the performance metrics obtained from the outer loop across all iterations, we obtain a more reliable indication of the model's overall effectiveness. 

-----

# Performance Metrics
I selected the **Binary Cross Entropy** (or Log Loss) as the training loss function. This loss function is particularly well-suited for binary classification because it increases when the prediction diverges from the target label, penalizing incorrect predictions more heavily and therefore encouraging the model to produce probabilities closer to the true labels. Furthermore, this loss is differentiable, which facilitates efficient gradient descent optimization, leading to faster and more reliable convergence during training.

- **BinaryAccuracy**: this metric calculates the accuracy of the model, which is the proportion of correctly classified samples out of the total number of samples. It's calculated as (true positives + true negatives) / (true positives + true negatives + false positives + false negatives);
- **Precision**: Precision measures the proportion of true positive predictions out of all positive predictions made by the model. It's calculated as true positives / (true positives + false positives). Precision is a measure of the model's ability to avoid false positives;
- **Recall (Sensitivity)**: Recall measures the proportion of true positive predictions out of all actual positive samples in the dataset. It's calculated as true positives / (true positives + false negatives). Recall is a measure of the model's ability to identify all positive samples;
- **AUC (Area Under the ROC Curve)**: AUC measures the area under the Receiver Operating Characteristic (ROC) curve, which plots the true positive rate (recall) against the false positive rate (FPR). AUC provides an aggregate measure of the model's performance across all possible classification thresholds.  AUC explains how much the model can distinguish between the two classes. The higher the AUC, the better the model is at predicting the corresponding class.

For the risk estimate, instead, I employed the Zero-One loss function, which is defined as follows:

$$\ell(y, \widehat{y}) = \cases{0 \quad \text{if } y = \widehat{y} \cr \cr 1 \quad \text{otherwise}}$$

where $\widehat{y}$ is the label predicted by the model and $y$ is the target label.

I also added the **confusion matrix**, a table used to evaluate the performance of a classification model. It allows to understand the performance of the model in terms of its ability to correctly or incorrectly classify instances into their respective classes. The confusion matrix is structured in the following way:
- **True Positives (TP):** Instances that are actually positive (belong to the positive class) and are correctly classified as positive by the model;
- **True Negatives (TN):** Instances that are actually negative (belong to the negative class) and are correctly classified as negative by the model;
- **False Positives (FP):** Instances that are actually negative but are incorrectly classified as positive by the model (Type I error);
- **False Negatives (FN):** Instances that are actually positive but are incorrectly classified as negative by the model (Type II error).

-----

# General Settings 
In building our datasets, I started applying a mapping to the labels ”chihuahua” and ”muffin”, in order to better compute the error between the prediction and the actual label. Therefore, for this project ”chihuahua” was assigned the label ”0” (False), while ”muffin” the label ”1”(True). 

## MLNN
As previously specified, in my experiments, I first used 5-fold cross-validation to evaluate which MLNN architecture was the most effective in the context of this classification task.
Initially, I considered only the following architectures:
- 128
- 256
- 128, 128
- 256, 128
- 128, 128, 128
- 256, 128, 64

as I wanted to observe how different network depths would affect the outcome.
 The first choice of parameterized values used was the following:

| Parameters | Optimizer | Learning rate | Dropout | Epochs |
| ---------- | --------- | ------------- | ------- | ------ |
| **Values** | ADAM      | 0.001         | 0.2     | 10     |

However, the differences in the zero one loss and in the binary cross entropy values from one architecture to another weren't significant enough to take a decision. Therefore, I increased the number of epochs to $15$:

| Parameters | Optimizer | Learning rate | Dropout | Epochs |
| ---------- | --------- | ------------- | ------- | ------ |
| **Values** | ADAM      | 0.001         | 0.2     | 15     |

Even though the increase in the number of epochs, as shown in the histogram below, no architecture substantially outperformed the others in terms of Zero-One loss on the validation set. For this reason, I would have liked to try training the different architectures with a greater number of epochs, but I was limited by the chosen environment.

![[ZOLValZOLPerArchitecture(15Epochs).png]]

Therefore, I tested two additional architecture, as deep as the previously tested architectures but with a greater number of neurons in each layer. Furthermore, in the second new architecture, the number of neuron in the hidden layer is increasing instead of decreasing. The reasoning behind this structure is that the early layers should learn simpler and more general features and this should require less neurons. On the other hand, the deeper layers should learn more complex features, therefore requiring more neurons. The proposed new architecture are:
- 512, 256, 128
- 128, 256, 512

![[ZOLValZOLPerArchitecture2(15Epochs).png]]

Overfitting occurs when our learning algorithm fails and returns a predictor with low training error. One way to discover overfitting is to plot the training and validation accuracy at each epoch during training. During training, the model continuously learns from the training data, which may lead to increasing training accuracy. However, if the model starts to overfit, the validation accuracy may plateau or even decrease, indicating that the model is not generalizing well to new data. In contrast, if both training and validation accuracy increase together, it indicates that the model is learning the underlying patterns of the data effectively without overfitting. By comparing the trends of training and validation accuracy over epochs, it is possible to identify when overfitting begins to occur.

![[Metrics128And256.png]]

![[Metrics128_128And256_128.png]]

![[Metrics128_128_128And256_128_64.png]]

![[Metrics_128_256_512And512_256_128.png]]

After considering all of this, I have decided to choose architecture $512\_256\_128$ for the hyperparameter tuning phase because it has returned a better Zero-One loss and it also appears to be more stable than the others. The binary accuracy of the other classifiers exhibits a pattern marked by significant fluctuations over time, displaying peaks and valleys. These fluctuations suggest variations in the classifiers' performance across different epochs, indicating potential challenges in maintaining consistent predictive accuracy.

The next step is the hyperparameter tung. It is important to emphasize that this step has been done only looking at the Zero-One loss.

These are the results:

| Learning Rate \ Dropout Rate | 0.1    | 0.2    | 0.4    |
| ---------------------------- | ------ | ------ | ------ |
| 0.001                        | 0.2324 | 0.2402 | 0.2301 |
| 0.01                         | 0.2532 | 0.2274 | 0.2261 |
| 0.1                          | 0.3474 | 0.3314 | 0.4435 |

Therefore, the final settings for the MLNN are the following:

| Parameters        | Values |
| ----------------- | ------ |
| **Learning rate** | 0.01   |
| **Dropout rate**  | 0.4    |

Once the final structure (layers and neurons) and hyper parameters is defined, the networks have been evaluated using the five fold cross validation previously described. In particular, we applied the estimate over the three different configuration of the dataset.

-----

## CNN
The idea behind the choice of this baseline CNN is literally to perform a comparison between one of the simplest CNN possible with a more elaborated MLNN. Tipically, the performances of CNN outclass the performances of fully connected networks. Therefore, I started from one really simple architecture.

==spiegare procedura==

These are the results:

| Learning Rate \ Kernel Size | 3 x 3  | 5 x 5  |
| --------------------------- | ------ | ------ |
| **0.001**                   | 0.0892 | 0.1142 |
| **0.01**                    | 0.1651 | 0.1482 |
| **0.1**                     | 0.2491 | 0.2490 |

Therefore, the final settings for the MLNN are the following:

| Parameters        | Values |
| ----------------- | ------ |
| **Learning Rate** | 0.001  |
| **Kernel Size**   | 3 x 3  |

-----

TogNet
This network is an evolution of the previous one, aiming to reduce overfitting as much as possible.

I decided to set the kernel size and the learning rate, remembering the results of the previous tuning and to choose the dropout rate as parameters to tune instead.
This time I also considered the binary accuracy and loss ==oltre che la zero one loss==

| Dropout Rate \ Learning Rate | 0.001  |
| ---------------------------- | ------ |
| **0.1**                      | 0.0902 |
| **0.2**                      | 0.0873 |
| **0.4**                      | 0.0864 |
| **0.5**                      | 0.0993 |


==Grafici loss e accuracy per ogni combinazione di hyperparam==

| Parameters       | Values |
| ---------------- | ------ |
| **Dropout Rate** | 0.4    |