# Diabetes-Indicators-Analysis

> - [Video Presentation](https://youtu.be/fwC4S627F9M)
> - [Summary Documentation](https://github.com/EllePancake/Diabetes-Indicators-Analysis/blob/main/Diabetes%20Summary%20Document.pdf)

# Introduction:

## The story Behind The Data
Diabetes is one of the most prevalent chronic diseases in the US, impacting millions of Americans each year and exerting a significant financial burden on the economy. 
Diabetes is a serious chronic disease in which individuals lose the ability to effectively regulate levels of glucose in the blood, and can lead to reduced quality of life and life expectancy. 
After different foods are broken down into sugars during digestion, the sugars are then released into the bloodstream. 
This signals the pancreas to release insulin. Insulin helps enable cells within the body to use those sugars in the bloodstream for energy. 
Diabetes is generally characterised by either the body not making enough insulin or being unable to use the insulin that is made as effectively as needed.

**A full ERD can be found [here](https://dbdiagram.io/d/638ceb8abae3ed7c4544a0da)**

## Data Description
In this task, few datasets are provided:

1. **`demographic_data.csv` - contains demographic data per each person**
    - `uniqueID` - responder ID. Represents one person
    - `Sex`- 0 = female 1 = male
    - `Age` - Age in category (see mapping below) -
        
        *1 - (18 <= AGE <= 24)*
        
        *2 - (25 <= AGE <= 29)*
        
        *3 - (30 <= AGE <= 34)*
        
        *4 - (35 <= AGE <= 39)*
        
        *5 - (40 <= AGE <= 44)*
        
        *6 - (45 <= AGE <= 49)*
        
        *7 - (50 <= AGE <= 54)*
        
        *8 - (55 <= AGE <= 59)*
        
        *9 - (60 <= AGE <= 64)*
        
        *10 - (65 <= AGE <= 69)*
        
        *11 - (70 <= AGE <= 74)*
        
        *12 - (75 <= AGE <= 79)*
        
        *13 - (80 <= AGE <= 99)*
        
        *14 - Don’t know / Refused to answer / Missing*
        
    - `Education` - Education category (see mapping below) -
        *1, 2, 3 - Didn’t graduate high school
        4 - Graduated high school
        5 - Attended college or technical school
        6 - Graduated college or technical school
        9 - Don’t know / Refused to answer / Missing*
    - `Income` - Income category (see mapping below) -
        
        1, 2 - income less than $15,000
        3, 4 - $15,000 <= income < $25,000
        5 - $25,000 <= income < $35,000
        6 - $35,000 to less than $50,000
        7, 8 - income >= $50,000
        9 - Don’t know / Not sure / Missing Respondents
        
2. **`id_label.csv` (Note: This file contains the label for this dataset)**
    - `uniqueID` - responder ID. Represents one person
    - `Diabetes_binary` - 0 is for no diabetes, and 1 is for prediabetes or diabetes
3. **`health_measures.csv` - contains relevant health measures per each person**
    - `uniqueID` - responder ID. Represents one person
    - `NoDocbcCost`- Was there a time in the past 12 months when you needed to see a doctor but could not because of cost? 0 = no 1 = yes
    - `AnyHealthCare` - Have any kind of health care coverage, including health insurance, prepaid plans such as HMO, etc. 0 = no 1 = yes
    - `CholCheck` - 0 = no cholesterol check in 5 years 1 = yes cholesterol check in 5 years
    - `DiffWalk` - Do you have serious difficulty walking or climbing stairs? 0 = no 1 = yes
    - `HvyAlcoholConsump` - (adult men >=14 drinks per week and adult women>=7 drinks per week) 0 = no 1 = yes
    - `Stroke` - (Ever told) you had a stroke. 0 = no 1 = yes
    - `Veggies` - Consume Vegetables 1 or more times per day 0 = no 1 = yes
    - `HighBP` - (Blood Pressure) 0 = no high BP 1 = high BP
    - `HeartDiseaseorAttack` - coronary heart disease (CHD) or myocardial infarction (MI) 0 = no 1 = yes
    - `PhysActivity` - physical activity in past 30 days - not including job; 0 = no 1 = yes
    - `MentHlth` - days of poor mental health scale 1-30 days
    - `HighChol` - 0 = no high cholesterol 1 = high cholesterol
    - `BMI` - Body Mass Index
    - `GenHlth` - Would you say that in general your health is: scale 1-5 1 = excellent 2 = very good 3 = good 4 = fair 5 = poor
    - `Fruits` - Consume Fruit 1 or more times per day 0 = no 1 = yes
4. **`enriched_data.csv` -** extra data gathered per each person and contains few more measures
    - `uniqueID` - responder ID. Represents one person
    - `PhysHlth` - physical illness or injury count of days in past 30 days, scale 1-30
    - `Smoker` - Have you smoked at least 100 cigarettes in your entire life? [Note: 5 packs = 100 cigarettes] 0 = no 1 = yes

## Process

> - See SQL questions & answers [here](https://github.com/EllePancake/Diabetes-Indicators-Analysis/blob/main/Diabetes%20Indicators%20-%20SQL%20Questions.ipynb)
> - See Jupyter Notebook with initial analysis & exploration [here](https://github.com/EllePancake/Diabetes-Indicators-Analysis/blob/main/Diabetes%20Indicators%20-%20Analysis.ipynb)

Python libraries used: NumPy, Pandas, Matplotlib, Seaborn 

### Initial Analysis

I set out to investigate each of the four datasets, of 10k rows each, before combining them horizontally using the "uniqueID" column. Next, I cleaned the dataframe and looked into outliers. Then I dove into exploratory data analysis to further understand the data and the relationships between various points. Lastly, I zoomed in by asking specific questions and using the exploration to find answers.  

## Questions & Findings

### Initial Analysis Questions

The goal in this project is to explore some of the following research questions:

1. Can survey questions from the data in this project provide accurate predictions of whether an individual has diabetes?
> Yes, we found a number of indicators that very consistently aligned with whether or not a person had diabetes. Correlations can be seen in this chart below.

![image](https://user-images.githubusercontent.com/107210379/219715310-d5265734-c0e8-4456-9fb4-05cd55fbb015.png)

2. What risk factors are most predictive of diabetes risk?
> As seen in the chart above, I found the following correlations: 

Positive:
- High blood pressure
- General Health
- BMI
- Difficulty walking/climbing stairs
- High Cholesterol

Negative (strong):
- Physical activity in the past 30 days (not including work)
- Eating fruits at least once per day
- Eating vegetables at least once per day
- Lack of heavy alcohol cunsumption (defined as 7 drinks/week for women & 14 drinks/week for men)

3. Can we use a subset of the risk factors to accurately predict whether an individual has diabetes?
> Absolutely. We can't easily measure things like cholesterol, blood pressure, and BMI without a doctor, but we can easily ask questions to find out things such as general health and whether or not someone has had difficulty walking recently. 

4. Can we create a short form of questions from the datasets in this task using feature selection to accurately predict if someone might have diabetes or is at high risk of diabetes, based on the analysis one will conduct?
> Yes, using the three strongest predictors for and against, that don't require an exam conducted by a doctor these are the questions we can ask:
- Have you had physical activity in the last 30 days, not including work? 
- Have you had difficulty walking or lcimbing the stairs in the last 30 days? 
- How would you rate your general health on a scale of 1 to 5? 

## Recommendations

- Create a short form of questions to find people at a higher risk for diabetes to then be seen by a doctor. 
