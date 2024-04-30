# Data Organization
This project is based on [https://www.kaggle.com/datasets/samuelcortinhas/muffin-vs-chihuahua-image-classification](https://www.kaggle.com/datasets/samuelcortinhas/muffin-vs-chihuahua-image-classification) provided by the professor through Kaggle. This dataset is composed of two different folders for each class of images, a **training** one and a **test** one.

The training folder initially contains $2559$ chihuahua images and $2147$ muffin images, while the test one initially contains $640$ chihuahua images and $544$ muffin images.

The whole folder has a size of $510,7$ MB: the chihuahuas folder (comprising both the training and the test folders) has a size of $206,1$ MB, while the muffin one has a size of $304,3$ MB.

After a preliminary analysis, it seemed evident that the dataset was composed of images with different dimensions and weights. These differences will need to be addressed in the preprocessing phase and, for this reason, I chose not to utilize the already prepared folders but to merge the training and the test folders into one for each class, postponing the evaluation and, eventually, the resolution of the possible unbalancing of the data after the image removal step. The current folders contain $3199$ chihuahua images and $2718$ muffin images.

------------------------------------------------------------------------

# Methodology

![[Images/Preprocessing Pipeline.png]]

------------------------------------------------------------------------

# Dataset Preprocessing
## Images Removal
Given the relatively small size of the dataset, the very first preliminary operation will be a visual inpection made manually, skimming through the images in the dataset and looking for evident errors in classification, like muffin in the chihuahua folder or viceversa, or images that are not representative for our task, as they would not represents one of the two classes at all. The content of the images is various: indeed, often chihuahaus and muffins are not the main content of the image, multiple subjects (like people, present in both classes) appear in the images, a lot of details in background and around the subjects create noise and sometimes also images whose subject belongs to both classes or to neither of them appear in the datasets.

### Chihuahua dataset
After the first skimming through the chihuahua folder, it is possible to divide its content into three different subsets: 
- chihuahua images (photos or drawings);
- different breeds of dog images;
- not dog images.

The reason for this subclassification will be made clear in the following paragraph.

My first operation will be the removal of the latter subset from the folder, since it would certainly compromise the classification task. The removed images comprise muffins (wrongly labelled images), muffins and chihuahuas (images in which both classes appear together) or neither of them (totally unrelated images). Some examples (e.g., a hospitalized woman, a muffin, both chihuahuas and muffins and a wood plank) can be seen in the figure below.

0_867 hospital![[HospitalizedWoman.jpg]]

0_879 muffin![[ChihuahuaMuffin.jpg]]
0_1167 both![[BothChihuahuaMuffin.jpg]]
0_1073 log
![[ChihuahuaLog.jpg]]

The folder after the removal contains now $3161$ images of different breeds of dogs, so only $38$ images were removed.

While what the content of the images that will be fed to the NNs should be clear -  chihuahua images, of course - through the initial skimming, I noticed a huge number of different breeds of dog images and, also, of mixed breed dogs. I decided to keep all of them because, by including mixed-breed and different breed images during training, the model learns to recognize common features and patterns shared across different breeds, improving its ability to classify images accurately.

------------------------------------------------------------------------

### Muffin dataset
I followed the same line of reasoning for what concern the muffin images removal. After the first skimming through the muffin folder, I noticed that it was possible to divide its content into two different subsets:
- muffin images;
- not muffin images.

Again, I made some strong assumptions in the removal process: I considered the raw muffin batter, while it was already in the stamp, to not be a muffin yet and, therefore, I removed it from the dataset.

Consequently, all the images representing chihuahuas (wrongly labelled images), muffins and chihuahuas (images in which both classes appear together) or neither of them (totally unrelated images) have been removed. Some examples (e.g., a plant of marijuana, an ill child, the ingredients necessary to make muffins but not a fully formed muffin yet and empty muffin stamps) can be seen in the figure below.

4_756 ill child
![[img_4_756.jpg]]
4_980 marijuana
![[img_4_980.jpg]]

2_986 Ingredients
![[img_2_986.jpg]]
2_779 stamps
![[img_2_779.jpg]]

The folder after the removal contains now $2590$ images of muffins, so $128$ images were removed.

------------------------------------------------------------------------

## Unbalance Resolution
Classifiers usually assume the training data to be composed by balanced data and an equal cost of misclassification, that is, the consequences or costs associated with making a particular type of mistake in classification are the same for all classes. In other words, the classifier treats all types of errors (false positives and false negatives) equally costly\\cite{Frasca}.

Naive classifiers attempt to reduce global quantities like the error rate, thus tending to misclassify examples from the minority class. The risks of learning from an unbalanced dataset are mostly identified by the failure of generalizing inductive rules for minority class, that is, the difficulty in learning over more features but less samples and the fact that naive learners are often biased towards the majority class, and by the risk of overfitting\\cite{Frasca}.

But when a dataset is unbalanced? Assume points to be vectors $x \in \mathbb{R}^n$. It is possible to distinguish between **relative rarity** and **absolute rarity**. With the term relative rarity are identified the cases in which the minority class is outnumbered, but not necessarily rare, e.g., $10^6 \vert 10^3$. In this case, the minority class can be accurately learned. With the term absolute rarity are identified the cases in which the minority class is not just outnumbered, but also not well defined, e.g, $10^3 \vert 1$.

One common heuristic to determine if a dataset composed of two different classes is unbalanced is to calculate the class distribution or class **Imbalance Ratio**. Here's a simple heuristic:

$$ \text{Imbalance Ratio } \rho = \frac{\text{Number of instances in Majority Class}}{\text{Number of instances in Minority Class}} $$

If the Imbalance Ratio is close to $1$, the dataset is relatively balanced. If the imbalance Ratio is significantly greater than $1$, it indicates an unbalanced dataset, with the larger value representing the degree of imbalance.

Classification of degree of imbalance in data \cite {Kumar}.

| **Class Imbalance Degree** | **Proportion of Minority Class** |
| -------------------------- | -------------------------------- |
| Extreme                    | $<1\%$ of the dataset            |
| Moderate                   | $1 - 20\%$ of the dataset        |
| Mild                       | $20 - 40 \%$ of the dataset      |

Good results can be obtained, regardless of class disproportion, if both groups are well represented and come from non-overlapping distributions\\cite{Johnson}. In the considered case, the Imbalance Ratio is equal to $1,22046$ ($3161$ instances of dogs images vs $2590$ instances of muffins images), which is a score sufficiently close to $1$ to proceed without having to make any action to fix the unbalance. 

------------------------------------------------------------------------

## Image Conversion
Understanding whether color significantly influences class distinction offers insights into the model's learned features. Thus, the next preprocessing step involves converting the dataset into two distinct color schemes: RGB and Greyscale. This division aids in deciphering the CNN's decision-making process. In fact, determining the representation that yields the superior classification accuracy could provide insight about the visual cues the model relies on for predictions.

Moreover, Greyscale images may exhibit greater resilience to lighting and color variations compared to RGB counterparts. Consequently, evaluating CNN performance on both RGB and Greyscale representations would allow for a direct comparison of color's significance in the classification task.

As term of comparison, it was found a $\sim 3\%$ classification accuracy drop between Greyscale and RGB images\\cite{Shorten}.

------------------------------------------------------------------------

## Image Cropping
A recurrent characteristic of the dataset was the presence of a large white border around several images. The white border surrounding an image contains no relevant information for the classification task, therefore I trimmed the borders to help the CNN focus its attention on the essential features within the image, reducing noise and potential distractions that could hinder classification accuracy. Removing this border was made to help the model focus on the discriminative features within the image, making it more robust to variations in background and irrelevant details.

------------------------------------------------------------------------

## Image Resizing
One of the defining characteristics of Neural Networks is that they receive inputs of the same size: each neuron so all images need to be resized to a fixed dimension before inputting them to the CNN. It is possible to resize the images larger than the fixed size (in one dimension or both) down to the desired one using three possible approaches\\cite{Hashemi}:
1) further cropping their border pixels;
2) scaling the images down using interpolation;
3) zero-padding.

