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
 - Rescaled images by standardization (substract mean and divide by standard deviation) because VGG16 pretrained weights expect normalized data as input

**CNN Architecture:** 
We start from a classic Convolutional Neural Network (CNN) model VGG16, which has been pre-trained on a large image dataset and learned to extract features from images for classification tasks.

Then, we built a new model on top of this pre-trained VGG16 model, called the attention model. The goal of the attention model is to make the neural network focus not just on the entire image equally but selectively on important parts of the image, enabling more effective learning and feature extraction from images.

To achieve this goal, we added some special layers after the convolution and pooling layers of VGG16, including a Global Average Pooling layer (GAP). The role of global average pooling is to take the average of all pixel values in each feature map, transforming it into a fixed-length vector. This vector contains the average importance of each feature map and better reflects the importance level of different parts in an image.
By adjusting the network structure and training process, we enable this new model to automatically learn and determine which parts are crucial in an image, thereby enhancing its performance for tasks like image classification or other related tasks.

### 3. Algorithm Training

**Parameters:**
* Types of augmentation used during training
* Batch size
* Optimizer learning rate
* Layers of pre-existing architecture that were frozen
* Layers of pre-existing architecture that were fine-tuned
* Layers added to pre-existing architecture

<< Insert algorithm training performance visualization >> 

<< Insert P-R curve >>

**Final Threshold and Explanation:**

### 4. Databases
 (For the below, include visualizations as they are useful and relevant)

**Description of Training Dataset:** 


**Description of Validation Dataset:** 


### 5. Ground Truth



### 6. FDA Validation Plan

**Patient Population Description for FDA Validation Dataset:**

**Ground Truth Acquisition Methodology:**

**Algorithm Performance Standard:**
