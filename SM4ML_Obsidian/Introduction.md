# Image Classification problem
**Image Classification** is one of the most fundamental and studied topics in the field of machine learning and it refers to the ability to understand and categorize an image as a whole under a specific label.

In Image Classification, given an input image, the goal is to predict the class which it belongs to. While this is not a big deal for humans, when it comes to mimicking perception, computer usually perform fairly poorly compared to them \cite{Kruse}. Indeed, teaching computers to see is a difficult problem that has become a broad area of research interest and both classic computer vision and \textbf{Deep Learning} techniques have been developed for decades now with this intention in mind. Classic techniques use \textbf{local descriptors} (algorithms or methods that capture information about the local appearance or features of a specific region in an image) to try to find similarities between images, but today, advances in technology allow the use of Deep Learning techniques to automatically extract representative features and patterns from each image \cite{Corominas}.

The modern techniques we are referring to are the **Convolutional Neural Networks** (henceforth CNN), a particular class of neural networks commonly used to analyze visual inputs. They are characterized by the extensive application of the convolution operation (and hence the name) to selectively extract features from small portions of the input.

Image Classification is now broadly used in lots of application fields such as medical imaging where they are used to identifying and diagnosing diseases from medical images like X-rays, or such as security and surveillance, where facial recognition, for example, could grant a higher level of security and access control.

------------------------------------------------------------------------

# Chihuahua vs Muffins classification
This report delves into the challenge of binary classification, specifically, the task of predicting two distinct outcomes. For instance, in our case, each image is categorized as either a **chihuahua** or a **muffin**. In this context, we propose a comparative analysis between the employment of Multi-Layer Neural Network and Convolutional Neural Network frameworks, with a focus on their suitability for image classification.

Our objective is not only to assess the performance disparities between these two structures but also to examine how variations in the network's hyperparameters impact overall performance.

------------------------------------------------------------------------

# Overview

riassunto di tutto

All the code is available on GitHub\footnote{\href{https://github.com/EliaTogni/Statistical-Methods-for-Machine-Learning-Project}{https://github.com/EliaTogni/Statistical-Methods-for-Machine-Learning-Project}}.