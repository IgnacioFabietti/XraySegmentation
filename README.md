# Xray Segmentation

### Problem Statement
This problem comes from comes from a Kaggle Notebook, details [here](https://www.kaggle.com/code/rostekus/lung-segmentation/data). The task behind the notebook is to segment lungs via a U-net model, albeit without any EDA or proper description.

### Background
Tuberculosis (TB) is caused by bacteria (Mycobacterium tuberculosis) that most often affect the lungs. Tuberculosis is curable and preventable. A total of 1.5 million people died from TB in 2020 (including 214 000 people with HIV). Worldwide, TB is the 13th leading cause of death and the second leading infectious killer after COVID-19 (above HIV/AIDS). Using advanced tools and technology, automatic analysis and classification of chest X-rays (CXRs) into TB and non-TB can be a reliable alternative to the subjective assessment performed by healthcare professionals. 


### Goal
Using a U-net CNN, we wish to accurately segment the lungs in chest X rays with and without TB.  The masked lungs can help a training physician understand the area of interest for the diagnosis, or be used by a classification model to improve its performance.



### Methods
The X rays and the corresponding masks were given for training. We did not separate them based on the diagnosis due to the small sample size of 704 images, and a vanilla U-net was built to train with the data.
Unlike classification tasks, where one may use accuracy, ROC, F1-score, there are other metrics for segmentation tasks. Out of them we chose the DICE score, together with Adam optimiser and binary cross-entropy loss.

### Results 
After 35 epochs, we achieved a validation loss of 0.3141 and a dice coefficient of 0.7042. After visualising the masks created by the network with the test set, we can say that good masks for segmentation have been achieved via the use of U-net with dice. The dice score could be further improved with some data augmentation and improving the vanilla U-net with resblocks.

### Risks and Assumptions

The dataset size is quite small, and not representative of the many things that can influence an X-ray (different X ray devices, left/right capturing, previous lesions, if they have/had Covid-19, heart problems, smoking habits, age group, etc). Therefore, more data should be collected before testing this on the field. However, the dataset can be aggregated with X-rays of other diseases (Covid-19, pneumonia, etc) in order to create a better segmentation model.

### Data Dictionaries

Image file names are coded as CHNCXR_#####_0/1.png, where ‘0’ represents the normal and ‘1’ represents the abnormal lung (336 cases with manifestation of tuberculosis, and 326 normal cases). The clinical readings of all X-rays are saved as text files following the same file format: _CHNCXR_#####_0/1.txt. 
Each text file contains the patient`s age, gender, and abnormality of the lung. (PTB: pulmonary tuberculosis).

Source: [Kaggle Notebook](https://www.kaggle.com/code/rostekus/lung-segmentation/data)

