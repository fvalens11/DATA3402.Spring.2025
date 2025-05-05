# Horse Health Prediction Challenge

By Frank Valenzuela:
This ReadMe file displays the efforts I went through to try and solve the Horse Health Prediction Challenge. 

## Overview

* The goal defined by the Kaggle Challenge was to predict the outcome of horses based on various medical indicators. This was a classification problem that I chose to solve using Scikit-Learn's Random Forest Model. My best model was able to predict the outcome of a horse (death/life) about 43% of the time. At the time of writing the best performance on Kaggle of this metric is 78%.

## Summary of Workdone

### Data


 * Type: 3 CSV Files
    * Input: CSV file (Test), CSV file (Train), CSV file (Sample_Submission)
    * Input: 29 features ranging from 'id', 'age', 'temperature of body features', 'pulse', and other medical indicators. 
  * Size: 386.6 KB
  * Instances (Train, Test, Validation Split): 1200 horses used for Train, 800 used for Test, and 800 used as validation

#### Data Visualization


![image](https://github.com/user-attachments/assets/af575ee1-b639-4958-828d-8a50c592bbb2)
![image](https://github.com/user-attachments/assets/c906f413-d7e3-40ee-93a6-b70ed0b73f6b)




There were not many numerical features to begin with but these 2 show an example of a good feature and a bad feature. I dropped the second feature before training my model.

#### Preprocessing / Clean up

* I first dropped any missing entries from both datasets. (Total of 350)
* I then One-Hot Encoded all the remaining categorical features
* I dropped features like 'hospital_number' that would interfere with the model's calculation
* Lastly, I standardized the remaining numerical features

### Problem Formulation

* I was trying to predict the outcome of horses if they would either live, die, or be euthanized
* I used Scikit-Learn's Random Forest Model with 100 classifiers with a random state of 42 to get my result
* At first I got a score of 22% so introduced a weight of 2 on correctly identifying horses who will live which increased my score to 34%
* I then decided to drop 'euthanized' as an outcome and combine it with 'die' which increased my score to 43%

### Training

* The training featured a split of the Train dataset across X_train and Y_train and a test from X_Test within Scikit-Learn's Random Forest Classifier Model.
* For this model I used 100 classifiers and a random state of 42.
* I then tried the model again but changed it by adding on a 2x weight for correctly classifying horses who will live
* I then tried the model again but changed it so that the outcomes 'died' and 'euthanized' were merged together into the outcome 'died' (Just 2 outcomes: lived/died)


### Performance Comparison

* With each new thing I tried my F1 score continued to increase.
* I came to the conclusion that my model that scored 43% was the best I was going to achieve with the Random Forest Classifier

![image](https://github.com/user-attachments/assets/26b9fcbb-4638-44e5-9e06-5b55fa73413e)



### Conclusions

* I achieved my best result after adding in a weight classifier to the outcome 'lived' and after merging the outcomes of 'euthanized' and 'died' into a single outcome 'died'

### Future Work

* I would like to try this project again but next time using a different model besides Random Forest such as XGBoost, or K-Nearest Neighbors, or a Decision Tree
* I would also like to try this project again but next time changing the percentage of the test, train, and validation split

## How to reproduce results

*Download and import into Python Notebook (Numpy, Pandas, Matplotlib, and Scikit-learn)
*Download csv files from Kaggle Challenge website
(Refer to "Data", "Training" and "Project Evaluation" subheadings for exact instructions/explanations)

### Overview of files in repository

* 2 notebooks:
* Readable Final: A notebook that is readable and easily understandable
* horse_project_final: A notebook that contains a lot of scratch work and double checking as well as all the things in "Readable Final"

### Software Setup

* I used these from Scikit-learn:
* from sklearn.ensemble import RandomForestClassifier
from sklearn.model_selection import train_test_split
from sklearn.preprocessing import LabelEncoder
from sklearn.metrics import f1_score
* Aswell as Pandas, Numpy, and Matplotlib


### Data

* This link will take you to the download page of the Kaggle Challenge : [https://www.kaggle.com/competitions/playground-series-s3e22/data](url)
* For preprocessing:
* I dropped all missing entries
* I One-Hot Encoded the following features: (surgery,temp_of_extremities,peripheral_pulse,capillary_refill_time,pain,peristalsis,abdominal_distention,nasogastric_tube,nasogastric_reflux,rectal_exam_feces,abdomen,abdomo_appearance,surgical_lesion,cp_data,lesion_2, lesion_3,and outcome)
* I dropped features (hospital_number, and lesion_1) & ('id' only for model training, needed it for result)
* I standardized the following numerical features: (pulse, rectal_temp, respiratory_rate, nasogastric_reflux_ph, packed_cell_volume, total_protein,and abdomo_protein)

### Training

* I set my X_train equal to my Train dataset making sure to drop the "outcome" column
* I set my Y_train equal to the "outcome" column within the Train dataset
* I set my X_test equal to my Test dataset making sure to drop the "id" column
* I then imported the RandomForestClassifier from Scikit-learn and set the n_estimators = 100, and the random_state = 42
* I mapped the outcomes accordingly : 1 == lived, 0 == died, (2 == euthanized)
* I then exported my result to a csv titled 'predictions.csv' with 2 columns 'id' and 'outcome'

#### Performance Evaluation

* I then evaluated my model by comparing it to the 800 entries that I put aside for validation
* I added a 2x weight to correctly identifying horses that lived
* I also merged the mapped outcomes for 'died' and 'euthanized'
* I imported scikit-learn's f1 score and found the f1 score for my model

## Citations

* link to Kaggle Challenge: [https://www.kaggle.com/competitions/playground-series-s3e22/data?select=sample_submission.csv
](url)
*@misc{playground-series-s3e22,
    author = {Walter Reade and Ashley Chow},
    title = {Predict Health Outcomes of Horses},
    year = {2023},
    howpublished = {\url{https://kaggle.com/competitions/playground-series-s3e22}},
    note = {Kaggle}
}




