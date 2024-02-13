# datafun-06-eda for Project 6 EDA Notebook- Exploratory Data Analysis with Jupyter Using Diamond Dataset

## Overview

This prjoect will use a Jupyter notebook to further analyze data for the Diamond dataset to produce visualizations and answer data related questions.

## The Dataset for Diamonds.csv 

This large Dataset has various columns of: carat, cut, color, clarity, depth as percentage, table-width of top diamond, price, x-length in mm, y-width, z-depth in mm for 50,000 diamonds.

https://raw.githubusercontent.com/mwaskom/seaborn-data/master/diamonds.csv  

Sample of the data: first ten lines:

"carat","cut","color","clarity","depth","table","price","x","y","z"
0.23,"Ideal","E","SI2",61.5,55,326,3.95,3.98,2.43
0.21,"Premium","E","SI1",59.8,61,326,3.89,3.84,2.31
0.23,"Good","E","VS1",56.9,65,327,4.05,4.07,2.31
0.29,"Premium","I","VS2",62.4,58,334,4.2,4.23,2.63
0.31,"Good","J","SI2",63.3,58,335,4.34,4.35,2.75
0.24,"Very Good","J","VVS2",62.8,57,336,3.94,3.96,2.48
0.24,"Very Good","I","VVS1",62.3,57,336,3.95,3.98,2.47
0.26,"Very Good","H","SI1",61.9,55,337,4.07,4.11,2.53
0.22,"Fair","E","VS2",65.1,61,337,3.87,3.78,2.49
0.23,"Very Good","H","VS1",59.4,61,338,4,4.05,2.39

## Project Setup

create repostitory in GitHub named datafun-06-ed

clone to machine with 
'''
git clone https://github.com/S572396/datafun-06-eda 

create virtual environment with
'''
. venv
'''

active virtual environoment with:
'''
.venv\Scripts\active
'''

install packages with:

'''
python -m pip install requests
python -m pip install numpy pandas matplotlib seaborn pyarrow
'''

freeze dependencies with:

'''
python -m pip freeze > requirements.txt
'''
## Project Setup Part II Jupyter Notebook

jupyter extention added in to terminal

sandraruiz_eda.ipynb jupyter notebook updated for overview

## Diamonds.csv dataset added in from seaborn :

'''
import seaborn as sns

# Load the diamonds dataset into a pandas DataFrame
df = sns.load_dataset('diamonds')

# Inspect the first rows of the DataFrame
print(df.head())

'''

# Dataset Diamonds.csv loaded sucessful, sample:

 carat      cut color clarity  depth  table  price     x     y     z


0   0.23    Ideal     E     SI2   61.5   55.0    326  3.95  3.98  2.43

## Data Inspection

'''
print(df.head(10))
print(df.shape)
print(df.dtypes)
'''

## Statistics Summary
'''
print (df.describe())

'''
## Avg of diamond carats
'''
# Calculate the average of the 'carat' column
average_carat = df['carat'].mean()

# Print the result
print("Average Carat:", average_carat)
'''
## Create histogram of column of 'carat'

'''
plt.figure(figsize=(10, 6))
sns.histplot(df['carat'], bins=30, kde=False, color='blue', edgecolor='black')

plt.title('Histogram of Carat')
plt.xlabel('Carat')
plt.ylabel('Frequency')
plt.show
'''