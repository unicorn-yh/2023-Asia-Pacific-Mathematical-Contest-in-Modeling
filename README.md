# Mathematical-Contest-In-Modeling
**Our paper:** [APMCM-paper.pdf](https://github.com/unicorn-yh/Mathematical-Contest-In-Modeling/blob/main/APMCM-paper.pdf)

**Problem A Selected:**  [2023 APMCM Problem A.pdf](https://github.com/unicorn-yh/Mathematical-Contest-In-Modeling/blob/main/Problem Analysis/2023 APMCM Problem A.pdf)

<br>

Index:

1. Overview
2. Q1: Counting Apple
3. Q2: Estimating the positions of apples
4. Q3: Estimating the maturity state of apples
5. Q4: Estimating the masses of apples
6. Q5: The recognition of apples

<br>

## 1. Overview

#### **1. Main task**

1. Question 1: Counting apples [Image recognition]
2. Question 2: Estimating the positions of apples [Image Segmentation + Object Localization]
3. Question 3: Estimating the maturity state of apples [Feature Extraction]
4. Question 4: Estimating the masses of apples [Object Area Calculation]
5. Question 5: The recognition of apples [Classification]

1. #### **Dataset**

   | Attachment   | Folder | Data Size | Image Size                                                   | Image                                                        | Label Format       |
   | :----------- | :----- | :-------- | :----------------------------------------------------------- | :----------------------------------------------------------- | :----------------- |
   | Attachment 1 | -      | 200       | 270 * 185                                                    |                                                              | Bounding Box       |
   | Attachment 2 | Apple  | 11144     | 270 * 180                                                    | ![img](https://aq2nilwxlpr.feishu.cn/space/api/box/stream/download/asynccode/?code=NTJhNWU2MWFjMjE5MDRjNTViZDBiODNlNmY1NTMyMWFfd0dZakZQckVhQWVmTThId01XR3FWcEFTbTg3cTFib3NfVG9rZW46WDA4eGI0MDVrb29MeWJ4N25BSGNyMlZKbmFiXzE3MDE5NTI0MjA6MTcwMTk1NjAyMF9WNA) | Classify by folder |
   | Carambola    | 2080   | 270 * 180 | ![img](https://aq2nilwxlpr.feishu.cn/space/api/box/stream/download/asynccode/?code=ZTZkZWZmZGFkMDg1M2VjN2Q3ZTY5YTU2NWFkMjRjNDhfZGtLWWRPcHdwV3N0aXBYdWFlT0YxMzRQOEdRQnA3dFlfVG9rZW46SW5UamJXc1E2b0ZJRTd4bzJ1U2NTY0tIbm5mXzE3MDE5NTI0MjE6MTcwMTk1NjAyMV9WNA) |                                                              |                    |
   | Pear         | 3012   | 270 * 180 | ![img](https://aq2nilwxlpr.feishu.cn/space/api/box/stream/download/asynccode/?code=NjViYjRjMDYxZjkwNzRiZmEwMTZlYTAwY2QyYTllMTNfeDVJRTVkZ3VxVWpwTDk1bVNiTktpT2VSb1NNQVZaQXBfVG9rZW46TjFWRWJnUGh2bzQ2STZ4c29lTmNrOFRLbmdnXzE3MDE5NTI0MjE6MTcwMTk1NjAyMV9WNA) |                                                              |                    |
   | Plum         | 2298   | 270 * 180 | ![img](https://aq2nilwxlpr.feishu.cn/space/api/box/stream/download/asynccode/?code=NzZjM2FkOTY4M2EwY2VmMWFjYzVmMmZkOTI3NDM3ZmVfSHhpM2VGc0Y1eUhGbkpCdmtHMnhiWm9mMDE3Rk9QeTBfVG9rZW46TFF4cWJRMmljb3ZvUDJ4RzBlRWNkaUZ1bmpoXzE3MDE5NTI0MjE6MTcwMTk1NjAyMV9WNA) |                                                              |                    |
   | Tomatoes     | 2171   | 270 * 180 | ![img]()                                                     |                                                              |                    |
   | Attachment 3 | -      | 20705     | 270 * 180                                                    |                                                              |                    |

1. #### **Evaluation Metrics**

   | No   | Term                 | IoU  | Definition                                                   |
   | :--- | :------------------- | :--- | :----------------------------------------------------------- |
   | 1    | True Positives (TP)  | 0.5  | Objects correctly identified by the model. The predicted bounding box matches a ground truth box with an Intersection over Union (IoU) above a certain threshold (commonly 0.5). |
   | 2    | False Positives (FP) | 0.0  | Objects incorrectly identified by the model. This includes cases where the model predicts a bounding box that either doesn't correspond to any ground truth box or has an IoU below the threshold. |
   | 3    | False Negatives (FN) | 0.0  | Objects that are present in the ground truth but missed by the model. This occurs when the model fails to detect an object that should have been detected. |

   | No   | Metrics                | Method                                          |
   | :--- | :--------------------- | :---------------------------------------------- |
   | 1    | Precision              | TP / (TP + FP)                                  |
   | 2    | Recall                 | TP / (TP + FN)                                  |
   | 3    | F1                     | (2 * Precision * Recall) / (Precision + Recall) |
   | 5    | AUC / AP               | Precision vs. Recall curve                      |
   | 6    | **mAP_val (0.5:0.95)** | Average APs across all classes                  |

1. #### Solution

   | No   | Module             | Details                                                      |
   | :--- | :----------------- | :----------------------------------------------------------- |
   | 1    | Model              | Faster R-CNN, SSD, or YOLO；DETR (attention)                 |
   | 2    | Dataset            | Annotation with bounding box [Attachment 1]                  |
   | 3    | Data Preprocessing | Resize images, Normalization, Data augmentation (rotation, scaling, flipping, super resolution) |
   | 4    | Training           | Split dataset, Loss function (cross-entropy loss, IoU-based loss) |
   | 5    | Evaluation         | Metrics (mAP, Precision, Recall, IoU), Test set              |
   | 6    | Post-Processing    | Non-Maximum Suppression (NMS): To reduce overlapping bounding boxes |

1. #### Params

1. ## Q1: Counting apples

1. Data: Attachment 1
2. Task: 
   1. Extract image features: mathematical model
   2. Count the number of apples in each image
   3. Draw a histogram of the distribution of all apples
3. Solution: 
   1. Image Segmentation: Watershed Algorithm, U-Net
   2. Object Localization: YOLO, SSD, Faster R-CNN
   3. Label: Determine the number of bounding box in ground truths as label

1. ## Q2: Estimating the positions of apples

1. Data: Attachment 1
2. Task: 
   1. Identify the position of the apples
   2. Draw a two-dimensional scatter diagram of the geometric coordinates of all apples
3. Solution: Image Segmentation, Object Localization

1. ## Q3: Estimating the maturity of apples

1. Data: Attachment 1
2. Task: 
   1. Calculate the maturity of apples in each image
   2. Draw a histogram of the maturity distribution of all apples
3. Solution: 
   1. Features extraction：color changes, distribution of spots, size, shape, uniformity (调查可用的特征提取工具)
      1. Color: Green (Low Ripeness), Yellow (Medium Ripeness), Red (High Ripeness)
   2. Classification：SVM, DT (调查可用的分类工具)
   3. Super Resolution: SRGAN

1. ## Q4: Estimating the masses of apples

1. Data: Attachment 1
2. Task: 
   1. Calculate the two-dimensional area of the apples in each image
   2. Estimate the masses of apples
   3. Draw a histogram of the mass distribution of all apples
3. Solution: Calculating the pixel area of the apples

1. ## Q5: The recognition of apples 

1. Data: Attachment 2 & 3

2. Task: 

   1. Extract image features (Attachment 2)

   2. Train an apple recognition model (Attachment 2)

   3. Identify the apples (Attachment 3)

   4. Draw a distribution histogram of the ID numbers of all apple images

      1. ```Python
         "Draw a distribution histogram of the ID numbers of all apple images" 
         means
         "create a histogram that displays the frequency distribution of ID numbers assigned to images of apples. Each bin in the histogram represents a range of ID numbers, and the height of each bin shows how many apple images fall into that range of IDs. This visualizes how the IDs are distributed across the apple images."
         ```

3. Solution:

   1. Training: Attachment 2
   2. Classification: (Attachment 3) CNN, DL
