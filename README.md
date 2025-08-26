# SomervilleOpenDataExploration
This code is designed to combine, explore, and evaluate open datasets provided by the city of Somerville, MA.
All datasets can be found on the Somerville Data webpage here: https://data.somervillema.gov/.

## Goals
In this project, I wanted to get a better sense of what would make life better for a Somerville resident. By combining regular survey results alongside other data (e.g., crime, vehicular crashes, etc.), I will train machine learning models to identify what features of city life are important for residents. In addition, through data visualization and exploratory data analysis, I can also determine historical trends across different features.

## Datasets Analyzed
Namely, every other year since 2011, Somerville has sent a survey to a random selection of residents where they are asked about their demographics, their satisfaction with parts of city living, and how happy they are in life. In addition, the Somerville Police Department has published data related to crime reports and vehicular crashes. In another dataset, Somerville assays the number of bikers and pedestrians there are through the city through biannual counting days. Together, these data give a sense of city life by combining individual demographics with city-wide statistics. Many of the analyses below will be interacting with a respondent's "happiness score" in response to the question "How happy do you feel right now?". The answer is a 5-point scale where 1 is "Very Unhappy" and 5 is "Very Happy".

## Strategy and Preliminary Results
First, I performed a series of exploratory data analysis to identify trends across years. Namely, I first looked to see how the average happiness score changed across time:

<img width="547" height="423" alt="image" src="https://github.com/user-attachments/assets/842afd8d-c8a2-43fa-9c70-1a5491d4f9ee" />

Plotted here is the average happiness score for each year +/- standard deviation. We can observe that, on average, the happiness scores provided are largely similar from year to year. The function to create this figure can take any categorical feature (e.g., neighborhood, race, sex, etc.) and create similar plots. More details are presented within the Jupyter Notebook. 

Knowing that happiness scores are stable is great, but we don't know what the underlying distribution of scores looks like. To this end, I defined a novel function to plot the distribution of happiness scores based on a given feature. Here I show the distribution of happiness scores across the years:
   
<img width="1037" height="540" alt="image" src="https://github.com/user-attachments/assets/f763aed9-9f48-4180-b48d-9451f083a5fb" />

In this, we can see that scores are largely positive (higher scores indicate greater happiness) and that in recent years there are fewer individuals scoring their happiness at the maximum level.

In addition to city-wide trends, we can also dive into more nuanced data analysis by splitting the data by more than one feature. For instance, Somerville is divided into 7 distinct Wards. In the function that plots happiness distributions, I have built in the ability to group scores by multiple, categorical features:

<img width="1113" height="207" alt="image" src="https://github.com/user-attachments/assets/ca585a38-119e-4f8a-8549-a080f9b21878" />

Here, we can observe that in the most recent year, Wards 1 and 6 have the highest proportion of respondents scoring their happiness as a 5. In addition, each Ward has a distinct profile of cross-year happiness score changes.

Throughout the notebook, you will observe how I joined disparate datasets (e.g., survey results with crime and crash data) to train and evaluate predictive models of different types (e.g., regression models, random forest classifiers, and gradient boosting classifiers). As of now, my best models are performing with ~70% accuracy. With additional feature engineering, I hope to increase that accuracy score (among other metrics) and determine what features are most important when predicting a happiness score.


