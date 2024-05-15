In this section I present the models I developed and used in my trials to find the best architecture for the proposed task. Moreover, I will choose the best model that will be deployed for the classification task. 

I opted for testing and comparing a Feed Forward Neural Network built from scratch with two kind of Convolutional Neural Networks: one built starting from an existing CNN and adapting it to the assigned task, and the other one built from scratch with fewer layers and parameters. All the configurations have been tested using the preprocessed data before both the augmentation and the segmentation.

==This will allow to show the effects of different normalization techniques such as dropout on networks of different sizes, and to compare if and how performances relate to the size and number of parameters in the network.==

One of the fundamental modeling choices regarded the number of layers and neurons in each one of them. Here I applied a similar approach for both the MLNN and the second CNN, that is, I started from a small network composed by one layer and then I increased both the number of layers and the number of neurons.

# MLNN
==Per quanto riguarda la MLNN, ho deciso di parametrizzare alcuni valori al fine di trovare la migliore configurazione di numero di neuroni e numero di layers. This should allow for exploration of the neural network's design space to find the most suitable model for the given classification task. Ho provato i seguenti insiemi di neuroni per layer:
- \[128]
- \[256]
- \[256, 128]
- \[128, 128]
- \[256, 256]
- \[256, 128, 64]

The architecture iterates over a list of hidden layer units, applying batch normalization, activation function, dropout regularization, and dense (fully connected) layers sequentially.
The Batch Normalization layer improves the training speed and stability of neural networks by normalizing the input to each layer. The activation layer applies an activation function element-wise to the output of the previous layer to introduce non-linearity to the network, allowing it to learn complex patterns and relationships in the data. The Dropout layer randomly sets a fraction ($20\%$) of input units to zero during training, which helps prevent overfitting by introducing noise and reducing the interdependence of neurons.

==I valori parametrizzati sono:==

| Parameters | Optimizer | Learning rate | Dropout | Epochs |
| ---------- | --------- | ------------- | ------- | ------ |
| **Values** | ADAM      | 0.01          | 0.1     | 10     |

==risultati==

The difference between the train and validation accuracy curves is an indicator that the model is overfitting to the training data, and thus is not able to generalize well to unseen samples (those of the test data). Moreover, the validation loss curve is unstable and not properly minimized.

Binary cross-entropy is mathematically well-suited for binary classification problems and it works well with models that use a sigmoid activation function in the output layer. it is easy to interpret. The value of binary cross-entropy loss directly reflects the model's performance on the binary classification task


# InceptionV3
 I fine-tune InceptionV3 to adapt it to our specific dataset. While InceptionV3 is used in multiclass classification, our task is the theoretically simpler binary classification, so while this model will be inspired by the InceptionV3 architecture, it will also be much smaller.
 The first approach we take is to use the existing model and weights by modifying only the last layer of the architecture: the softmax layer. This is a required step to adapt the output to the number of classes that our dataset has: eight. First of all, we freeze all the layers except the last one, so that the training stage does not affect the pre-trained weights of the model.