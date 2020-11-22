# AI for Medicine - Course 1: AI for Medical Diagnosis

## Week 1: Disease detection with computer vision

### Introduction 
In the first course, you learn about building machine learning models for diagnosis. You will also covered deep learning tools for medical image interpretation. 

Diagnosis means, the process of determining which disease or condition explains the person's symptoms, signs, and medical results. 

In particular, you will:
- Data preparation: Pre-process (visualisation) and prepare a real-world X-ray dataset (data leakage prevention)
- Model Development: Use Transfer Learning to retrain a DenseNet model for X-ray image classfication
- Weighted Loss: Learn a technique to handle Class Imbalance.
- Evaluation: Measure diagnostic performace by computing the AUC (Area Under the Curve)* for the ROC (Receiver Operating Characteristic) curve
- Visualise model activity using GradCAMs

### Application of computer vision to mdeical diagnosis 

#### Medical Image Diagnosis
Examples of Medical image diagnosis used in this course:
- Dermatology (the branch of medicine dealing with the skin) and skin cancer detection
- Ophthalmology (the diagnosis and treatment of eye disorders)
<p align="center"><img width="50%" src="./images/eye.png"></p>

- Histopathology, a medical specialty involving examination of tissues under the microscope.

<p> </p>
<b>Example 1:</b>
<p> </p>
Dermatology is the branch of medicine dealing with the skin and skin cancer detection. One of the task dermatologists perform is to look at a suspicious region of the skin to determine whether a mole is skin cancer or not. Early detection could likely have an enormous impact on skin cancer outcomes. The five-year survival rate of one kind of skin cancer drops significantly if detected in its later stages. 
<p> </p>


