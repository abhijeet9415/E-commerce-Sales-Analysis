
# E-Commerce Sales Analysis

## Description
This project focuses on analyzing e-commerce sales data by extracting key insights using both SQL queries and Python. It leverages MySQL for data extraction and Python libraries such as Pandas, Matplotlib, and Seaborn for data cleaning, exploratory data analysis (EDA), and visualization. The goal is to uncover customer purchasing behavior and provide data-driven recommendations to enhance sales performance.

## Table of Contents
- [Installation](#installation)
- [Usage](#usage)
- [Features](#features)
- [Data](#data)
- [SQL Integration](#sql-integration)
- [Visual Analysis](#visual-analysis)
- [Results](#results)


## Installation

1. **Clone the repository**:
    ```bash
    git clone https://github.com/yourusername/ecommerce-sales-analysis.git
    ```

2. **Navigate to the project folder**:
    ```bash
    cd ecommerce-sales-analysis
    ```

3. **Install the required dependencies**:
    ```bash
    pip install -r requirements.txt
    ```

4. **Run the Jupyter Notebook**:
    ```bash
    jupyter notebook ecommerce_analysis.ipynb
    ```

5. **Set up MySQL Database**:
    Ensure you have MySQL installed and set up on your system. Import the dataset into a MySQL database and configure your connection credentials.

## Usage

1. **Open the Jupyter Notebook**: You can explore the notebook `ecommerce_analysis.ipynb` to review the analysis, visualizations, SQL queries, and key findings.
   
2. **Explore the Data**: Use the notebook to explore customer purchasing behavior, sales trends, and customer segmentation.

## Features
- **Data Extraction with SQL**: Connects to a MySQL database to retrieve e-commerce sales data using SQL queries.
- **Data Cleaning**: Processes missing values and handles outliers to ensure data quality.
- **Exploratory Data Analysis (EDA)**: Analyzes key features such as product categories, customer demographics, sales volume, and transaction trends.
- **Sales Trends Analysis**: Evaluates sales performance across different time periods, product categories, and regions.
- **Visual Analysis**: Uses visualizations to interpret trends, outliers, and relationships between key variables.

## Data

The dataset used for the analysis includes the following columns:

- **Customer ID**: Unique identifier for each customer.
- **Product ID**: Unique identifier for each product.
- **Order Date**: The date when the order was placed.
- **Sales**: The total sales amount for each transaction.
- **Quantity**: Number of units sold.
- **Profit**: The profit generated from each transaction.
- **Category**: The category to which each product belongs.

## SQL Integration

Data is extracted from the MySQL database using the `mysql-connector-python` library. Here's an example of how the connection to the MySQL server is established:

```python
import mysql.connector
import pandas as pd

# Connect to MySQL
conn = mysql.connector.connect(
    host='localhost',
    user='your_username',
    password='your_password',
    database='ecommerce_db'
)

# Query to extract data
query = "SELECT * FROM sales_data WHERE order_date BETWEEN '2023-01-01' AND '2023-12-31'"

# Load data into a DataFrame
data = pd.read_sql(query, conn)

# Close the connection
conn.close()
```

The data is then processed in Python for further analysis and visualization.

## Visual Analysis

Key visualizations from the project:

### 1. Sales Over Time
A line plot to show sales trends over time, helping to identify peak periods and sales fluctuations.

```python
import matplotlib.pyplot as plt
import seaborn as sns

# Plot Sales Over Time
plt.figure(figsize=(10,6))
data['Order Date'] = pd.to_datetime(data['Order Date'])
sales_over_time = data.groupby('Order Date')['Sales'].sum()
plt.plot(sales_over_time)
plt.title('Sales Over Time')
plt.xlabel('Date')
plt.ylabel('Sales')
plt.show()
```

### 2. Top-Selling Products
A bar plot that highlights the top 10 products with the highest sales.

```python
# Plot Top-Selling Products
top_products = data.groupby('Product ID')['Sales'].sum().nlargest(10)
plt.figure(figsize=(10,6))
sns.barplot(x=top_products.values, y=top_products.index)
plt.title('Top 10 Best-Selling Products')
plt.xlabel('Sales')
plt.ylabel('Product ID')
plt.show()
```

### 3. Profit by Product Category
A bar plot to show profit distribution across various product categories.

```python
# Plot Profit by Product Category
plt.figure(figsize=(10,6))
sns.barplot(x='Category', y='Profit', data=data, palette='Set2')
plt.title('Profit by Product Category')
plt.xlabel('Category')
plt.ylabel('Profit')
plt.show()
```

### 4. Heatmap of Correlations
A heatmap showing correlations between sales, quantity, profit, and discount to explore relationships between key variables.

```python
# Heatmap of correlations
plt.figure(figsize=(10,8))
sns.heatmap(data.corr(), annot=True, cmap='coolwarm', linewidths=0.5)
plt.title('Correlation Heatmap')
plt.show()
```

## Results

- **Key Insights**:
  - The analysis identified the top-selling products and most profitable categories.
  - Seasonal trends and high-demand periods were detected in the sales data.
  - Products with higher discounts saw an increase in sales but a reduction in profit margins.
  
- **Recommendations**:
  - Focus on promoting high-margin products.
  - Optimize discount strategies to balance sales volume and profitability.
  - Introduce targeted marketing during high-demand periods to maximize sales.
