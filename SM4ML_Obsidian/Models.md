In this section I present the models I developed and used in my trials to find the best architecture for the proposed task. I opted for testing and comparing a Feed Forward Neural Network built from scratch with two kind of Convolutional Neural Networks: one built starting from an existing CNN and adapting it to the assigned task, and the other one built from scratch with fewer layers and parameters.

By comparing different architectures, I aim to demonstrate the impacts of various normalization techniques like dropout on networks of different sizes. Additionally, I seek to assess whether and how performance correlates with the scale and the number of parameters of the network.

One of the fundamental modeling choices regarded the number of layers and neurons in each one of them. Here I applied a similar approach for both the MLNN and the second CNN, that is, I started from a small network composed by one layer and then I increased both the number of layers and the number of neurons. All the configurations have been tested using the preprocessed data before both the augmentation and the segmentation.

# MLNN
In regard to MLNN, I've opted to parameterize certain values to discover the optimal configuration of neuron count and layer number. This approach facilitates the exploration of the neural network's design space, aiming to identify the most fitting model for this specific classification task. I've experimented with the following sets of neurons per layer:
- \[128]
- \[256]
- \[256, 128]
- \[128, 128]
- \[256, 128, 64]
- \[128, 128, 128]

Each one of these architectures iterates over a list of hidden layer units, applying batch normalization, activation function, dropout regularization, and dense (fully connected) layers sequentially. The Batch Normalization layer improves the training speed and stability of neural networks by normalizing the input to each layer. The activation layer applies an activation function element-wise to the output of the previous layer to introduce non-linearity to the network, allowing it to learn complex patterns and relationships in the data. The Dropout layer randomly sets a fraction ($20\%$) of input units to zero during training, which helps prevent overfitting by introducing noise and reducing the interdependence of neurons.

Each network architecture has been evaluated by $5$ fold cross validation (described in details in the following section), choosing some hyperparameter values as default. The parameterized values are:

| Parameters | Optimizer | Learning rate | Dropout | Epochs |
| ---------- | --------- | ------------- | ------- | ------ |
| **Values** | ADAM      | 0.01          | 0.2     | 10     |

After this step, the chosen architecture that will pass through the hyperparameters tuning phase is the .... one. 

summary rete scelta

-----

# InceptionV3
InceptionV3 is a convolutional neural network (CNN) architecture designed for image classification and object detection tasks that was introduced by Google researchers in 2015. The hallmark of the Inception architecture is its use of inception modules, which consist of multiple parallel convolutional operations with different filter sizes. This design allows the network to capture features at various scales efficiently.
I will fine-tune InceptionV3 to adapt it to the chihuahua vs muffin specific dataset. While InceptionV3 is used in multiclass classification, this task is the theoretically simpler binary classification so, while this model will be inspired by the InceptionV3 architecture, it will also be much smaller.
The first approach we take is to use the existing model and weights by modifying only the last layer of the architecture: the softmax layer. This is a required step to adapt the output to the number of classes that our dataset has: eight. First of all, we freeze all the layers except the last one, so that the training stage does not affect the pre-trained weights of the model.

summary rete scelta

-----

# TogNet

summary rete scelta

-----