In this [study](https://www.nature.com/articles/nature21056), an algorithm is trained to determine whether a region of skin tissue is cancerous or not. Using hundreds of thousands of images and labels as input, a convolutional neural network can be trained to do this task. Once the algorithm has been trained, the algorithms predictions can be evaluated against the predictions of human dermatologists on a new set of images. In this study, it was found that the algorithm performed as well as the dermatologists did.

<p> </p>
<b>Example 2:</b>
<p> </p>
Ophthalmology deals with the diagnosis and treatment of eye disorders. One well-known study in 2016 looked at retinal fundus images, which photographed the back of the eye. One disease or pathology to look at here is diabetic retinopathy, which is damage to the retina caused by diabetes and is a major cause of blindness. Currently, detecting DR is a time-consuming and manual process that requires a trained clinician to examine these photos.
<p> </p>

In this [study](https://www.nature.com/articles/s41433-018-0269-y), an algorithm was developed to determine whether patients had diabetic retinopathy by looking at such photos. This study used over 128,000 images of which only 30 percent had diabetic retinopathy. We'll look at this data imbalanced problem, which is prominent in medicine and in many other fields with real-world data. 
<p> </p>

Similarly to the previous study, this study showed that the performance of the resulting algorithm was comparable to ophthalmologists. In the study, a majority vote of multiple ophthalmologists was used to set the reference standard or ground troops, which is a group of experts, best guess of a right answer.
<p> </p>

<b>Example 3: </b>
<p> </p>
Our third example is in histopathology, a medical specialty involving examination of tissues under the microscope. One of the tasks that pathologists do is look at scanned microscopic images of tissue called whole slide images, and determine the extent to which a cancer has spread. This is important to help plan treatment, predict the course of the disease, and the chance of recovery.
<p> </p>

In one study in 2017, using only 270 whole slide images, AI algorithms were developed and then evaluated against pathologists. It was found that the best algorithms performed as well as the pathologists did. Now in histopathology, the images are very large and cannot be fed directly into an algorithm without breaking them down. 
<p> </p>

The general setup of these studies is that instead of feeding in one large, high resolution digital image of the slide, several patches are extracted at a high magnification and used to train a model. These patches are labeled with the original label of the whole slide image and then fed into a deep learning algorithm. 
<p> </p>

In this way, the algorithm can be trained on hundreds of thousands of patches. In this course, you will apply a similar idea of breaking down a large image into smaller images for model training to the task of brain tumor segmentation.

[Relavent study](https://pubmed.ncbi.nlm.nih.gov/30312179/)

### Data Exploration & Image Pre-processing
Below are the common steps to check the data before feeding into the model:
- Data types and null values check
- Unique IDs check
- Explore data labels
- Investigate a single image
- Investigate pixel value distribution
- Standardization by subtracting the mean and dividing by the standard deviation.

### How to handle class imbalance and small training sets
It is worth noting that our dataset contains multiple images for each patient. This could be the case, for example, when a patient has taken multiple X-ray images at different times during their hospital visits. In our data splitting, we have ensured that the split is done on the patient level so that there is no data "leakage" between the train, validation, and test datasets.

### Building and Training a Model for Medical Diagnosis
### Image Classfication and Class Imbalance
Three Key Challenges:
- Class Imbalance 
- Multi-Task
- Dataset Size

### Class Imbalance Problem
What is Class Imbalance problem?
In a medical dataset, it's common to have not an equal number of examples of non-disease and disease. This is a reflection of the prevalence or the frequency of disease in the real-world
- Non-disease examples > Disease examples 

<p align="center"><img width="100%" src="./images/ClassImbalance.png"/></p>

Common Approches to solve "Class Imbalance" is 
- Weighted Loss: By counting the number of each labels and modifying the loss function to weighted loss with the ratio of each label 
<p align="center"><img width="50%" src="./images/WeightedLoss1.png"/></p>

<p align="center"><img width="50%" src="./images/WeightedLoss2.png"/></p>


### Resampling: Re-sample the dataset such that we have an equal number of normal and abnormal examples

With Resampling, you can use just a standard loss function (not a weighted loss function).

The basic idea here is to re-sample the dataset such that we have an equal number of normal and abormal examples in the dataset. 

Things to keep in mind when applying resampling:
- may not be able to include all of the normal examples in re-sample data 
- may have more than one copy of abnormal examples which may lead to overfitting to the example

There are many variations of Resampling:
- Oversampling the normal/abnormal case
- Undersampling the normal/abnormal case

For example, if you find that your training set has 70% negative examples and 30% positive:
- reweight examples in training loss
- undersample negative examples
- oversample positive examples

### Binary Cross Entropy Loss Function
What is "Binary Cross Entropy Loss Function?"
<p align="center"><img width="50%" src="./images/BinaryCrossEntropyLoss.png"/></p>

It is often used in the presence of imbalanced data when algorithm is learning from mostly normal examples. This is nesissary beacause the model that starts to predict a very low probability of disease for everybody and won't be able to identify when an example has a disease.

This loss over here is called the binary cross-entropy loss and this measures the performance of a classification model whose output is between zero and one

Used in the X-ray example (maybe go through the example or go through in word to understand the formula)

### Multi-task challenge
Real World Problem is usually not a binary classficiation, but a  Multi-Task.

There could be various labels as below: 
- Mass or No Mass
- Pneumonia or No Pneumonia
- Edema or No Edema
- ...

Maybe we can learn to do all of the tasks above using one model. An advantage of this is that we can learn features that are common to identifying more than one disease, allowing us to use our existing data more efficiently. This is the setup of multitask learning.

We define **"Multi-Label/Multi-Task Loss"**.
For Multi-Task learning, We can apply the "weighted loss" that we have covered earlier.

## Dataset size: Working with a Small Training Set
"Convolutional Neural Network" is the most common and well suited architecture for processing image which require millions of examples in image classification.

However, the common dataset size in medical imaging is about **10 thousand to 100 thousand.**

## Transfer Learning
1. Pretrain the Network
2. Fine Tuning

Here the idea is to first have the network, look at natural images, and learn to identify objects such as penguins, then use this network as a starting point for learning in medical imaging task by copying over the learned features. The network can then further be trained to look at chest X-rays and identify the presence and absence of diseases. The idea of this process, is that when we're learning our first task of identifying penguins, the network will learn general features that will help it's learning on the medical task. An example of this, might be that the features that are useful to identify the edges on a penguin, are also useful for identifying edges on a lung, which are then helpful to identify certain diseases. Then when we transfer these features to our new network, the network can learn the new task of chest X-ray interpretation with a better starting point. This first step, is called pre-training, and the second step, is called fine-tuning. 

It is generally understood that the early layers of the network, capture low-level image features that are broadly generalisable, while the later layers capture details that are more high-level or more specific to a task. So for instance, the early layer might learn about the edges of an object, and this might be useful for chest X-ray interpretation later. But the later layers, might learn how to identify the head of a penguin and may not be useful for chest X-ray interpretation. So when we fine-tune the network on chest X-rays, instead of fine-tuning all features we've transferred, we can freeze the features learned by the shallow layers and just fine-tune the deeper layers.

Principle of Transfer Learning: 
- the early layers of the network: Low level image features / Broadly generalisable / Edges of image
- the later layers of the network: High level image features / More specific to the task 

How to *"Transfer Learning"*?
- Case 1. To fine tune all of the layers (For moderate or large size of dataset)
- Case 2. Freeze early layers and only fine-tune the later or the last layer (For small size of dataset)

Given a very large dataset, you have the option of training a new model instead of using a pre-trained model.

## Data Augmentation
Generating More Samples : Data Augmentation
- Flipping (may harm the label)
- Rotation (most commonly adopted)
- Translation
- Zoom
- Change brightness or contrast
- Random Cropping
- Noise Insertion
- ...

Things to Keep in Mind when applying Data Augmentation
1. Does the transformation will make the network generalize better?
2. Do Augmentation Keep the Label the Same?

*Slide at the end of 'Generating more samples'

<b>Solutions to thr three key challenges of medical image classification:</b>

Class Imbalance | Multi-Task | Dataset Size
--- | --- | ---
Weighted Loss / Resampling | Multi-Label Loss | Transfer Learning + Data Augmentation

# The problem of Random Sampling
- The Test-set may not include disease case

To get a good estimate of the performance of the model both on non-disease and disease examples,
- sampling oreder: Test , Validation , Training
- sample a tests tset to have at least  X% of examples of our minority class.
- sample to have same distribution of classes as the test set. (same sampling strategy should be used)
- Remaining patients in Training set: Since test and validation set have been artificially sampled to have a large fraction of disease examples. (In the presence of imbalance data, you can still train your model!)
- It's bad to have patients in both training and test sets : Overly optimistic test performace

To tackle this problem in our data set, we can make sure that a patient's X-rays only occur in one of the sets.

## Ground Truth and Consensus Voting
*"How can we determine the correct label for an example?"*

Consensus Voting from a board of doctors
- In medical settings, *"Inter Observer Disagreement"* is common.
- To tackle the inter observer disagreement problem, we use *"Consensus Voting"*.
- Use a group of human experts to determine the ground truth
- In general, the answer will be the majority vote of the three radiologist
- Consensus is considered less reliable than biopsy verification.  However, the limited availability of biopsy data means that consensus voting may still be the best (or only viable) option.

## Additional Medical Testing
Examples:

CT(Computerized Tomography) + X-ray scan
- CT scan shows the 3D structure of the potential abnormality, thus giving the radiologists more information.
-  Keep in mind that there are likely fewer data examples where patients have both the chest x-ray and an additional diagnostic test for the same disease.
![CTconfirmation](./images/CTconfirmation.png)
- In the dermatology study, the ground truth for the test set was determined by a skin lesion biopsy.(Biopsy : an examination of tissue removed from a living body to discover the presence, cause, or extent of a disease.)
![confirmation2](./images/Confirmation2.png)
