---
title: "Mastering Pandas Groupby for Data Analysis"
---

# Introduction

The `pandas` `groupby` function is one of the most powerful tools for summarizing and aggregating data in Python. It allows you to split your data into groups based on one or more keys, apply aggregation or transformation functions, and combine the results into a new DataFrame.  

This tutorial will guide you through creating groups, applying common aggregations, and performing advanced transformations — all without needing to load an external dataset.

## Creating a Sample Dataset

We’ll start by creating a simple DataFrame with sales data for a small store:

```python
import pandas as pd

data = {
    'Store': ['A', 'A', 'B', 'B', 'C', 'C', 'C'],
    'Employee': ['Alice', 'Bob', 'Charlie', 'Diana', 'Eve', 'Frank', 'Grace'],
    'Sales': [250, 200, 150, 300, 400, 350, 200],
    'Hours_Worked': [8, 7, 8, 6, 9, 8, 7]
}

df = pd.DataFrame(data)
df
```

## Basic GroupBy

You could group the data by the Store column and calculate the total sales per store:

``` python
store_sales = df.groupby('Store')['Sales'].sum()
store_sales
```

- df.groupby('Store') splits the DataFrame into groups based on the Store column.
- ['Sales'] selects the column to aggregate.
- .sum() computes the sum of sales for each group.

You could also group the data by the Store column and calculate the total hours worked per store:

``` python
store_hours = df.groupby('Store')['Hours_Worked'].sum()
store_hours
```

- df.groupby('Store') splits the DataFrame into groups based on the Store column.
- ['Hours_Worked'] selects the column we want to aggregate.
- .sum() computes the total hours worked for each store.


## Multiple Aggregations

You can compute multiple statistics at once using .agg():

``` python
store_summary = df.groupby('Store').agg(
    total_sales=('Sales', 'sum'),
    average_sales=('Sales', 'mean'),
    total_hours=('Hours_Worked', 'sum')
)
store_summary
```

- You can pass a dictionary of {new_column_name: (column_to_aggregate, function)} to .agg().
- Supports multiple aggregation functions at once.


## GroupBy Multiple Columns

Grouping by multiple keys is also straightforward. Suppose we want average sales by store and employee:

``` python 
employee_summary = df.groupby(['Store', 'Employee'])['Sales'].mean()
employee_summary
```
Each combination of Store and Employee is treated as a separate group.


## Filtering Groups

You can filter groups using .filter(). For example, only keep stores with total sales greater than 500:

```python
high_sales_stores = df.groupby('Store').filter(lambda x: x['Sales'].sum() > 500)
high_sales_stores
```


## Transforming Groups

.transform() allows you to perform operations that return an array of the same length as the original DataFrame. For example, calculate each employee's sales as a percentage of their store's total sales:

``` python
df['Sales_Percent'] = df.groupby('Store')['Sales'].transform(lambda x: x / x.sum() * 100)
df
```
Useful for normalization and creating new columns based on group-level calculations.


## Summary Table of Common GroupBy Methods

| Method      | Purpose                             |
|:-----------:|:-----------------------------------:|
|.sum()       | sum values within a group           |
|.mean()      | average values within each group    |
|.agg()       | multiple aggregations at once       |
|.filter()    | keep groups that satisfy a condition|
|.transform() | transform values while keeping shape|


## Try it yourself! 

Experiment with groupby on your own datasets. Try combining multiple columns, applying different aggregation functions, and transforming groups to calculate percentages or rankings. Understanding groupby deeply will make your data analysis faster, cleaner, and more efficient.