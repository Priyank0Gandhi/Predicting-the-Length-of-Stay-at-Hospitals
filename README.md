# Predicting-the-Length-of-Stay-at-Hospitals

I. Introduction
--
The length of stay (LOS) is the period a patient is admitted to a hospital or other
similar medical facility. Moreover, LOS is correlated with disease severity and
mortality. Our goal is to provide an initial length of stay prediction of new coming
patients using a numerical and categorical database as a starting point. By using data
mining algorithms, this prediction is made achievable. The data mining techniques are
employed to make sure the procedure is reliable and lessen the effect of
certainty. Moreover, studies have found patients that, at an emergency department
(ED) are associated with a longer LOS and patients who develop further
complications in intensive care units (ICU) have a longer LOS beforehand at the ED.
To optimize healthcare planning and resources while minimizing the impact of
uncertainty, the LOS must be predicted.
One of the most crucial medical resources is hospital beds, which are frequently
regarded as an important indicator of hospital performance and an accurate predictor
of the state of the local healthcare system's development. Patients' length of stay and
hospital costs are strongly related because most hospitals have a limited supply of
beds. Therefore, cutting the length of stay can save medical costs and the social
burden of medical care while simultaneously increasing the turnover of inpatients.
Finding the pertinent risk variables associated with patient recovery and length of stay
is crucial for the medical system. As a result, one of the biggest issues facing hospital
management right now is how to better allocate hospital beds and address the bed
shortage.
The issue of bed allocation has not been fully solved, and there are still a lot of
hospitals that need beds due to a lack of medical resources in hospitals and a number
of unpredictable events during treatment. Therefore, estimating the length of stay
precisely will aid in logical bed allocation and boost bed usage. An important measure
of hospital management is how long patients stay there. Its prediction calls for the use
of statistical techniques to summarize, analyze, and research its distribution law and
change rule as well as the use of machine learning algorithms to create models that
forecast the length of hospital stay. Studies contributing to LOS have regularly
appeared in the literature. One study was conducted to determine the factors affecting LOS in
the public hospital in Iran. Demonstrated that an increase in age would lead to
an increase in average LOS, Secondly, the average LOS of men is longer than women.
Data mining algorithms such as Decision trees were used for this study.

