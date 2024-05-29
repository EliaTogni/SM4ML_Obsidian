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
- \[512, 256, 128\]
- \[128, 256, 512\]

Each one of these architectures iterates over a list of hidden layer units, applying batch normalization, activation function, dropout regularization, and dense (fully connected) layers sequentially. The batch normalization layer improves the training speed and stability of neural networks by normalizing the input to each layer. The activation layer applies an activation function element-wise to the output of the previous layer to introduce non-linearity to the network, allowing it to learn complex patterns and relationships in the data. The dropout layer randomly sets a fraction ($20\%$) of input units to zero during training, which helps prevent overfitting by introducing noise and reducing the interdependence of neurons.

Each network architecture has been evaluated by $5$ fold cross validation (described in details in the following section ), choosing some hyperparameter values as default.

After this step, the chosen architecture that will pass through the hyperparameters tuning phase is the $512\_156\_128$ one, due to its overall better binary accuracy, loss and Zero-One loss in comparison with the other architectures.

![[MLNNSummary.png]]

-----

# CNN
In regard to CNN, I've opted for a quite simple configuration. The Convolutional Neural Network presented follows a typical architecture for image classification tasks. It consists of three main types of layers: convolutional layers, max-pooling layers, and fully connected layers. The convolutional layers apply filters to the input image to extract feature. Each one fo the three convolutional layers has increasing numbers of filters and it is followed by a maxpooling layer, which reduces the spatial dimensions of the feature maps, retaining the most important information. The final convolutional layer is flattened to transform the $2$D feature maps into a $1$D vector, which is then fed into fully connected layers. These two layers learn to classify the extracted features into different classes, with the last layer producing a single output using a sigmoid activation function for binary classification. The purpose of this specific CNN is to serve as a comparative benchmark against the MLNN previously presented.

summary cnn

-----

# TogNet
TogNet is a Convolutional Neural Network builded and tuned for this specific task to avoid the overfitting from the previous network. To do so, the model implements dropout layers after each pooling layer and before the dense layer, which help in preventing overfitting by randomly setting a fraction of input units to $0$ during training. This approach prevents the model from relying too heavily on any single neuron.

I decided to include BatchNormalization layers after each convolutional layer to normalize the output of the previous activation layer, helping in stabilizing and accelerating the training process.

I also pplied L$2$ regularization to the convolutional and dense layers. This penalizes large weights and encourages the model to find simpler patterns, which helps reduce overfitting.

summary tognet

-----