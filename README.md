# Mathematical-Contest-In-Modeling
**Our paper:** [APMCM-paper.pdf](https://github.com/unicorn-yh/Mathematical-Contest-In-Modeling/blob/main/APMCM-paper.pdf)

**Problem A Selected:**  [2023 APMCM Problem A.pdf](https://github.com/unicorn-yh/Mathematical-Contest-In-Modeling/blob/main/Problem-Analysis/2023 APMCM Problem A.pdf)

<br>

***Index:***

1. [Overview](https://github.com/unicorn-yh/Mathematical-Contest-In-Modeling/tree/main#overview)
2. [Q1: Counting apples](https://github.com/unicorn-yh/Mathematical-Contest-In-Modeling/tree/main#question-1-counting-apples)
3. [Q2: Estimating the positions of apples](https://github.com/unicorn-yh/Mathematical-Contest-In-Modeling/tree/main#question-2-estimating-the-positions-of-apples)
4. [Q3: Estimating the maturity state of apples](https://github.com/unicorn-yh/Mathematical-Contest-In-Modeling/tree/main#question-3-estimating-the-maturity-of-apples)
5. [Q4: Estimating the masses of apples](https://github.com/unicorn-yh/Mathematical-Contest-In-Modeling/tree/main#question-4-estimating-the-masses-of-apples)
6. [Q5: The recognition of apples](https://github.com/unicorn-yh/Mathematical-Contest-In-Modeling/tree/main#question-5-the-recognition-of-apples)

<br>

## Overview

#### **1. Main task**

- Question 1: Counting apples <u>*[Image recognition]*</u>

- Question 2: Estimating the positions of apples <u>*[Image Segmentation + Object Localization]*</u>

- Question 3: Estimating the maturity state of apples *<u>[Feature Extraction]</u>*

- Question 4: Estimating the masses of apples <u>*[Object Area Calculation]*</u>

- Question 5: The recognition of apples <u>*[Image Classification]*</u>

#### **2. Dataset**

![image-20231207203914241](./typora/image-20231207203914241.png)

<br>

## Question 1: Counting apples

*Data used: Attachment 1*

We have designed the **Tri-Harmonize Augmentation** and **Contours Detection** to identify the count of apples. This method ensures precise apple counting by generating circles around each identified fruit, leading to an approximate of 28,073 apples detected throughout the dataset.

1. ***Tri-Harmonize Augmentation.*** We design to augment the dataset by creating new images that combine different types of noise and sharpness. This can be beneficial in training robust machine learning models, especially in image processing tasks. We blends three different versions of an image (unsharp masked, with Gaussian noise, and with salt-and-pepper noise) to create an the augmented images.

2. ***Setup and Color Range Definition.*** We define color ranges in the HSV (Hue, Saturation, Value) color space for different states of apples (ripe red, raw red, ripe yellow, raw yellow, ripe green, raw green). These color ranges are used to create masks that filter out apples based on their color and maturity state. 

3. ***Create Masks for Apple Detection.*** For each predefined apple color range, a binary mask is created. This mask highlights areas of the image that fall within the specified color range. All individual masks are combined into a single mask that represents all apples regardless of their color or maturity.

4. ***Find and Draw Contours.*** The algorithm uses combined mask to detect contours, which are essentially boundaries of apples.For each contour, we find the smallest circle that can enclose the contour, which represents an apple.If the radius of this circle is above a certain threshold (0.5 for original images, 1 for augmented images), it is counted as an apple, and the circle is drawn on the image.

5. ***Count Apples.*** The number of apples detected in each image is counted. For each apple detected in the augmented images, a dictionary with label, center point, and radius is created and added to a list.

   ![image-20231207205827870](./typora/image-20231207205827870.png)

![image-20231207205928832](./typora/image-20231207205928832.png)

![image-20231207210031880](./typora/image-20231207210031880.png)

<br>

## Question 2: Estimating the positions of apples

*Data used: Attachment 1*

**Image segmentation** techniques will isolate the apples from the background, and **object localization** methodologies will be applied to pinpoint their exact positions, culminating in a 2D scatter diagram to visually map their spatial distribution.

1. 

<br>

## Question 3: Estimating the maturity of apples

*Data used: Attachment 1*

**Bicubic interpolation** for image scaling and **GrabCut** for precise background removal are being utilized. **Feature extraction** is conducted via KMeans clustering, analyzing RGB values within central circular segments. The classification of apple maturity is then visualized in a histogram, effectively demonstrating the method's capability in discerning ripeness levels from image data.

<br>

## Question 4: Estimating the masses of apples

*Data used: Attachment 1*

We manipulate the RGB values of pixels in each image to calculate the **two-dimensional area** of the apples. This area is then adjusted according to the image's scaling ratio and multiplied by a density factor of 0.7 to estimate mass.

<br>

## Question 5: The recognition of apples 

*Data used: Attachment 2 & 3*

**Convolutional Neural Network (CNN)** is trained using a designated dataset for the task of apple recognition. This model is then applied to a separate set of images for identifying apples. Following this, a histogram is generated to visually depict the frequency of 11,241 identified apples, effectively illustrating their distribution within the dataset.