II. Methods
--
a. Data source
A crucial component of this project is to be able to analyze the large amount
of data contained in Electronic Medical Records (EMRs). Our dataset of
choice was the MIMIC III database which houses over 50,000 actual records
of people that have been admitted to ICU units between 2001 and 2012. As
one would expect the MIMIC database comprises of anonymized EMRs
with the data stored in a relational database format. The Data tables that we
have used for our analysis and predictions are as follows:
A) PATIENTS: This table has 42,520 number of instances, and links to
ADMISSIONS table as well as ICUSTAYS on “Subject_ID”
B) ICUSTAYS: ICUSTAYS tables contains 61,532 rows in it and has links
to PATIENTS table on “Subject_ ID”, and ADMISSIONS table on
“HADM_ID”.
C) ADMISSIONS: The number of rows that the ADMISSIONS table
contains is 58,976. And this table has links to PATIENTS table on
“Subject_ID” .
D) DIAGNOSES_ICD: This table has 651,047 rows, and it has links to
PATIENTS on “Subject_ID”, ADMISSIONS on “HADM_ID”.
b. Data preprocessing:
Data preprocessing involves various steps that need to be followed to
prepare the data appropriately for the model building and training. These
steps depend on the type of dataset we are working on, and this varies from
data to data.
Firstly, we checked the data for any null values present. Upon checking that,
we found that 3% of the data is missing so we removed those instances from
the dataset. The length of stay variable (LOS) represented the number of
days a patient stayed in the hospital. Upon examining this variable, it was
found that few of the data values were negative, and the number of days
cannot be negative, so we removed such values from the data tables, as a
part of data cleaning process.
The admission type variable had 4 types, but it seems that “Emergency and
“Urgent” are one and the same, so the “Urgent” values were replaced with
“Emergency” and the value counts were normalized.
![image](https://github.com/Priyank0Gandhi/Predicting-the-Length-of-Stay-at-Hospitals/assets/96395339/b4ed735f-b37a-4949-8668-5e5049715155)

Fig. 1 Frequency of Admission Type 

![image](https://github.com/Priyank0Gandhi/Predicting-the-Length-of-Stay-at-Hospitals/assets/96395339/ca6aa301-bef8-4eac-8c90-fc0fc321c1d5)

Fig. 2 After converting
urgent category to emergency

As LOS is the target variable, it was important to check the distribution of
this variable across the dataset. A histogram was generated, along with a
frequency curve.

![image](https://github.com/Priyank0Gandhi/Predicting-the-Length-of-Stay-at-Hospitals/assets/96395339/208bbef0-53af-43a5-b48f-fa765905888b)

Fig. 3 Distribution of LOS variable
The above histogram suggests that the data values in LOS variable are not
normally distributed, and the distribution is heavily skewed towards the right.
Hence, we can conclude from this that most of the patients admitted had
their length of stay in the hospital to be less than 10 days.
There was no column containing the ages of patients. So, we created a new
the column containing the Ages of patients by using data values from 2 other
columns like DOB from PATIENTS Table and ADMITTIME from
ADMISSIONS table
A boxplot for the Age variable was also generated, and a table containing
descriptive analysis of Age was prepared.

![image](https://github.com/Priyank0Gandhi/Predicting-the-Length-of-Stay-at-Hospitals/assets/96395339/efde588c-c7ba-43eb-a4ee-fe52865b7693)

Fig. 4 Boxplot for Age variable 
![image](https://github.com/Priyank0Gandhi/Predicting-the-Length-of-Stay-at-Hospitals/assets/96395339/f96c3bf7-2acf-4add-9c9c-fe1699afe3f1)

Fig. 5 Descriptive analysis of Age

This boxplot helped in detecting the outliers in the age variable. On
examining these outliers, it was found that these outliers were irrelevant for
the analysis and prediction but were present in a very small negligible
amount across the data.
For regression analysis, a min-max scaler was used to scale the data, and for
classification technique, we binarized the response variable where 0
represents LOS=< 10 and 1 represents LOS>10 days (about 1 and a half
weeks).
Distribution of the death variable based on gender was generated to
Check what gender type had the most deaths and vice versa.

![image](https://github.com/Priyank0Gandhi/Predicting-the-Length-of-Stay-at-Hospitals/assets/96395339/10b5255a-f016-4a74-9636-3c752c1f0355)

Fig. 6 Distribution of death variable based on gender
Here it can be seen that Males were the most who died and the same can be
seen for alive. This indicates that the number of females admitted was less
than that of male patients.
Later, to increase the interpretability of each ICD-9 code we mentioned the
corresponding diseases and plotted it using a bar graph.

![image](https://github.com/Priyank0Gandhi/Predicting-the-Length-of-Stay-at-Hospitals/assets/96395339/9a2cba6c-d19e-472c-b0ee-77f52c270846)

Fig. 7 ICD-9 Codes and diseases 

![image](https://github.com/Priyank0Gandhi/Predicting-the-Length-of-Stay-at-Hospitals/assets/96395339/131a3d3e-02c0-45eb-b540-60f07bbada08)

Fig.8 ICD-9 Code Diseases
From the bar graph, it is evident that circulatory diseases are more prominent
in ICU patients.

c. Feature selection process
There are various techniques that we can use for selecting features from the
dataset to get accurate predictions after training the model. There needs to
be a balance between model complexity and model simplicity.
Too many features make a model complex, while fewer features make the
model very simple, which would hinder the results. So, selecting an appropriate
number of features is very crucial.
For this, we have used the “Recursive Feature Elimination” technique.
In this, the least important features are eliminated at each feature elimination
step, For this feature importance metrics are used, to select the least
important features for model building.
In general, feature selection techniques are used to get rid of unnecessary
and redundant attributes that don't contribute much to the predictive model's
accuracy or, in certain cases, even make it less accurate. The accuracy of the
prediction model may increase because of feature selection, but it will also
be faster and more cost-effective because the model will be less complex.
We chose all the variables such as Gender_M, nervous, neoplasms, misc,
pregnancy, prenatal, respiratory, skin, age, muscular, mental, Gender_F,
circulatory, blood, injury, congenital, digestive, endocrine, genitourinary,
infectious, ICU, NICU, etc. Removing all death-related columns because we
are finding length of stay and these patients were never discharged.
We also used Weka to see what attributes Weka suggests based on the
Attribute Rankings. Classifier Feature Evaluator was used by using Attribute
Ranking.

![image](https://github.com/Priyank0Gandhi/Predicting-the-Length-of-Stay-at-Hospitals/assets/96395339/7fcd6ad3-1ae5-439f-9924-f5366e07990e)

Fig.9 Attribute Selection in Weka 
![image](https://github.com/Priyank0Gandhi/Predicting-the-Length-of-Stay-at-Hospitals/assets/96395339/41e1f940-61aa-4805-9f54-8536d18d9f86)

Fig.10 Attribute Selection in Weka

d. Description of dependent and independent variables:

A dependent variable here is the Length of Stay. i.e., LOS. We are predicting the LOS
variable of a patient in the ICU. The histogram that we generated (Fig.) for LOS
depicted that the LOS variable is not normally distributed and has most of its
data values under 10 days (about 1 and a half weeks).
For the classification problem, we have converted this variable into a binary variable,
where 1 means LOS>10 days, and 0 means LOS<=10 days.
There are numerous independent variables present in the dataset which help
in predicting the data for the LOS variable. These variables differ based on the
type of problem. For classification problems, there are a different set of
variables than in the regression problem.
Various dummy variables were also generated in the process, to help for
better model building and prediction.

![image](https://github.com/Priyank0Gandhi/Predicting-the-Length-of-Stay-at-Hospitals/assets/96395339/97cabe4f-5c60-4215-a84f-c5dd999acead)

Fig.11 Creation of Dummy Variables

![image](https://github.com/Priyank0Gandhi/Predicting-the-Length-of-Stay-at-Hospitals/assets/96395339/0f0c449e-cf43-4487-be40-7d978bcec9c3)

Fig.12 Creation of Dummy Variables
Descriptive statistics of all the variables are as follows.

  ![image](https://github.com/Priyank0Gandhi/Predicting-the-Length-of-Stay-at-Hospitals/assets/96395339/03ff4902-9dfd-47cc-830e-9526f2b6d804)

Fig.13 Statistical Analysis for Independent Variables

![image](https://github.com/Priyank0Gandhi/Predicting-the-Length-of-Stay-at-Hospitals/assets/96395339/e7f08c51-66d3-491d-8534-671f98254b15)

Fig.14 Statistical analysis for Independent Variables


III. Results and Discussion
--
Random Forest is a versatile machine learning method capable of performing both
regression and classification models. The random forest starts with a standard
machine-learning technique called “decision trees”. In a decision tree, an input is
entered at the top and as it traverses down the tree the data gets put into smaller
and smaller sets or classes. The random forest goes a step beyond by combining
multiple trees to produce the mode class, in the case of classification, or, in the
case of regression, a mean prediction by averaging the results of the individual
trees. In addition, random forests correct for decision trees’ habit of overfitting to
their training set. When a new input is entered into the system, it is run down all
the trees. In the case of a numerical variable, the result may either be an average or
a weighted average of all the terminal nodes that are reached. However, if the input
variable is categorical, then the result will be a voting majority.
Initially, we implemented the Regression technique on our dataset after splitting it
into 80% test and 20% train data, and the following results were obtained. Here,
we have used the Decision Tree and Random Forest models for the regression
tasks. Decision Trees and Random Forest models can be used for both –
Classification and Regression. The metrics used here are R2 (R-square) and MSE
(Mean Square Error) rate. R square explains how well the regression model
explains the observed data which is also known as a goodness of fit measure for
linear regression models. The R-square value measures the strength of the relationship
between your model and the dependent variable on a convenient scale of 0-100%
or 0 to 1. We note that our R-square values obtained for the two models
implemented yield a value close to 0.5 which is considered to be a good fit. 
A higher R-square value does not necessarily mean that the model fits well, but it means
the model is overfitting. It is also noted that the differences between the observed
and the predicted variables are small and unbiased.

Test Set
![image](https://github.com/Priyank0Gandhi/Predicting-the-Length-of-Stay-at-Hospitals/assets/96395339/fe6ba16f-da10-4d7e-b152-951607cf1c77)
Table 2
Mean Square Error (MSE) signifies the average square residual. MSE represents
the error of the predicted model created based on the given set of observations in
the sample. To put it in other words, MSE shows the cost incurred while making
each prediction. There is no correct value for MSE. Simply put, the lower the value
the better, and 0 means the model is perfect. Since there is no correct answer, the
MSE’s basic value is in selecting one prediction model over another. MSE is a
metric to know how close you got to the perfect fit. The model is often fitted by
minimizing MSE, so you'd like to know how close you got to ZERO in the end.
You can use this metric later to compare models, those with smaller MSE fit better
to the data.
Next, we proceeded to implement Classification algorithms using sklearn
library in Python where we considered the same split of the dataset as we did while
implementing Regression techniques. We implemented the Decision Tree and
Logistic Regression as a classifier and obtained the following results.

![image](https://github.com/Priyank0Gandhi/Predicting-the-Length-of-Stay-at-Hospitals/assets/96395339/a3dfe89f-d4ca-4d43-b43f-807b5503b092)

Fig 15. Accuracy Metrics

We achieved an F1 score of 0.793 for the Decision tree classifier algorithm while for
Logistic Regression we achieved 0.394.
We considered Accuracy, Sensitivity, F1 Score, and Specificity as metrics to
evaluate the classification models. Our sensitivity describes how well our test
catches all our positive cases. Sensitivity is calculated by dividing the number of
true-positive results by the total number of positives (which include false positives).
Our specificity describes how well our test classifies negative cases as
negatives. Specificity is calculated by dividing the number of true-negative results
by the total number of negatives (which include false negatives).
Our study involves implementing 3 other classification models for the sake of
comparison through which we could infer the best model that suits our dataset. For
this, we used the Weka software, and the results for the classification algorithms
implemented are as follows. It is to be noted that the Weka software could not
process algorithms on the complete dataset involved in our study, hence we have
performed a random sampling in Weka and considered 15% of data for implementing these algorithms. After sampling, the total instance count was 7655.

The three classification algorithms implemented in Weka were:
1. Naïve Bayes - every pair of features being classified is independent of each
other
2. J48 - J48 is a machine-learning decision tree classification algorithm based on
Iterative Dichotomiser 3. It is very helpful in examining the data categorically and
continuously
3. A random forest is a meta-estimator that fits several decision tree classifiers on various sub-samples of the dataset and uses averaging to improve the predictive accuracy and control over-fitting

   ![image](https://github.com/Priyank0Gandhi/Predicting-the-Length-of-Stay-at-Hospitals/assets/96395339/791e5e30-c383-463c-84aa-085062cddcf1)

Apart from Accuracy as a metric, we have considered AUC which stands for Area under the ROC curve. AUC is used for model comparison. AUC value of 1 infers a perfect model which might be a true case of overfitting and a value under 0.5 is not so favored. Our results have AUC values greater than 0.5 and less than 1 which concludes a good-fitting model. Amongst the three models,
Random Forest performs the best based on accuracy and AUC values. Next in
order is Naïve Bayes and the least performing model is J48.

Strengths and limitations of your study
-
1. The Mimic dataset does not provide any data for patients aged between 7 to 13 years.
2. Weka software could not handle large datasets and we sampled the data to
perform Classification for few of the approaches.
3. MIMIC contains a vast data set and the tables in it. A careful study of all the
tables and variables needs to be conducted to join the tables to form the
required dataset to build the model. Extracting and joining tables is a tedious
process.
4. Classification models perform better than the Regression models which has
been proved with the metrics chosen while implementing models.
5. Our data does not include any bias as we did not focus on a particular
race/ethnicity, nor patients with certain diseases, nor based on the resources of
the hospitals, etc.
6. We followed the best Feature selection methodology as we noted the models
have given good accuracy and specificity values, which confirms our model fits
the data best and does not lead to overfitting.
7. Initially our dataset was imbalanced which would yield to biased and inaccurate
models. To improve this, we performed SMOTE (Synthetic Minority OverSampling technique) and balanced our dataset to ensure the models were accurate
which was done by upsampling the minority class.

IV. Conclusion
--
The scope of our project showcases how Classification algorithms improve the
drawbacks of Regression on the MIMIC dataset. We can infer from the scores of
Specificity and Sensitivity obtained from the Classification and Regression models
in Python that the models we built are good for predicting the LOS. Predicting
LOS is an example of how EHR data can be potentially used for good by applying
data mining techniques. The MIMIC database offered surprisingly good depth and
detail related to medical admissions which enabled me to create a hospital length-of-stay prediction model that considered a lot of interesting input features. The
most surprising aspect of this work was how the patient ICD-9 diagnoses played a
more important role than age when predicting the length of stay.

Future work:
-
This way of predicting Length of Stay outcomes in patients admitted to hospitals
can be used effectively. We used random forest models to predict LOS at the ED
since this model is well suited for treating data with complex interactions between
variables and other non-linear effects. Models based on Deep Neural Networks are
another option that could be explored in further studies.

References:
--
1) Nouaouri, A. Samet and H. Allaoui, "Evidential data mining for length
of stay (LOS) prediction problem," 2015 IEEE International Conference
on Automation Science and Engineering (CASE), 2015, pp. 1415-
1420, doi: 10.1109/CoASE.2015.7294296.
2) Hachesu PR, Ahmadi M, Alizadeh S, Sadoughi F. Use of data mining
techniques to determine and predict length of stay of cardiac
patients. Healthc Inform Res. 2013 Jun;19(2):121-9.doi:
10.4258/hir.2013.19.2.121.Epub 2013 Jun 30. PMID: 23882417;
PMCID: PMC3717435
3) Rathor, R., & Agarkar, P. (2015). LOSH Prediction using Data Mining.
International Journal of Computer Applications, 119.
4) Johnson AE;Pollard TJ;Shen L;Lehman LW;Feng M;Ghassemi
M;Moody B;Szolovits P;Celi LA;Mark RG; (n.d.). Mimic-III, a freely
accessible Critical Care Database. Scientific data. Retrieved November
29, 2022, from https://pubmed.ncbi.nlm.nih.gov/27219127/
5) Yong Chen, "Prediction and Analysis of Length of Stay Based on
Nonlinear Weighted XGBoost Algorithm in Hospital", Journal of
Healthcare Engineering, vol. 2021, Article ID 4714898, 9 pages,
2021. https://doi.org/10.1155/2021/4714898
6) Chrusciel, J., Girardon, F., Roquette, L. et al. The prediction of hospital
length of stay using unstructured data. BMC Med Inform Decis Mak 21,
351 (2021). https://doi.org/10.1186/s12911-021-01722-4
