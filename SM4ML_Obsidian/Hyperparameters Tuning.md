the main hyper-parameters we wanted to make the tuning of and the tuning methods.

Once the hyper-parameters have been defined, we proceeded with the choice of the tuning
technique: there are several algorithms to fulfill this task but, again, here we got the limitation of our environment which made us nearly impossible to run an algorithm like Grid Search. We preferred to rank our hyper parameters and then apply a Nested Cross Validation algorithm sequentially.

# Nested Cross Validation

The algorithms described above is the one actually implemented in our work: it takes the
dataset and split it in train and test set, then, for each provided value of the hyper-parameter, performs a five fold cross validation thus to estimate the average performance and saves the hyper parameter value that led to the lowest 0-1 loss. The selected value is then employed in the retraining of the model, and the result is evaluated on the test partition. This process is repeated three times over different splits of the dataset in order to avoid bias of a ”lucky” partition. The result is an estimation of the error for each theta (if selected by the five fold cross validation as a good values for a particular split, otherwise the error estimate is ∞).

The internal procedure of five fold cross validation performs the training of the model five times over different splits of the dataset provided as argument. These trained models are evaluated on the current validation partition and the errors are summed together. The result is the mean of the error as an estimation of the risk of the model with that particular hyper-parameter value


# MLNN
We recall the strategy for the hyper parameter tuning is conditioned by the Colab limitations, thus we started from the basic setting found in section 4.2 and we applied the nested cross validation on the parameters sequentially, using 10 epochs for each training phase. We also highlight the fact that the hyper parameter tuning has been done only looking at the 0-1 loss. Here are shown the results: