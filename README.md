# SomervilleOpenDataExploration
This code is designed to combine, explore, and evaluate open datasets provided by the city of Somerville, MA.
All datasets can be found on the Somerville Data webpage here: https://data.somervillema.gov/.

## Goals
In this project, I wanted to get a better sense of what would make life better for a Somerville resident. By combining regular survey results alongside other data (e.g., crime, vehicular crashes, etc.), I will train machine learning models to identify what features of city life are important for residents. In addition, through data visualization and exploratory data analysis, I can also determine historical trends across different features.

## Datasets Analyzed
Namely, every other year since 2011, Somerville has sent a survey to a random selection of residents where they are asked about their demographics, their satisfaction with parts of city living, and how happy they are in life. In addition, the Somerville Police Department has published data related to crime reports and vehicular crashes. In another dataset, Somerville assays the number of bikers and pedestrians there are through the city through biannual counting days. Together, these data give a sense of city life by combining individual demographics with city-wide statistics. Many of the analyses below will be interacting with a respondent's "happiness score" in response to the question "How happy do you feel right now?". The answer is a 5-point scale where 1 is "Very Unhappy" and 5 is "Very Happy".

## Preliminary Results
### Exploratory Data Analysis
First, I performed a series of exploratory data analysis to identify trends across years. Namely, I first looked to see how the average happiness score changed across time:

<img width="547" height="423" alt="image" src="https://github.com/user-attachments/assets/842afd8d-c8a2-43fa-9c70-1a5491d4f9ee" />

Plotted here is the average happiness score for each year +/- standard deviation. We can observe that, on average, the happiness scores provided are largely similar from year to year. The function to create this figure can take any categorical feature (e.g., neighborhood, race, sex, etc.) and create similar plots. More details are presented within the Jupyter Notebook. 

Knowing that happiness scores are stable is great, but we don't know what the underlying distribution of scores looks like. To this end, I defined a novel function to plot the distribution of happiness scores based on a given feature. Here I show the distribution of happiness scores across the years:
   
<img width="1037" height="540" alt="image" src="https://github.com/user-attachments/assets/f763aed9-9f48-4180-b48d-9451f083a5fb" />

In this, we can see that scores are largely positive (higher scores indicate greater happiness) and that in recent years there are fewer individuals scoring their happiness at the maximum level.

In addition to city-wide trends, we can also dive into more nuanced data analysis by splitting the data by more than one feature. For instance, Somerville is divided into 7 distinct Wards. In the function that plots happiness distributions, I have built in the ability to group scores by multiple, categorical features:

<img width="1113" height="207" alt="image" src="https://github.com/user-attachments/assets/ca585a38-119e-4f8a-8549-a080f9b21878" />

Here, we can observe that in the most recent year, Wards 1 and 6 have the highest proportion of respondents scoring their happiness as a 5. In addition, each Ward has a distinct profile of cross-year happiness score changes.

### Combining Data and Predictive Modeling
Throughout the notebook, you will observe how I joined disparate datasets (e.g., survey results with crime and crash data) to train and evaluate predictive models of different types. Namely, I trained and evaluated: ridge regression model, logistic regression models (one vs one and one vs rest), random forest classifiers, and gradient boosting classifiers (with and without XGBoost). Through RandomSearchCV, I optimized an XGBoostClassifier using the F-1 score as the metric and created a model with ~70.1% accuracy and an F-1 score of ~0.698 after a stratified 5-fold split. With the optimized parameters in hand, I began exploring what features were important for resident happiness.

### Feature Importance
As a first pass, I identified what features were most important for predicting a resident's happiness score. Using the output of XGBoostClassifier (this time without categorical data), I was able to find a number of features related to accessibility, childcare, and safety:

<img width="1107" height="1142" alt="Screenshot 2025-08-29 153943" src="https://github.com/user-attachments/assets/8e61220d-056b-4247-9716-42eba5fe683b" />

With these results, one can make data-driven decisions for what aspects of city life leaders should prioritize. By my eye, increasing efforts into public amenities (e.g., sidewalks, schools, etc.) and ensuring an affordable cost-of-living would be great places to start!
