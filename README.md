# Ex-03 EXPLORATORY DATA ANALYSIS

## AIM:
To perform Exploratory Data Analysis on the given data set. 

## EXPLANATION:
The primary aim with exploratory analysis is to examine the data for distribution, outliers and 
anomalies to direct specific testing of your hypothesis.
 

## ALGORITHM:
### STEP 1:
Import the required packages to perform Data Cleansing,Removing Outliers and Exploratory Data Analysis.
### STEP 2:
Replace the null value using any one of the method from mode,median and mean based on the dataset available.
### STEP 3:
Use boxplot method to analyze the outliers of the given dataset.
### STEP 4:
Remove the outliers using Inter Quantile Range method.
### STEP 5:
Use Countplot method to analyze in a graphical method for categorical data.
### STEP 6:
Use displot method to represent the univariate distribution of data.
### STEP 7:
Use cross tabulation method to quantitatively analyze the relationship between multiple variables.
### STEP 8:
Use heatmap method of representation to show relationships between two variables, one plotted on each axis.


## CODE:
```
import pandas as pd
import numpy as np
import seaborn as sns
df=pd.read_csv("titanic_dataset.csv")
df.info()
df.isnull().sum()
df["Age"]=df["Age"].fillna(df["Age"].median())
df["Embarked"]=df["Embarked"].fillna(df["Embarked"].mode()[0])
df["Cabin"]=df["Cabin"].fillna(df["Cabin"].mode()[0])
df.info()
df.isnull().sum()
df.boxplot()
cols = ['Age', 'SibSp','Parch','Fare'] # one or more.
Q1 = df[cols]. quantile(0.25)
Q3 = df[cols]. quantile(0.75)
IQR = Q3 - Q1
df = df[~((df[cols] < (Q1 - 1.5 * IQR)) |(df[cols] > (Q3 + 1.5 * IQR))). any(axis=1)]
df.boxplot()
df.info()
df["Embarked"].value_counts()
df["Pclass"].value_counts()
df["Survived"].value_counts()
sns.countplot(x="Survived",data=df)
sns.countplot(x="Pclass",data=df)
sns.countplot(x="Sex",data=df)
sns.displot(df["Fare"])
sns.countplot(x="Pclass",hue="Survived",data=df)
sns.countplot(x="Sex",hue="Survived",data=df)
sns.displot(df[df["Survived"]==0]["Age"])
sns.displot(df[df["Survived"]==1]["Age"])
pd.crosstab(df["Pclass"],df["Survived"])
pd.crosstab(df["Sex"],df["Survived"])
df.corr()
sns.heatmap(df.corr(),annot=True)
```
## OUTPUT:
### DATA CLEANSING:
![OUTPUT](./output1.png)
![OUTPUT](./output2.png)
### BOXPLOT METHOD TO ANALYZE OUTLIERS:
![output](./output3.png)
### REMOVING OUTLIERS USING IQR METHOD:
![output](./output4.png)
### COUNTPLOT METHOD FOR DATA ANALYSIS:
![output](./output5.png)
![output](./output6.png)
![output](./output7.png)
![output](./output8.png)
### DISPLOT METHOD FOR DATA ANALYSIS:
![output](./output9.png)
![output](./output12.png)
![output](./output13.png)

### COUNTPLOT METHOD TO COMPARE TWO ENTITIES:
![output](./output10.png)
![output](./output11.png)

### CROSS TABULATION FOR DATA ANALYSIS:
![output](./output14.png)
### CORRELATION METHOD:
![output](./output15.png)
## INFERENCE:
* The count of passengers who survived is high for those who travelled in class 3.
* Female passengers had survived more than male passengers.
* Passengers with age in the range of 20-30 had survived compared to other age group people.
* Maximum number of passengers had travelled in class 3.
* There is high proportion of male with respect to female in the ship.

## RESULT:
Hence the given data set has undergone data cleansing and outlier removal.Later Exploratory data analysis is done to get inference from the given data set.