Cropping could cause the missing of features or patterns that appear in the peripheral areas of the image. Scaling could deforme the features or patterns across the image. However, since deforming patterns is still preferable than losing them, scaling results to be the reasonable choice to resize larger images\\cite{Hashemi}. Therefore, I decided to utilize zero-padding because it has two advantages in comparison with scaling: it does not carry the risk of deforming the patterns in the image, while scaling does, and it speeds up the calculations in comparison with scaling, resulting in better computational efficiency. The reason of this improved efficiency is that neighboring zero input units (that is, pixels) will not activate their corresponding convolutional unit in the next layer\\cite{Hashemi}.

A choice of great importance in terms of model performance is the fixed size. A size that is too large will result in high accuracy but extensive memory usage and a larger neural network. Thus, increasing both the space and time complexity. On the other hand, a size that is too small will result in a more manageable but less accurate network. It is obvious now that choosing this fixed size for images is a matter of tradeoff between computational efficiency and accuracy. The selected size for the images was $256 \times 256$.

------------------------------------------------------------------------

## Data Augmentation
One of the characteristics of these networks is that they are heavily reliant on big data to avoid overfitting. Due to the relatively small size of the dataset, I decided to rely on **Data Augmentation**, a data-space solution to this problem which encompasses a set of techniques that enhance the size and quality of training datasets such that better Deep Learning models can be built using them\\cite{Shorten}. 

To build useful models, it's essential for the validation error to continue decreasing alongside the training error, a goal achievable through Data Augmentation. The augmented data will represent a more comprehensive set of possible data points. Creating more diverse data through augmentation ensures the model to be trained on a broader range of scenarios, potentially improving its performance on unseen data.

Since the restricted dimension of the dataset, I chose to perform Data Augmentation. In fact, while many other strategies for increasing generalization performance focus on the model’s architecture itself, Data Augmentation approaches overfitting from the root of the problem, the training dataset. This is based on the assumption that it is possible to extract more information from the original dataset through augmentations. These augmentations artificially increase the training dataset size by either data warping or oversampling\\cite{Shorten}.

