# Myntra Sales Data Analysis

## Project Overview

This project performs exploratory data analysis (EDA) on a Myntra sales dataset using Python. The analysis includes data loading, data quality checks, feature engineering, sales aggregation, and data visualization to uncover insights about monthly sales performance and category-wise revenue distribution.

## Features

* Load data from multiple Excel sheets
* Inspect dataset structure and summary statistics
* Detect duplicate records
* Create new calculated fields
* Analyze monthly sales trends
* Analyze revenue contribution by product category
* Visualize results using bar charts and pie charts

---

## Dataset

The project uses an Excel file named:

```text
Myntra dataset.xlsx
```

The workbook contains the following sheets:

| Sheet Name      | Description            |
| --------------- | ---------------------- |
| `dim_products`  | Product details        |
| `dim_customers` | Customer information   |
| `fact_orders`   | Order transaction data |

---

## Technologies Used

* Python
* Pandas
* NumPy
* Matplotlib
* Seaborn

Install the required libraries using:

```bash
pip install pandas numpy matplotlib seaborn openpyxl
```

---

## Project Workflow

### 1. Load Data

The script reads data from the Excel workbook into three DataFrames:

```python
products
customers
orders
```

### 2. Data Exploration

The following methods are used to understand the datasets:

```python
.info()
.describe()
```

These provide information about:

* Data types
* Missing values
* Number of records
* Statistical summaries

### 3. Duplicate Detection

The script checks for duplicate records in all tables:

```python
products.duplicated()
customers.duplicated()
orders.duplicated()
```

It also calculates the total number of duplicate rows:

```python
products.duplicated().sum()
customers.duplicated().sum()
orders.duplicated().sum()
```

### 4. Data Cleaning

Duplicate rows are removed from the products table:

```python
products.drop_duplicates()
```

### 5. Feature Engineering

#### Extract Month from Order Date

A new column called `Month` is created from the order date:

```python
orders["Month"] = orders["Date"].dt.strftime("%B")
```

#### Calculate Total Price After Discount

A new column called `Total Price` is created:

```python
orders["Total Price"] = (
    orders["Original Price"] -
    (orders["Original Price"] * orders["Discount%"])
)
```

---

## Analysis Performed

### Monthly Sales Analysis

Monthly sales are calculated using:

```python
gb = orders.groupby("Month").agg({
    "Original Price": "sum"
})
```

#### Visualization

A Seaborn bar chart displays total sales by month.

**Insights:**

* Identifies high-performing months
* Highlights seasonal sales trends

---

### Category-wise Revenue Analysis

Orders and product information are merged using:

```python
df = pd.merge(
    left=orders,
    right=products,
    on="Product ID",
    how="inner"
)
```

Revenue is then aggregated by product category:

```python
gb1 = df.groupby("Category").agg({
    "Total Price": "sum"
})
```

#### Visualization

A pie chart shows the percentage contribution of each category to total revenue.

**Insights:**

* Identifies top-performing categories
* Shows category contribution to overall sales

---

## Output

The script generates:

### Reports

* Dataset information
* Summary statistics
* Duplicate counts
* Monthly sales totals
* Category-wise revenue totals

### Visualizations

1. Monthly Sales Bar Chart
2. Category Revenue Pie Chart

### Revenue Calculation

Total revenue after discounts:

```python
df["Total Price"].sum()
```

---

## Project Structure

```text
Myntra-Sales-Analysis/
│
├── Myntra dataset.xlsx
├── analysis.py
└── README.md
```

---

## How to Run

1. Place `Myntra dataset.xlsx` in the project directory.
2. Install required libraries.
3. Run the Python script:

```bash
python analysis.py
```

4. View the generated charts and analysis results.

---

## Business Questions Answered

* Which months generate the highest sales?
* How do discounts affect total revenue?
* Which product categories contribute the most revenue?
* Are there duplicate records in the dataset?

---

## Future Enhancements

* Handle missing values and outliers
* Save cleaned datasets to new files
* Create interactive dashboards using Power BI or Plotly
* Perform customer segmentation analysis
* Build sales forecasting models
* Analyze discount effectiveness

---

## Author

**Myntra Sales Data Analysis Project**

A Python-based exploratory data analysis project for understanding sales performance, customer behavior, and product category revenue using Pandas, Matplotlib, and Seaborn.
