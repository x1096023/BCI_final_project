# BCI Final Project
Authors: X1096021 許絜茵 X1096023 潘和新 X1096028 余維廷
## Introduction

### Overview

- In this proposal, we try to develop an EEG-based diagnostic tool for depression could offer several advantages, including objective measurements, reduced reliance on subjective self-reporting, and potentially earlier detection and intervention for individuals at risk of depression.
- Our BCI system uses EEG signals to find out the characteristics of EEG from the dataset.

### Data description
- **Experimental Design/Paradigm:**
This dataset comprises resting EEG data from 122 college-aged participants.  Each participant engaged in alternating one-minute periods of eyes-open and eyes-closed tasks, marked by triggers such as OCCOCO or COOCOC. The data were collected between 2008 and 2010 at the John J.B. Allen lab at the University of Arizona. 


All participants were reliably scored as either high or low on the Beck Depression Inventory (BDI), with some also undergoing clinical interviews. The experiment included two resting state sessions: the first one immediately after EEG hookup, lasting 6 minutes, and the second one about an hour after task performance, also lasting 6 minutes. Note that participant 516 lacks second resting data, and participant 544 was excluded from all analyses due to unstable BDI scores between mass and lab assessments. 

It is important to note that some (possibly all) participants may have mislabeled horizontal (HEOG) and vertical (VEOG) electrooculogram channels, and some files have had certain channels interpolated, with no raw data available for reversion. Despite these issues, the first resting session's data quality is high. 

- **Procedure for Collecting Data:**
Resting EEG data were collected from 122 college-aged participants, who are the same individuals involved in the Openneuro probe selection task. Each participant has matching task IDs across both datasets, allowing for easy correlation.

The task was programmed using the DMDX language and included instructions for alternating one-minute periods of eyes open and eyes closed, with triggers indicating these periods (e.g., OCCOCO or COOCOC). Data collection took place between 2008 and 2010 in John J.B. Allen's lab at the University of Arizona.

The dataset involved 122 college-age participants. Participants were consistently scored as either high or low on the Beck Depression Inventory (BDI), and some underwent clinical interviews (see .xls sheet for details). It should be noted that the horizontal (HEOG) and vertical (VEOG) electrooculogram channels might be mislabeled for some, if not all, participants. Additionally, some files have already had certain channels interpolated, with no raw data available for reversion.
The first resting session lasted 6 minutes and was conducted immediately after the EEG setup, while the second session also lasted 6 minutes and was conducted about an hour after task performance. Participant 516 does not have data for the second resting session, and participant 544 was excluded from all analyses due to inconsistent BDI scores between mass and lab assessments (1-4 months apart). Despite these issues, the data quality of the first resting session is high, although the quality of the second resting session has not been reviewed.

