# Interesting Questions and Observations
The process of visual inspection has involved some more or less debatable decision-making choices, as already anticipated. To assess the quality of these choices, an analysis will be conducted using GradCAM on a subset of the dataset composed of peculiar images.

- dogs and cakes
- dog not chihuahuas
- chihuahua and muffins
- chihuahua with foam
- ...
# Results
The results obtained by our analysis can be considered as preliminary: indeed, the multi-layered neural network and the convolutional neural network performances looks promising with respect to the 0-1 loss and the accuracy for both the original and augmented dataset, but, in order to have more accurate results, it is necessary to execute the models with more computational power, which would allow to have more experiments and a better tuning approach, increasing the number of epochs and the number/size of the layers, which is not possible in the Google Colab environment. Concerning our results, they showed that it is possible to obtain good results (besides the overfitting) in the binary classification task with the convolutional neural network, while the multi-layered network showed poor results.
The segmentation task, whose objective was to delete non relevant details, showed better results in the MLNN, making the images too simple for the convolutional.
The best dataset seemed to be the augmented one that in both network allowed a better
understanding of the data, introducing ”good noise” making the network learning true relevant features. This dataset has been also useful in order to reduce the overfitting in each tested architecture.