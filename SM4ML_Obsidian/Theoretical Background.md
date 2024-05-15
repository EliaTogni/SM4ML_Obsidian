# Artificial Neural Networks
**Artificial Neural Networks** (ANNs) are a large and complex class of predictors applicable to a variety of fields, given their powerful capability in tasks like classification, regression, and sequence prediction. 

A Neural Network is usually depicted as a graph $G = \langle V , E \rangle$, where $V$ is the finite set of vertices or nodes and $E$ is the finite set of weighted edges. The vertices $v \in V$ are called **neurons** or units and the edges $e \in E$ are called **connections**.

Each neuron first computes the product of the weights of incoming edges with the corresponding incoming inputs and then applies an activation function over it.

![[NeuralNetworkNeuron.jpeg]]

I will only refer to and consider **feed forward neural networks**, that is, models in which there are no loops or cycles in the graph representation of the network. The term feed forward refers to the fact that the computation can be transmitted only along the directed connections and that the output of a layer becomes the input of the following one\\cite{Kruse}.

## Multi Layer Neural Networks
The simplest form of feedforward NN is the Multi Layer Neural Network, a class of artificial neural networks characterized by their layered architecture, consisting of multiple interconnected nodes organized into three main type of layers:
- **input** layer: this type of layer represent the entry point of a neural network. Its shape should be equal to the shape of the inputs. It is in charge of propagate the input without any change to the successive layer. The nodes in this type of layer have no incoming edges;
- **output** layer: this type of layer is in charge of returning the output of the network. The nodes in this type of layer have no outgoing edge;
- **hidden** layers: this type of layer comprises all the layers between the input one and the output one. All the nodes in this type of layer have both incoming and outgoing edges.

![[FeedForwardNeuralNetwork.png]]

------------------------------------------------------------------------

# Convolutional Neural Networks
One of the largest limitations of traditional forms of ANN is that they tend to struggle with the computational complexity required to compute image data. To choose a type of network more suited for image-focused tasks, whilst further reducing the parameters required to set up the model, **Convolutional Neural Networks** (CNNs) are the obvious choice. As previously stated, CNNs are a particular subclass of Neural Networks that became popular in computer vision tasks, such as image recognition and classification. They are inspired by the visual processing mechanism of the human brain, specifically the **receptive fields** of neurons in the visual cortex, in which a neuron is activated only by a small region of its input.

CNNs are comprised of three types of layers\\cite{Oshea}, each of which has a different role determined by its structure:
- **convolutional** layer: this type of layer is characterized by the convolution operation and its purpose is to extract features from the images. To do so, it uses a kernel (which is a squared vector/matrix typically of odd dimension), called **convolutional kernel**, which are smaller than the dimension of the initial image. To extract features, the CNN calculates the convolution between this kernel and the region covered by it. This procedure is repetitively applied and shifted along all the input dimensions and the amount of movement of the kernel is regulated by the **stride**. A CNN layer can contain multiple filters, each of which produces a different **feature map** matrix, capturing different aspects of the input. Furthermore, since these kernels are shifted along the entire input, the presence of a certain feature will be captured no matter where it occurs in the input. Each convolutional layer efficiently reduces the size of the input matrix by consolidating regions into single outputs for subsequent layers. This hierarchical stacking of convolutional layers enables the recognition of increasingly complex patterns within the image.

![[ConvolutionalKernel.png]]

- **pooling** layer: this layer is the components of the networks in charge of aggregating features in a feature map using a certain window size juxtaposed across the entire feature map. In particular, this layer is built to reduce the sensitivity of the model to the spatial location. In this way, the model will be spatially invariant, that is, it will not be sensible to the absolute position of an object in order to classify the overall image. To accomplish this, it is fundamental to focus on finding the correlation between features rather than where that exact feature is located. The pooling layer basically downsaples the feature map: it extracts a value from a submatrix/vector of the matrix/vector it takes as input: this value can be, for example, the maximum or the average one. By doing so, the layer summarize the information held by some pixels in just one. Reducing the dimension of feature maps allows CNNs to increase in depth without significantly increasing the computational load on the network;
- **dropout** layer: to avoid the problem of quickly overfitting due to the huge number of parameters in the model, one of the most used techniques is applying a dropout layer, which randomly drops out nodes (input and hidden layer) in a neural network by setting their activation to $0$. Other ways to address the issue of overfitting is adding regularization terms to the convolutional layers, in order to apply weight penalties;
- **fully connected** layer: these layers are the same previously described as Multi Layer Neural Network. Usually, the concluding segment of a CNN comprises a fully connected network. The concept is that the convolutional section of the network discerns patterns from the input and forwards them as features to a traditional network, which then undertakes a classification task based on these features.

The overall structure of a CNN can thus be divided into two major sections: the first one is designated for feature learning and extraction while the second one is employed in the classification task.

![[ConvolutionalNeuralNetworkStructure.png]]

------------------------------------------------------------------------