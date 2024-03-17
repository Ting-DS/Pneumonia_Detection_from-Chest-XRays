# FDA  Submission

**Your Name:** Ting Lu

**Name of your Device:** AttnPnoNet

## Algorithm Description 

### 1. General Information

**Intended Use Statement:** Assist radiological diagnosis of pneumonia

**Indications for Use:** In Screening Studies: Exclude patients unlikely to have pneumonia. In Diagnostic Studies: Deprioritize the review of predicted negative cases and assist radiologists in prioritizing cases with a high probability of pneumonia for initial review, enabling faster diagnosis and treatment for positive patients.

**Device Limitations:** The device can't replace the diagnosis decision of radiologist, only as a reference.

**Clinical Impact of Performance:** 

In non-emergency situations, it is advisable to utilize the algorithm to assist in radiological diagnosis of pneumonia.

With a specificity of 30.62%, a negative prediction (no pneumonia) is correct, while a positive prediction (pneumonia) is correct with a precision of 31.91%.

The model exhibits a high recall rate of 83.92%, accurately identifying actual positive cases (pneumonia). When the prediction result is negative, the credibility is high because the algorithm has a strong ability to identify positive patients. This high recall rate makes the predictions well-suited for aiding in screening studies and prioritizing radiologists' worklists, where reviewing predicted positive cases can be prioritized.

### 2. Algorithm Design and Function

<< Insert Algorithm Flowchart >>

**DICOM Checking Steps:**

 - is examined body part the chest area?
 - is the image scan position either posterior/anterior (PA) or anterior/posterior (AP)?
 - is the modality a digital radiography (DX)?

**Preprocessing Steps:**

 - Images are resized to 224x224 to fit the input dimension of the pre-trained VGG16 CNN model.
 - Rescaled pixel values of image by standardization (substract mean and divide by standard deviation) because VGG16 pretrained weights expect normalized data as input

**CNN Architecture:** 

We start from a classic Convolutional Neural Network (CNN) model VGG16, which has been pre-trained on a large image dataset and learned to extract features from images for classification tasks.

Then, we built a new model on top of this pre-trained VGG16 model, called the attention model. The goal of the attention model is to make the neural network focus not just on the entire image equally but selectively on important parts of the image, enabling more effective learning and feature extraction from images.

To achieve this goal, we added some special layers after the convolution and pooling layers of VGG16, including a Global Average Pooling layer (GAP). The role of global average pooling is to take the average of all pixel values in each feature map, transforming it into a fixed-length vector. This vector contains the average importance of each feature map and better reflects the importance level of different parts in an image.
By adjusting the network structure and training process, we enable this new model to automatically learn and determine which parts are crucial in an image, thereby enhancing its performance for tasks like image classification or other related tasks.

### 3. Algorithm Training

**Parameters:**
- Image augmentation during training: Rescaled 1/255, Centered & Std normalized sample-wise, Horizontal flips, Height/Width shift range 0.05, Zoom range 0.15
- Batch size:
  - Training: 64
  - Validation: 1024
  - Prediction: 64
- Optimizer learning rate: Adam 0.0001 (1e-4)
- Layers of pre-existing architecture:
  - Frozen: First 17 layers of VGG16
  - Fine-tuned: All dense layers of VGG16 and attention
- Layers added to pre-existing architecture: Batch Normalization, Conv2D, Locally Connected 2D, Conv2D, Multiply, Global Avg Pooling, Global Avg Pooling, RescaleGAP, Dropout, Dense, Dropout, Dense


<< Insert algorithm training performance visualization >> 

<< Insert P-R curve >>

**Final Threshold and Explanation:**

### 4. Databases

For EDA process, metadata for all images (Data_Entry_2017.csv) containing Image Index, Finding Labels, Follow-up #, Patient ID, Patient Age, Patient Gender, View Position, Original Image Size, and Original Image Pixel Spacing.
 (For the below, include visualizations as they are useful and relevant)
**Age and Gender:**

**View Position:**

**Comorbidies:**


**Description of Training Dataset:** The training dataset consisted of 2290 image files, with a 50/50 split of positive and negative pneumonia cases.

**Description of Validation Dataset:** The validation dataset consisted of 1430 image files, with a 20/80 split of positive and negative pneumonia cases to approach a more realistic distribution of pneumonia in the real world.


### 5. Ground Truth
Training and validation data (112,120 frontal-view chest X-ray PNG images in 1024*1024 resolution) were drawn from a comprehensive dataset curated by the NIH to address the scarcity of large X-ray datasets with accurate disease labels, vital for developing disease detection algorithms. While the original radiology reports remain inaccessible to the public, detailed information on the labeling process can be accessed at this [paper](https://arxiv.org/abs/1705.02315).

The dataset comprises 112,120 X-ray images, each annotated with disease labels, derived from 30,805 unique patients. These labels were generated through Natural Language Processing (NLP) applied to radiological reports, capturing 14 common thoracic pathologies such as Atelectasis, Consolidation, and Pneumonia. One notable limitation of this dataset is its reliance on NLP-extracted labels, which may contain errors. However, the estimated accuracy of the NLP labeling exceeds 90%.


### 6. FDA Validation Plan

**Patient Population Description for FDA Validation Dataset:**

 - Age: 0 to 100
 - Gender: Female (56%) and Male (44%)
 - Type of imaging modality: DX
 - Body part imaged: Chest

**Ground Truth Acquisition Methodology:**

The gold standard: Sputum test or Pleural fluid culture, which is expensive and time consumed.
The sliver standard: The comprehensive diagnostic results of three independent radiologists on X-ray reports.

**Algorithm Performance Standard:**

The performance of the model should be evaluated based on its F1 score compared to the silver standard. According to Rajpurkar et al. (2017), the average F1 score of radiologists is 0.387. To validate the effectiveness of this model, its F1 score should significantly exceed that of radiologists statistically.