It is possible to distinguish different techniques for augmenting data:
1) **geometric transformations**: randomly flip, crop, rotate, stretch, and scale images. Care should be taken when applying multiple transformations on the same images, as this has the potential to reduce model performance;
2) **color space transformations**: randomly change RGB color channels, contrast, and brightness;
3) **noise Injection**: injecting a matrix of random values, usually drawn from a Gaussian distribution. Adding noise to images can help NNs learn more robust features;
4) **kernel filters**: randomly change the sharpness or blurring of the image;
5) **random erasing**: this technique was specifically designed to prevent overfitting by altering the input space and, consequently, to combat image recognition challenges due to occlusion. By removing certain input patches, the model is forced to find other descriptive characteristics;
6) **mixing images**: blending and mixing multiple images by averaging their pixel values.

The augmentations I chose to perform are described in the following sections.

Considering the safety of data augmentation is fundamental in ensuring the integrity and reliability of machine learning models. In fact, certain transformations might generate unrealistic or misleading data points, leading to erroneous model predictions.

### Geometric transformations
This family of transformations takes the image and changes it, keeping the pixel values the same. These changes have been applied not only to increase the number of training examples, but also to prevent the network from overfitting to specific features like perspective or background details that may be present in the original training data but are not relevant to the classification task. The main disadvantages of geometric transformations are the increased need of memory, the transformation costs and the higher training time.

In terms of safety of the geometric transformations, I evaluated all of the chosen augmentations to be safe and to be useful to improve the robustness of the model.

#### Flipping
This geometric transformation consists in flipping the horizonal axis.

------------------------------------------------------------------------

#### Mirroring
This geometric transformation consists in flipping the vertical axis.

------------------------------------------------------------------------

#### Rotation
Rotation augmentations are done by rotating the image right or left on an axis of a random degree.

------------------------------------------------------------------------

## Color space transformation
This family of transformations changes the pixel values, resulting in the consequential change of the colors of the pixels. Since color variations occur naturally in real-world scenarios due to factors like lighting conditions, camera settings, and environmental factors. by augmenting the dataset with color space transformations, I simulate these real-world variations, enabling the model to learn more representative features and generalize effectively. Furthermore, these changes have been applied in order to differentiate the color scheme, thus avoiding the network to learn biases over some particular palette or scheme of the image’s lighting.

Similar to geometric transformations, the main disadvantages of color space transformations are the increased need of memory, the transformation costs and the higher training time. Additionally, color transformations may discard important color information and thus are not always a label-preserving transformation.

In effect, color space transformations will eliminate color biases present in the dataset in favor of spatial characteristics but, for some tasks, color could be a fundamental distinctive feature.

#### Brightness
This color space transformation consists in the decreasing or increasing of the pixel values by a constant value. For example, when decreasing the pixel values of an image to simulate a darker environment, it may become impossible to see the objects in the image.

------------------------------------------------------------------------

#### Contrast
This color space transformation involves modifying the distribution of pixel intensities within an image to increase or decrease the difference between light and dark areas.

------------------------------------------------------------------------

#### Saturation
This color space transformation involves adjusting the intensity or purity of colors within an image while keeping the brightness and contrast levels constant.

------------------------------------------------------------------------

### Kernel filters
Kernel filters are modifications that change the pixel values, resulting in the change of the arrangement of the pixels. Filters are a very popular technique in image processing to sharpen and blur images. These filters operate by moving a matrix of size $n \times n$ across an image, applying either a box blur filter, causing the image to become blurrier, or a high-contrast vertical or horizontal edge filter, resulting in sharper edges in the image\\cite{Shorten}.

#### Unsharp masking sharpening
This kernel filter involves exploiting a method commonly known as **unsharp masking sharpening**: a Gaussian blur is applied to the dataset and  it is then subtracted from the original image, obtaining in this way an increment in terms of contrast for the smallest details. Sharpening images for Data Augmentation could result in encapsulating more details about objects of interest.

------------------------------------------------------------------------

#### Blurring
This kernel filter involves, as the name suggests, blurring the image and reducing noise, resulting in a smoothed version of the image. Intuitively, blurring images for Data Augmentation could lead to higher resistance to motion blur during testing. In my case, the blurring is obtained through a **box blur**, that is, by setting the value of each pixel to the average of the pixels in the radius of 3.

------------------------------------------------------------------------

### Image Segmentation
even if some filters, like spreading and blurring, simplify a picture giving almost only the main shape, in some cases this is not enough to exclude the features we know are completely irrelevant.

------------------------------------------------------------------------

## Image Normalization


------------------------------------------------------------------------

## Dataset Shuffling
motivazione dataset shuffling report kidara

------------------------------------------------------------------------

## Dataset Splitting
Tabella con i numeri

numero di chihuahua e numero di muffin training

numero di chihuahua e numero di muffin validation

numero di chihuahua e numero di muffin test

------------------------------------------------------------------------


