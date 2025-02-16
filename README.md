#Zomato Data Analysis Using Python

## Overview
This project analyzes a Zomato dataset using Python to gain insights into restaurant trends, customer preferences, and pricing strategies. The analysis includes data cleaning, visualization, and answering key business questions.

## Libraries Used
NumPy – Fast numerical computations

Pandas – Data manipulation and analysis

Matplotlib – Data visualization

Seaborn – Statistical data visualization

(You can use Google Colab or Jupyter Notebook for this analysis.)

## Key Questions Addressed
a. Do more restaurants offer online delivery than offline services?
b. What types of restaurants are most preferred by the public?
c. What is the preferred price range for couples dining out?

## Data Preparation
Step 1: Import Required Libraries
``` python

import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns
```
Step 2: Load the Dataset
python
Copy
Edit
df = pd.read_csv("Zomato-data.csv")
print(df.head())
Step 3: Data Cleaning
Convert the rate column to a float by removing the denominator:

python
Copy
Edit
def clean_rate(value):
    return float(str(value).split('/')[0])

df['rate'] = df['rate'].apply(clean_rate)
Exploratory Data Analysis (EDA)
1️⃣ Check for Missing Values
python
Copy
Edit
print(df.info())
2️⃣ Restaurant Type Distribution
python
Copy
Edit
sns.countplot(x=df['listed_in(type)'])
plt.xlabel("Type of Restaurant")
plt.show()
🔹 Insight: Most restaurants belong to the dining category.

3️⃣ Most Voted Restaurant
python
Copy
Edit
max_votes = df['votes'].max()
top_restaurant = df[df['votes'] == max_votes]['name']
print("Most voted restaurant:", top_restaurant.values[0])
4️⃣ Online vs Offline Orders
python
Copy
Edit
sns.countplot(x=df['online_order'])
plt.show()
🔹 Insight: Most restaurants do not accept online orders.

5️⃣ Rating Distribution
python
Copy
Edit
plt.hist(df['rate'], bins=5)
plt.title('Ratings Distribution')
plt.show()
🔹 Insight: Most restaurants have ratings between 3.5 to 4.0.

6️⃣ Preferred Price Range
python
Copy
Edit
sns.countplot(x=df['approx_cost(for two people)'])
plt.show()
🔹 Insight: Couples mostly prefer restaurants with an approximate cost of ₹300.

7️⃣ Online vs Offline Order Ratings
python
Copy
Edit
sns.boxplot(x='online_order', y='rate', data=df)
plt.show()
🔹 Insight: Online orders tend to receive higher ratings than offline ones.

8️⃣ Heatmap for Online Orders vs Restaurant Type
python
Copy
Edit
pivot_table = df.pivot_table(index='listed_in(type)', columns='online_order', aggfunc='size', fill_value=0)
sns.heatmap(pivot_table, annot=True, cmap='YlGnBu', fmt='d')
plt.title('Heatmap of Online Orders by Restaurant Type')
plt.show()
🔹 Insight: Dining restaurants prefer offline orders, while cafes receive more online orders.

Conclusion
Most restaurants do not accept online orders.
Dining restaurants are the most common category.
The most popular price range for couples is around ₹300.
Online orders tend to receive better ratings than offline orders.
🔗 Dataset Source: [Provide dataset link]
