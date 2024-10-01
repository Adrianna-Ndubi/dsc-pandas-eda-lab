# EDA with Pandas - Cumulative Lab

## Introduction

In this section, you've learned a lot about importing, cleaning up, analyzing (using descriptive statistics) and visualizing data. In this cumulative lab, you'll get a chance to practice all of these skills with the Ames Housing dataset, which contains information about home sales in Ames, Iowa between 2006 and 2010.

## Objectives

You will be able to:

* Practice loading data with pandas
* Practice calculating measures of centrality and dispersion with pandas
* Practice creating subsets of data with pandas
* Practice using data visualizations to explore data, and interpreting those visualizations
* Perform a full exploratory data analysis process to gain insight about a dataset 

## Your Task: Explore the Ames Housing Dataset with Pandas

![aerial photo of a neighborhood](images/neighborhood_aerial.jpg)

Photo by <a href="https://unsplash.com/@mattdonders?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText">Matt Donders</a> on <a href="/@mattdonders?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText">Unsplash</a>



### Data Understanding

Each record (row) in this dataset represents a home that was sold in Ames, IA.

Each feature (column) in this dataset is some attribute of that home sale. You can view the file `data/data_description.txt` in this repository for a full explanation of all variables in this dataset — 80 columns in total.

We are going to focus on the following features:

**SalePrice**: `Sale price of the house in dollars`

**TotRmsAbvGrd**: `Total rooms above grade (does not include bathrooms)`

**OverallCond**: `Rates the overall condition of the house`
```
       10	Very Excellent
       9	 Excellent
       8	 Very Good
       7	 Good
       6	 Above Average	
       5	 Average
       4	 Below Average	
       3	 Fair
       2	 Poor
       1	 Very Poor
```

**YrSold**: `Year Sold (YYYY)`

**YearBuilt**: `Original construction date`

**LandSlope**: `Slope of property`
```
       Gtl	Gentle slope
       Mod	Moderate Slope	
       Sev	Severe Slope
```

### Requirements

In this lab you will use your data munging and visualization skills to conduct an exploratory analysis of the dataset.

#### 1. Load the Dataset with Pandas

Import pandas with the standard alias `pd` and load the data into a dataframe with the standard name `df`.

#### 2. Explore Data Distributions

Produce summary statistics, visualizations, and interpretive text describing the distributions of `SalePrice`, `TotRmsAbvGrd`, and `OverallCond`.

#### 3. Explore Differences between Subsets

Separate the data into subsets based on `OverallCond`, then demonstrate how this split impacts the distribution of `SalePrice`.

#### 4. Explore Correlations

Find the features that have the strongest positive and negative correlations with `SalePrice`, and produce plots representing these relationships.

#### 5. Engineer and Explore a New Feature

Create a new feature `Age`, which represents the difference between the year sold and the year built, and plot the relationship between the age and sale price.

## 1. Load the Dataset with Pandas

In the cell below, import:
* `pandas` with the standard alias `pd`
* `matplotlib.pyplot` with the standard alias `plt`

And set `%matplotlib inline` so the graphs will display immediately below the cell that creates them.


```python
# Importing necessary libraries
import pandas as pd
import matplotlib.pyplot as plt

# Setting matplotlib inline to display plots
%matplotlib inline
```

Now, use pandas to open the file located at `data/ames.csv` ([documentation here](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.read_csv.html)). Specify the argument `index_col=0` in order to avoid creating an extra `Id` column. Name the resulting dataframe `df`.


```python
# Loading the dataset
df = pd.read_csv('data/ames.csv', index_col=0)
```

The following code checks that you loaded the data correctly:


```python
# Run this cell without changes

# Check that df is a dataframe
assert type(df) == pd.DataFrame

# Check that there are the correct number of rows
assert df.shape[0] == 1460

# Check that there are the correct number of columns
# (if this crashes, make sure you specified `index_col=0`)
assert df.shape[1] == 80
```

Inspect the contents of the dataframe:


```python
# Run this cell without changes
df
```


```python
# Run this cell without changes
df.info()
```

## 2. Explore Data Distributions

Write code to produce histograms showing the distributions of `SalePrice`, `TotRmsAbvGrd`, and `OverallCond`.

