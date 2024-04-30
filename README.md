# Statistical-Methods-for-Machine-Learning-Project

## Neural Networks
Use Keras to train a neural network for the binary classification of muffins and Chihuahuas based on images from [this dataset](https://www.kaggle.com/datasets/samuelcortinhas/muffin-vs-chihuahua-image-classification).
Images must be transformed from JPG to RGB (or grayscale) pixel values and scaled down. The student is asked to:
- experiment with different network architectures (at least 3) and training hyperparameters;
- use 5-fold cross validation to compute your risk estimates;
- thoroughly discuss the obtained results, documenting the influence of the choice of the network architecture and the tuning of the hyperparameters on the final cross-validated risk estimate.

While the training loss can be chosen freely, the reported cross-validated estimates must be computed according to the zero-one loss.
Besides complying with the project’s specifications, it is extremely important that students follow a sound methodology both in the data pre-processing phase and when running the experiments. In particular, no data manipulation should depend on test set information. Moreover, hyperparameters tuning should focus on regions of values where performance trade-offs are explicit.
