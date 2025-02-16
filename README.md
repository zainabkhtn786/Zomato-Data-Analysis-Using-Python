# Zomato Data Analysis Using Python

## 1. Overview
This project analyzes a Zomato dataset using Python to gain insights into restaurant trends, customer preferences, and pricing strategies. The analysis includes data cleaning, visualization, and answering key business questions.

## 2. Libraries Used
NumPy – Fast numerical computations

Pandas – Data manipulation and analysis

Matplotlib – Data visualization

Seaborn – Statistical data visualization

(You can use Google Colab or Jupyter Notebook for this analysis.)

## 3. Key Questions Addressed
a. Do more restaurants offer online delivery than offline services?

b. What types of restaurants are most preferred by the public?

c. What is the preferred price range for couples dining out?

## 4. Data Preparation
#### Step 1: Import Required Libraries
``` python

import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns
```

#### Step 2: Load the Dataset
``` python

df = pd.read_csv("Zomato-data.csv")
print(df.head())
 ```

#### Step 3: Data Cleaning
Convert the rate column to a float by removing the denominator:

``` python

def clean_rate(value):
    return float(str(value).split('/')[0])

df['rate'] = df['rate'].apply(clean_rate)
```

## 5.Exploratory Data Analysis (EDA)

1️⃣ Check for Missing Values

``` python

print(df.info())
```

2️⃣ Restaurant Type Distribution

``` python

sns.countplot(x=df['listed_in(type)'])
plt.xlabel("Type of Restaurant")
plt.show()```

🔹 Insight: Most restaurants belong to the dining category.

3️⃣ Most Voted Restaurant

```python

max_votes = df['votes'].max()
top_restaurant = df[df['votes'] == max_votes]['name']
print("Most voted restaurant:", top_restaurant.values[0]) ```


4️⃣ Online vs Offline Orders
`` python

sns.countplot(x=df['online_order'])
plt.show()
```
🔹 Insight: Most restaurants do not accept online orders.

5️⃣ Rating Distribution
``` python

plt.hist(df['rate'], bins=5)
plt.title('Ratings Distribution')
plt.show() ```

🔹 Insight: Most restaurants have ratings between 3.5 to 4.0.

6️⃣ Preferred Price Range
``` python

sns.countplot(x=df['approx_cost(for two people)'])
plt.show() ```

🔹 Insight: Couples mostly prefer restaurants with an approximate cost of ₹300.

7️⃣ Online vs Offline Order Ratings
``` python

sns.boxplot(x='online_order', y='rate', data=df)
plt.show()
```

🔹 Insight: Online orders tend to receive higher ratings than offline ones.

8️⃣ Heatmap for Online Orders vs Restaurant Type
``` python

pivot_table = df.pivot_table(index='listed_in(type)', columns='online_order', aggfunc='size', fill_value=0)
sns.heatmap(pivot_table, annot=True, cmap='YlGnBu', fmt='d')
plt.title('Heatmap of Online Orders by Restaurant Type')
plt.show()
```

🔹 Insight: Dining restaurants prefer offline orders, while cafes receive more online orders.

## Conclusion
a. Most restaurants do not accept online orders.
b. Dining restaurants are the most common category.
c. The most popular price range for couples is around ₹300.
d. Online orders tend to receive better ratings than offline orders.

