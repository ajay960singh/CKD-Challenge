# homusk-test

### Task Description
Build a disease progression classification model to detect progress of CKD(Chronic Kidney Disease) patients. A dataset of 300 patients, consisting of lab test results, medication dosages and demographic, is provided for predicting if a patient would progress in the disease stage.

### Challenges

- Imbalanced Dataset : The datset is imbalanced with 200 negative examples and 100 positive examples.

  - Evaluation Metric : Keeing in mind the imbalance, the model was optimized for maximum F1 score on the validation set. F1 score is a good predictor of precision and recall of classes, making it a suitable choice for such cases.
  
  - Loss Function : Binary Cross Entropy is used as a loss function and it is weighed to give more importance to the smaller positive examples.
  
- Irregular Time Gap : The data provided consists of irregular lab tests and medication with varying gap between subsequent visits. It is important to account for this irregularity in the data, which is crucial from RNNs.

  - Approach I : For every lab test and medication data, three vectors are created - value, mask vectors and time difference vectors. Mask vectors serve as a binary representation for missing values and time difference vectors represent the number of days since the last visit. The idea is to let RNN learn from these additional vectors information about our data
  
  - Approach II : The irregular data is converted into regular intervals. Seven new timestamps from 100 to 700 days are created with time gap of 100 days. 100 is selected as the mean difference between subsequent visits lies between 100 and 150 for all the six lab tests. For each timestamp, the data for the day nearest to it is selected - for example, if at timestamp = 200, there's two lab test results for glucose at 150 day and 170 day, the one for 170 day will be selected. Furthermore, the missing values are replaced by respective means of the features. This approach is finally used, as shown in main.ipynb
  
### Model

The model consists of two parts -  the first part is an RNN, which reads sequence, containing the lab test results and medication data and the second part is Linear layers, which add static features (age and gender) to the output of RNN. 
 
### Result

 A mix of pre-processing methods are used to come up with the final model. The final_model gives an F1 score of 0.75 on the validation set.
 
