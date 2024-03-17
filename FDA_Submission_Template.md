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

**Preprocessing Steps:**

**CNN Architecture:**


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
