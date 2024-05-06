# Artificial Neural Networks
## An introduction to Artificial Neural Networks
**Artificial Neural Networks** (ANNs) are a large and complex class of predictors applicable to a variety of fields, given their powerful capability in tasks like classification, regression, and sequence prediction. 

A Neural Network is usually depicted as a graph $G = \langle V , E \rangle$, where $V$ is the finite set of vertices or nodes and $E$ is the finite set of weighted edges. The vertices $v \in V$ are called **neurons** or units and the edges $e \in E$ are called **connections**.

immagine rete

Each neuron first computes the product of the weights of incoming edges with the corresponding incoming inputs and then applies an activation function over it.

immagine neurone

I will only refer to and consider **feed forward neural networks**, that is, models in which there are no loops or cycles in the graph representation of the network. The term feed forward refers to the fact that the computation can be transmitted only along the directed connections and that the output of a layer becomes the input of the following one\\cite{Kruse}.

## Multi Layer Neural Networks
The simplest form of feedforward NN is the Multi Layer Neural Network, a class of artificial neural networks characterized by their layered architecture, consisting of multiple interconnected nodes organized into three main type of layers:
- **input** layer: this type of layer is in charge of propagate the input without any change to the successive layer. The nodes in this type of layer have no incoming edges;
- **output** layer: this type of layer is in charge of returning the output of the network. The nodes in this type of layer have no outgoing edge;
- **hidden** layers: this type of layer comprises all the layers between the input one and the output one. All the nodes in this type of layer have both incoming and outgoing edges.

immagine MLLL

------------------------------------------------------------------------

# Convolutional Neural Networks
**Convolutional Neural Networks** (CNNs), as previously stated, are a particular subclass of neural networks that became popular in computer vision tasks. Here is a brief introduction describing the main components:
- **Convolutional layer**: this layer’s purpose is to extract features from the images and uses a kernel (which is a vector/matrix), called **convolutional kernel** , whose dimensions are smaller then the image’ ones. Imaging the the picture into consideration as a matrix, it starts from the top-left angle, select the image’s submatrix of kernel’s dimensions and multiplies it with the kernel itself. This procedure is repetitively applied and shifted along all the input dimensions producing a **feature map** matrix.

immagine convolutional kernel + feature map

- **Pooling layer**: as the convolutional, the pooling layer is one of the components of the networks in charge of extracting features from the image. It basically extracts a value from a submatrix/vector of the matrix/vector it takes as input: this value can be, for example, the maximum or the average one as shown in figure 4.3.

- Fully connected layers: these layers are the same previously described as multi-layered neural network.

hese networks are characterized by the convolution operation, that is performed through a kernel, which is repetitively applied and shifted along all the input dimensions, producing the so-called **feature map**. Convolutional kernels are squared matrices, generally of odd dimension, that are convoluted with a portion of the input, commonly called receptive field (term borrowed from biology, more precisely from the human visual system, from which CNNs are inspired). Since these kernels are shifted along the entire input, the presence of a certain feature will be captured no matter where it occurs in the input. For this


CNNs, as previously stated, are a particular subclass of neural networks characterized by the convolution operation. This operation is performed through a kernel, called convolutional kernel, that is repetitively applied and shifted along all the input dimensions, producing the so-called feature map. Convolutional kernels are squared matrices, generally of odd dimension, that are convoluted with a portion of the input, commonly called receptive field (term borrowed from biology, more precisely from the human visual system, from which CNNs are inspired). Since these kernels are shifted along the entire input, the presence of a certain feature will be captured no matter where it occurs in the input. For this
reason, CNNs are also known as shift invariant or space invariant artificial neural networks (SIANN). Apart from the convolution operation, CNNs are characterized by another operation called pooling. Pooling is the aggregation of features in a feature map using a certain window size juxtaposed across the entire feature map. All the data in each window are aggregated into one value, and this is tipically done to reduce the dimension of the feature maps while trying to preserve as much useful information as possible. Lowering feature maps dimension, CNNs are free to grows in depth, without much burden on the amount of computation performed in the network.

- Input layer: this layer represent the entry point of a neural network. Its shape should be equal to the shape of the inputs. In our case the shape is determined by the image size and the image channels;
- Conv2D layer: this layer applies the convolution operation, with a certain convolutional kernel, to the input of the layer. The significant arguments to provide to this layer are:
	- Filters: this argument represent the number of feature maps generated by the Conv2D layer;
	- Kernel size: in our case, the kernel size is fixed to 3 for all Conv2D layers. This choice is due to the fact that chaining subsequent 3x3 kernels can mimic any other bigger kernel, using lesser parameters. For example, consider a 5x5 kernel: it consists of 25 parameters, but we can obtain the same receptive field using two 3x3 kernels chained one after the other. Each 3x3 kernel consists of 9 parameters, using two of such kernels we have a total of 18 parameters. Thus, we bring down the number of parameters from 25 to 18.