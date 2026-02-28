---
title: "Mastering Pandas Groupby for Data Analysis"
---

# Introduction

The `pandas` `groupby` function is one of the most powerful tools for summarizing and aggregating data in Python. It allows you to split your data into groups based on one or more keys, apply aggregation or transformation functions, and combine the results into a new DataFrame.  

## How `groupby` works

The following diagram shows the basic concept of splitting, applying functions, and combining results in `groupby`:

![Example of Pandas groupby output](images/groupby.webp "GroupBy tutorial illustration")

### Why is `pandas` `groupby` so important?

- Splitting Data into Meaningful Groups
    - `groupby` allows you to split your dataset based on one or more columns (keys).
        - Example: You can group sales data by store or by employee to analyze each subgroup separately.

- Aggregation Made Easy
    - Once you’ve grouped data, you can apply functions like sum(), mean(), count(), min(), max(), etc., to quickly get summaries.
        - Example: Calculate the total sales per store or the average sales per employee without manually filtering the data.

- Data Transformation
    - Beyond aggregation, groupby lets you transform data within each group while keeping the same structure.
        - Example: Normalize sales by dividing each employee’s sales by their store’s total sales.

- Flexibility with Complex Operations
    - You can use custom functions, multiple aggregations, or even combine groupby with apply() to perform complex operations on groups.
        - Example: Find the top 2 salespeople per store or calculate the weighted average for each group.

- Efficiency and Scalability
    - groupby is optimized for large datasets. Instead of looping through rows manually, it handles grouping operations internally, which is much faster and cleaner.


In this tutorial, you'll learn how to:

- Create groups in a DataFrame
- Apply aggregation and transformation functions
- Filter and rank groups
- Summarize multiple statistics at once

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

This DataFrame contains:

- Store: store identifier
- Employee: employee name
- Sales: total sales per employee
- Hours_Worked: hours worked by each employee

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

Either copy this tutorial code and run it on your own machine or experiment with groupby on your own datasets. Try combining multiple columns, applying different aggregation functions, and transforming groups to calculate percentages or rankings. Understanding groupby deeply will make your data analysis faster, cleaner, and more efficient.