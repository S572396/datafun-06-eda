# datafun-06-eda for Project 6 EDA Notebook- Exploratory Data Analysis with Jupyter Using Diamond Dataset

## Overview

This prjoect will use a Jupyter notebook to further analyze data for the Diamond dataset to produce visualizations and answer data related questions.

## The Dataset for Diamonds.csv 

This large Dataset has various columns of: carat, cut, color, clarity, depth as percentage, table-width of top diamond, price, x-length in mm, y-width, z-depth in mm for 50,000 diamonds.

https://raw.githubusercontent.com/mwaskom/seaborn-data/master/diamonds.csv  

Sample of the data: first few lines:

"carat","cut","color","clarity","depth","table","price","x","y","z"
0.23,"Ideal","E","SI2",61.5,55,326,3.95,3.98,2.43
0.21,"Premium","E","SI1",59.8,61,326,3.89,3.84,2.31

## Dependencies Implemented:
'''
import matplotlib.pyplot as plt
import pandas as pd
import seaborn as sns
'''


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

## Load the diamonds dataset into a pandas DataFrame
df = sns.load_dataset('diamonds')

## Inspect the first rows of the DataFrame
print(df.head())

'''

### Dataset Diamonds.csv loaded sucessful, sample:

 carat      cut color clarity  depth  table  price     x     y     z


0   0.23    Ideal     E     SI2   61.5   55.0    326  3.95  3.98  2.43

## Data Inspection

'''
print(df.head(10))
print(df.shape)
print(df.dtypes)
'''
## Helpful information about Diamdonds: The 4 C's of Diamonds 
#### Arranged from lowest to highest category

* Cut-Poor Cut, Fair Cut, Good Cut, Very Good Cut, Excellent Cut, Ideal Cut
* Color- Faint(KLM), Near Colorless(G,H,I), Colorless(D,E,F)
* Clarity-Included(11,12,13), Slightly Inclued(S11,S12,S13), Very Slightly Inclued(VS1,VS2), IF(Internal Flawless)
* Carat-Weight of Diamond can range from 0 to whole nummbers, often decimals used, example 0.75 carat, 1.0 carat, 2.5 carat etc.
 
** Retrived from: [Grown Brilliance](https://www.grownbrilliance.com/education-guide/learn-about-the-4cs)



## Statistics Summary
'''
print (df.describe())

'''
## Avg of diamond carat weight
'''
## Calculate the average of the 'carat' column
average_carat = df['carat'].mean()

## Print the result
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
### markdown answer added

## how many are 'Ideal' diamonds?

'''
import seaborn as sns
import matplotlib.pyplot as plt
df = sns.load_dataset('diamonds')

## Create a count plot for the 'cut' column
plt.figure(figsize=(8, 6))
sns.countplot(x='cut', data=df, palette='viridis')  # You can choose a different color palette if desired

plt.title('Count Plot of Diamond Cuts')
plt.xlabel('Cut')
plt.ylabel('Count')

plt.show()

ideal_count = df['cut'].value_counts()['Ideal']
print("Number of diamonds labeled 'Ideal':", ideal_count)

'''
### mardown answer added

## Data Transformation and Feature Engineering

    1.Rename one column:
    '''
import seaborn as sns

df = sns.load_dataset('diamonds')

df = df.rename(columns={'x': 'length', 'y': 'width', 'z': 'depth'})

print("Column names after renaming:")
print(df.columns)

print("\nFirst 4 rows of the DataFrame:")
print(df.head(4))
'''
### markdown insight added of sucessful rename

    2.Add one new column named best_value:
    '''
    import seaborn as sns

df = sns.load_dataset('diamonds')

### Create a new column 'best_value' based on specified conditions
conditions = (
    (df['price'] < 5000) &
    (df['color'].isin(['D', 'E', 'F'])) &
    (df['cut'].isin(['Ideal', 'Premium'])) &
    (df['clarity'].isin(['VS1', 'VS2', 'IF']))
)
df['best_value'] = conditions.astype(int)

best_value_rows = df[df['best_value'] == 1]

### Display the DataFrame with 'best_value' equal to 1
print("Rows with 'best_value' equal to 1:")
print(best_value_rows)

### Count the total number of rows that meet the 'best_value' specification
total_best_value_count = df['best_value'].sum()
'''

### markdown insight noted of sucessful creation


## how many meet criteria of 4 C's: cut, color, clairity,and carat?
'''
 Filter the DataFrame based on the specified conditions

filtered_df = df[(df['cut'] == 'Ideal') & (df['color'] == 'D') & (df['clarity'] == 'IF') & (df['carat'] > 0.8)]

count_best_values = len(filtered_df)
print("Number of diamonds meeting the best values:", count_best_values)

'''
### markdown answer added

## What is the correlation between diamond quality and price?

'''
## Sort the DataFrame by 'price' column in descending order
sorted_df = df.sort_values(by='price', ascending=False)

## Display all rows of the sorted DataFrame
print(sorted_df)

'''
### Markdown observation added

### Price and Carat Scatter Plot created to further compare information

'''
import seaborn as sns
import matplotlib.pyplot as plt

sorted_df = df.sort_values(by='price', ascending=False)

## Create a scatter plot
plt.figure(figsize=(10, 6))
sns.scatterplot(x='carat', y='price', data=sorted_df)

plt.xlabel('Carat')
plt.ylabel('Price')
plt.title('Scatter Plot of Diamonds - Price vs. Carat')

plt.show()
'''
### markdown findings added in

## other factors that affect diamond prices of cut, color, clarity in additon to carat.

Scatter Plot Matrix for cut, carat in relation to price

'''
import seaborn as sns
import matplotlib.pyplot as plt

## Create a scatter plot matrix
sns.pairplot(df, vars=['carat', 'price'], hue='cut', markers='o', palette='viridis')

plt.show()
'''
### mardown insights added in

## Histograms Created for Color and Clarity in relation to Price
'''
import seaborn as sns
import matplotlib.pyplot as plt
df = sns.load_dataset('diamonds')

plt.figure(figsize=(8, 16))

plt.subplot(4, 1, 2)
sns.histplot(x='price', data=df, hue='color', multiple='stack', palette='viridis', bins=30)
plt.title('Diamond Price Histogram by Color')

plt.subplot(4, 1, 3)
sns.histplot(x='price', data=df, hue='clarity', multiple='stack', palette='viridis', bins=30)
plt.title('Diamond Price Histogram by Clarity')

plt.tight_layout()
plt.show()

'''
### markdown insights added in