- **Data Source:**

   - The dataset is publicly available from researchers in John J.B. Allen lab at U Arizona.
   - We download it from OpenNeuro. [[link]](https://openneuro.org/datasets/ds003478/versions/1.1.0))
- **Data Size:**
    - Number of participants: 122 subjects
    - Number of Channels: 64 EEG channels
    - Formats: .tsv
- **Quality Evaluation:**
   - Surveying and analyzing existing literature
   - Based on the review paper published by Atefeh S et al.[[4]](#ref4), they focus on the application of deep learning algorithms to detect and predict depression using EEG signals. Employing the Systematic Literature Review (SLR) method, they conducted a thorough evaluation of 22 articles published between 2016 and 2021. This review provides detailed summaries of each study and compares their significant aspects. They observed that CNN-based methods, including CNN, 1D CNN, 2D CNN, and 3D CNN, were the most commonly used, representing almost 50% of the total methods, with CNN alone accounting for about one-third. Combined models incorporating CNN and LSTM blocks were also notably popular.
Researchers utilized various feature extraction techniques, with many studies favoring convolutional layers for end-to-end extraction of local features. The common workflow among the analyzed studies involved collecting EEG signals, removing artifacts and noise, extracting relevant features from the pre-processed signals, and using deep learning methods to classify subjects as depressive or normal.

   - Analyzing the hidden independent components within EEG using ICA with ICLabel

![表格](https://github.com/x1096023/BCI_final_project/assets/69157513/0f0bb33b-7348-436e-80ad-0c34b5261561)

## Model Framework
Our BCI architecture is showed below:


- Input/Output Mechanisms:
    - Input: Raw EEG data collected from subjects, who were recruited to be either consistently low or consistently high.
    - Output: The analysis methods used in this project include XGBoost and Random Forest. The results will present the accuracy and confusion matrix of the trained models for both raw and processed data.
- Signal Preprocessing Techniques:
    - We preprocess the data with artifact signal removal using the Artifact Subspace Reconstruction (ASR) method.
- Feature Extraction Approaches:
    - Feature extraction involves calculating the mean, standard deviation, and peak-to-peak amplitude for the alpha, beta, theta, and delta bands to be used as features.
- Classification
-We applied two different machine learning models:
* **XGBoost**

  XGBoost is a highly effective machine learning tool in BCI projects for classifying and interpreting EEG data. Its ability to handle complex, nonlinear data and deliver high performance makes it a valuable component in developing robust and accurate BCI systems.
* **Random Forest**

  Similar to XGBoost, after extracting features such as mean, standard deviation, and peak-to-peak amplitude for various EEG frequency bands (alpha, beta, theta, delta), Random Forest can classify these features to determine different cognitive states or detect conditions like epilepsy.
The data was divided into training and testing sets with a 6:4 split.
## Validation
- **Training and Testing on Separate Datasets**
- The dataset is split into two parts: a training set and a testing set (60% training, 40% testing). The model is trained on the training set and evaluated on the testing set. This method provides an initial assessment of the model's performance on unseen data.
- **Confusion Matrix**
-It provides detailed insights into the performance of the classification model by displaying the true positives, false positives, true negatives, and false negatives.
## Usage
- **Environment and Dependencies**
	- Python Environment: `!pip install mne numpy xgboost scikit-learn matplotlib seaborn`
- **Execution Instructions**
	- Place your EEG data files (.set format) in the specified folder_path.
   - Ensure correct labels are assigned in the labels list corresponding to each EEG file.
   - Open your Python environment and execute the script (bci_model.py). The script will read EEG data, preprocess it (including resampling and filtering), extract features from specified frequency bands, and train an XGBoost classification model.

## Results
- **Raw – xgb1: Raw Data (First time) with XGBoost**
  	- data picked：1\~37、39\~122
  	- accuracy: 0.78
  	- Confusion matrix:
  
- **Raw – xgb1: Raw Data (Second time) with XGBoost**
  	- data picked：1\~9、11\~37、39\~122
  	- accuracy: 0.72
  	- Confusion matrix:

- **Raw – forest1: Raw Data (First time) with random forest**
  	- data picked：1\~37、39\~122
  	- accuracy: 0.65
  	- Confusion matrix:

- **Raw – forest2: Raw Data (Second time) with random forest**
  	- data picked：1\~9、11\~37、39\~122
  	- accuracy: 0.67
  	- Confusion matrix:

- **ASR –Xgb1: Processed Data (First time) with random XGBoost**
  	- accuracy: 0.86
  	- Confusion matrix:

- **ASR –Xgb2: Processed Data (Second time) with random XGBoost**
  	- accuracy: 0.63
  	- Confusion matrix:

- **ASR –forest1: Processed Data (First time) with random forest**
  	- accuracy: 0.91
  	- Confusion matrix:

- **ASR –forest2: Processed Data (Second time) with random forest**
  	- accuracy: 0.70
  	- Confusion matrix:

# Reference
[1] Park, S. M. (2021, August 16). EEG machine learning. Retrieved from osf.io/8bsvr  

[2] Ksibi A, Zakariah M, Menzli LJ, Saidani O, Almuqren L, Hanafieh RAM. Electroencephalography-Based Depression Detection Using Multiple Machine Learning Techniques. Diagnostics (Basel). 2023 May 17;13(10):1779. doi: 10.3390/diagnostics13101779. PMID: 37238263; PMCID: PMC10217709.  

[3] Jaseja H. Electroencephalography in the diagnosis and management of treatment-resistant depression with comorbid epilepsy: a novel strategy. Gen Psychiatr. 2023 Apr 17;36(2):e100868. doi: 10.1136/gpsych-2022-100868. PMID: 37082530; PMCID: PMC10111881.  

[4] Atefeh Safayari, Hamidreza Bolhasani(2021). Depression diagnosis by deep learning using EEG signals: A systematic review. Medicine in Novel Technology and Devices.[[pdf]](https://www.sciencedirect.com/science/article/pii/S2590093521000461)