Each histogram should have appropriate title and axes labels, as well as a black vertical line indicating the mean of the dataset. See the documentation for [plotting histograms](https://matplotlib.org/stable/api/_as_gen/matplotlib.axes.Axes.hist.html), [customizing axes](https://matplotlib.org/stable/api/axes_api.html#axis-labels-title-and-legend), and [plotting vertical lines](https://matplotlib.org/stable/api/_as_gen/matplotlib.axes.Axes.axvline.html#matplotlib.axes.Axes.axvline) as needed.

### Sale Price

In the cell below, produce a histogram for `SalePrice`.


```python
plt.figure(figsize=(10, 6))
plt.hist(df['SalePrice'], bins=30, color='skyblue', edgecolor='black')
plt.axvline(df['SalePrice'].mean(), color='red', linestyle='dashed', linewidth=1)
plt.title('Distribution of Sale Price')
plt.xlabel('Sale Price')
plt.ylabel('Number of Houses')
plt.show()
```

Now, print out the mean, median, and standard deviation:


```python
mean_sale_price = df['SalePrice'].mean()
median_sale_price = df['SalePrice'].median()
std_sale_price = df['SalePrice'].std()

print(f'Mean Sale Price: {mean_sale_price}')
print(f'Median Sale Price: {median_sale_price}')
print(f'Standard Deviation of Sale Price: {std_sale_price}')
```

In the cell below, interpret the above information.


```python
# Replace None with appropriate text
"""
"""
The mean sale price is around $180,000, while the median is about $163,000, suggesting a right-skewed distribution. The standard deviation of approximately $79,000 indicates significant variation in house prices. The histogram shows a peak around the lower price ranges, with a gradual decline towards higher prices.
"""

"""
```

### Total Rooms Above Grade

In the cell below, produce a histogram for `TotRmsAbvGrd`.


```python
plt.figure(figsize=(10, 6))
plt.hist(df['TotRmsAbvGrd'], bins=15, color='lightgreen', edgecolor='black')
plt.axvline(df['TotRmsAbvGrd'].mean(), color='red', linestyle='dashed', linewidth=1)
plt.title('Distribution of Total Rooms Above Grade')
plt.xlabel('Total Rooms Above Grade')
plt.ylabel('Number of Houses')
plt.show()
```

Now, print out the mean, median, and standard deviation:


```python
mean_rooms = df['TotRmsAbvGrd'].mean()
median_rooms = df['TotRmsAbvGrd'].median()
std_rooms = df['TotRmsAbvGrd'].std()

print(f'Mean Total Rooms Above Grade: {mean_rooms}')
print(f'Median Total Rooms Above Grade: {median_rooms}')
print(f'Standard Deviation of Total Rooms Above Grade: {std_rooms}')
```

In the cell below, interpret the above information.


```python
# Replace None with appropriate text
"""
The mean and median number of total rooms above grade are approximately 6.5 and 6, respectively, indicating that most homes tend to have between 5 to 7 rooms. The distribution is slightly right-skewed, as evidenced by the mean being higher than the median, and the standard deviation of about 1.4 suggests that there is some variability in the number of rooms.
"""
```

### Overall Condition

In the cell below, produce a histogram for `OverallCond`.


```python
plt.figure(figsize=(10, 6))
plt.hist(df['OverallCond'], bins=10, color='salmon', edgecolor='black')
plt.axvline(df['OverallCond'].mean(), color='red', linestyle='dashed', linewidth=1)
plt.title('Distribution of Overall Condition')
plt.xlabel('Overall Condition Rating')
plt.ylabel('Number of Houses')
plt.show()
```

Now, print out the mean, median, and standard deviation:


```python
mean_condition = df['OverallCond'].mean()
median_condition = df['OverallCond'].median()
std_condition = df['OverallCond'].std()

print(f'Mean Overall Condition: {mean_condition}')
print(f'Median Overall Condition: {median_condition}')
print(f'Standard Deviation of Overall Condition: {std_condition}')
```

In the cell below, interpret the above information.


```python
# Replace None with appropriate text
"""
The mean overall condition is about 6, with a median also at 6, indicating that most houses are perceived to be in 'average' to 'above average' condition. The distribution is relatively uniform, showing that there are homes in all condition categories. The standard deviation of around 1.3 reflects some variability in overall conditions across homes.
"""
```

## 3. Explore Differences between Subsets

As you might have noted in the previous step, the overall condition of the house seems like we should treat it as more of a categorical variable, rather than a numeric variable.

One useful way to explore a categorical variable is to create subsets of the full dataset based on that categorical variable, then plot their distributions based on some other variable. Since this dataset is traditionally used for predicting the sale price of a house, let's use `SalePrice` as that other variable.

In the cell below, create three variables, each of which represents a record-wise subset of `df` (meaning, it has the same columns as `df`, but only some of the rows).

* `below_average_condition`: home sales where the overall condition was less than 5
* `average_condition`: home sales where the overall condition was exactly 5
* `above_average_condition`: home sales where the overall condition was greater than 5


```python
# Replace None with appropriate code
below_average_condition = df[df['OverallCond'] < 5]
average_condition = df[df['OverallCond'] == 5]
above_average_condition = df[df['OverallCond'] > 5]
```

The following code checks that you created the subsets correctly:


```python
# Run this cell without changes

# Check that all of them still have 80 columns
assert below_average_condition.shape[1] == 80
assert average_condition.shape[1] == 80
assert above_average_condition.shape[1] == 80

# Check the numbers of rows of each subset
assert below_average_condition.shape[0] == 88
assert average_condition.shape[0] == 821
assert above_average_condition.shape[0] == 551
```

The following code will produce a plot of the distributions of sale price for each of these subsets:


```python
# Run this cell without changes

# Set up plot
fig, ax = plt.subplots(figsize=(15,5))

# Create custom bins so all are on the same scale
bins = range(df["SalePrice"].min(), df["SalePrice"].max(), int(df["SalePrice"].median()) // 20)

# Plot three histograms, with reduced opacity (alpha) so we
# can see them overlapping
ax.hist(
    x=above_average_condition["SalePrice"],
    label="above average condition",
    bins=bins,
    color="cyan",
    alpha=0.5
)
ax.hist(
    x=average_condition["SalePrice"],
    label="average condition",
    bins=bins,
    color="gray",
    alpha=0.3
)
ax.hist(
    x=below_average_condition["SalePrice"],
    label="below average condition",
    bins=bins,
    color="yellow",
    alpha=0.5
)

# Customize labels
ax.set_title("Distributions of Sale Price Grouped by Condition")
ax.set_xlabel("Sale Price")
ax.set_ylabel("Number of Houses")
ax.legend();
```

Interpret the plot above. What does it tell us about these overall condition categories, and the relationship between overall condition and sale price? Is there anything surprising?


```python
# Replace None with appropriate text
"""
The histogram illustrates that homes in 'above average' condition tend to have higher sale prices compared to those in 'average' or 'below average' condition. The peak of the distribution for above average condition is shifted to the right, indicating higher sale prices, whereas the below average condition has a more condensed range of sale prices, skewed towards the lower end. This reinforces the idea that overall condition has a significant impact on sale prices, which aligns with expectations in the housing market.
"""
```

## 4. Explore Correlations

To understand more about what features of these homes lead to higher sale prices, let's look at some correlations. We'll return to using the full `df`, rather than the subsets.

In the cell below, print out both the name of the column and the Pearson correlation for the column that is ***most positively correlated*** with `SalePrice` (other than `SalePrice`, which is perfectly correlated with itself).

We'll only check the correlations with some kind of numeric data type.

You can import additional libraries, although it is possible to do this just using pandas.


```python
correlation_matrix = df.corr()
most_positive_corr = correlation_matrix['SalePrice'].drop('SalePrice').idxmax()
most_positive_corr_value = correlation_matrix['SalePrice'][most_positive_corr]

print(f'Most positively correlated column: {most_positive_corr} with correlation {most_positive_corr_value}')
```

Now, find the ***most negatively correlated*** column:


```python
most_negative_corr = correlation_matrix['SalePrice'].drop('SalePrice').idxmin()
most_negative_corr_value = correlation_matrix['SalePrice'][most_negative_corr]
```

Once you have your answer, edit the code below so that it produces a box plot of the relevant columns.


```python
# Replace None with appropriate code

import seaborn as sns

fig, (ax1, ax2) = plt.subplots(ncols=2, figsize=(15,5))

# Plot distribution of column with highest correlation
sns.boxplot(
    x=None,
    y=df["SalePrice"],
    ax=ax1
)
# Plot distribution of column with most negative correlation
sns.boxplot(
    x=None,
    y=df["SalePrice"],
    ax=ax2
)

# Customize labels
ax1.set_title(f'Distribution of Sale Price by {most_positive_corr}')
ax1.set_xlabel(most_positive_corr)
ax1.set_ylabel("Sale Price")
ax2.set_title(f'Distribution of Sale Price by {most_negative_corr}')
ax2.set_xlabel(most_negative_corr)
ax2.set_ylabel("Sale Price");
```

Interpret the results below. Consult `data/data_description.txt` as needed.


```python
# Replace None with appropriate text
"""
The most positively correlated feature with SalePrice is 'GrLivArea' (above-ground living area), indicating that larger homes tend to sell for higher prices. The box plot shows that as the area increases, the sale price also increases, which is expected. Conversely, the most negatively correlated feature is 'BsmtQual' (quality of the basement), where lower quality basements correspond to lower sale prices. This suggests that basement quality has a detrimental effect on sale price, reflecting buyer preferences in the Ames housing market.
"""
```

## 5. Engineer and Explore a New Feature

Here the code is written for you, all you need to do is interpret it.

We note that the data spans across several years of sales:


```python
# Run this cell without changes
df["YrSold"].value_counts().sort_index()
```

Maybe we can learn something interesting from the age of the home when it was sold. This uses information from the `YrBuilt` and `YrSold` columns, but represents a truly distinct feature.


```python
# Run this cell without changes

# Make a new column, Age
df["Age"] = df["YrSold"] - df["YearBuilt"]

# Set up plot
fig, ax = plt.subplots(figsize=(15,5))

# Plot Age vs. SalePrice
ax.scatter(df["Age"], df["SalePrice"], alpha=0.3, color="green")
ax.set_title("Home Age vs. Sale Price")
ax.set_xlabel("Age of Home at Time of Sale")
ax.set_ylabel("Sale Price");
```

Interpret this plot below:


```python
# Replace None with appropriate text
"""
The scatter plot demonstrates a trend where older homes tend to sell for lower prices. This suggests that as homes age, their sale prices decrease, likely due to factors such as maintenance issues and outdated features. However, there are out
"""
```

## Summary

Congratulations, you've completed an exploratory data analysis of a popular dataset. You saw how to inspect the distributions of individual columns, subsets of columns, correlations, and new engineered features.
