After performing our experiments, we collected all the results regarding the performances within tables and graphs.

# Comparative Analysis of Models
After performing the experiments, I collected all the results regarding the performances. In the tables below, the average values for each metric computed on the test set after I trained each model using the totality of the training set are presented for MLNN_512_256_128, for CNN_128 and for TogNet.

| MLNN 512_256_128 | Binary Cross Entropy | Binary Accuracy | Precision | Recall | AUC    |
| ---------------- | -------------------- | --------------- | --------- | ------ | ------ |
| RGB              | 0.4363               | 0.8038          | 0.7802    | 0.8008 | 0.8801 |
| RGB_Augmented    | 0.4267               | 0.8208          | 0.8906    | 0.7023 | 0.9154 |
| RGB_Segmented    | 0.3848               | 0.7535          | 0.7767    | 0.6541 | 0.8439 |

Binary accuracy is highest for the RGB_Augmented dataset, suggesting that this model is the most accurate among the three in correctly classifying images. This indicates that the RGB_Augmented model has the best overall performance in terms of correctly predicting both positive and negative classes. The higher accuracy demonstrates the model's ability to generalize well to unseen data, making fewer errors in its predictions. This improvement can be attributed to the effectiveness of data augmentation techniques, which likely provide the model with a more diverse, representative and numerous training set, leading to better generalization and accuracy.

The highest precision is, again, achieved with the RGB_Augmented dataset, indicating that the model has a high rate of correctly identified positive images among those it has classified as positive. This means that when the model predicts an image as positive, it is highly likely to be correct. In this case, the model trained with the RGB_Augmented dataset demonstrates superior performance in accurately identifying true positives, suggesting that data augmentation techniques have significantly improved its classification reliability.

==loss migliore rgb segmented ma il resto è peggio==

| CNN_128           | Binary Cross Entropy | Binary Accuracy | Precision | Recall | AUC    |
| ----------------- | -------------------- | --------------- | --------- | ------ | ------ |
| **RGB**           | 0.3517               | 0.9236          | 0.9173    | 0.9172 | 0.9648 |
| **RGB_Augmented** | 0.3626               | 0.9361          | 0.9394    | 0.9227 | 0.9660 |
| **RGB_Segmented** | 0.8976               | 0.7448          | 0.7262    | 0.7180 | 0.8238 |

CNNs have demonstrated clear superiority over MLNNs in terms of accuracy, precision, recall, and AUC. This highlights the importance of using convolutional architectures in image processing, where the ability to capture and learn local spatial features is crucial.
However, segmented images did not provide the same rich information as the other versions of the dataset, leading to a decrease in the performance of the CNN. This suggests that while segmentation can be useful for highlighting specific areas of interest, it can also remove important contextual information necessary for accurate classification.

| TogNet            | Binary Cross Entropy | Binary Accuracy | Precision | Recall | AUC    |
| ----------------- | -------------------- | --------------- | --------- | ------ | ------ |
| **RGB**           | 0.2224               | 0.9288          | 0.9245    | 0.9212 | 0.9737 |
| **RGB_Augmented** | 0.2277               | 0.9153          | 0.8940    | 0.9286 | 0.9703 |
| **RGB_Segmented** | 0.4125               | 0.8195          | 0.8092    | 0.7970 | 0.8985 |

-----

# Observations


## Missclassifications

-----

## Insights for Data Augmentation

-----

## Impact of Preprocessing Steps

-----
