# Part 1


## Student Information

**Project:** Applied AI & ML Essentials Capstone Project  
**Part:** Part 1 – Data Acquisition, Cleaning, and Exploratory Data Analysis

---

# Dataset

For this project I used the **Bangalore Housing Prices Dataset**, which contains information about residential properties in Bangalore, India.

The dataset contains information such as:

- Area Type
- Availability
- Location
- Size
- Society
- Total Square Feet
- Number of Bathrooms
- Number of Balconies
- House Price

This dataset was selected because it contains both numerical and categorical variables, missing values, duplicate records, and enough observations to perform data cleaning and exploratory data analysis.

---

# Python Libraries Used

- pandas
- numpy
- matplotlib
- seaborn

---

# Data Cleaning

## Loading the Dataset

The dataset was loaded into a pandas DataFrame using:

```python
pd.read_csv()
```

The first five rows, column data types, and dataset shape were displayed before cleaning.

---

## Missing Value Analysis

Missing values were calculated for every column using:

```python
df.isnull().sum()
```

The percentage of missing values was also calculated.

Columns with less than 20% missing values were filled using the **median**.

I selected the median because it is less affected by extreme values and skewed distributions than the mean.

The **society** column contained over 20% missing values, so it was left unchanged.

---

## Duplicate Removal

Duplicate rows were identified using:

```python
df.duplicated().sum()
```

A total of **529 duplicate rows** were found and removed using:

```python
df.drop_duplicates()
```

After removing duplicates, the percentage of missing values remained essentially unchanged.

---

## Data Type Conversion

Some columns were stored with incorrect data types.

The **total_sqft** column was originally stored as an object because it contained ranges and measurement units.

A custom function was created to:

- convert ranges into their average value
- convert numeric values into float
- replace unsupported formats with NaN

The **area_type** column was converted to the **category** data type to reduce memory usage.

Memory usage was compared before and after conversion.

---

# Exploratory Data Analysis

## Descriptive Statistics

Descriptive statistics were generated using:

```python
df.describe()
```

Statistics included:

- Mean
- Median
- Standard Deviation
- Minimum
- Maximum
- Quartiles

---

## Skewness

Skewness was calculated for every numerical column.

The **total_sqft** column had the highest absolute skewness.

A positive skew means that a small number of very large values pull the distribution toward the right. Because of this, the median is a better measure of central tendency than the mean when filling missing values.

---

## Outlier Detection

Outliers were identified using the Interquartile Range (IQR) method.

The following columns were analyzed:

- Price
- Total Square Feet

Outliers were documented but were **not removed**.

They were retained because unusually large houses can represent legitimate observations rather than data errors.

---

# Visualizations

The following visualizations were created:

- Line Plot
- Bar Chart
- Histogram
- Scatter Plot
- Box Plot
- Correlation Heatmap

Each visualization includes titles and axis labels.

---

## Scatter Plot Interpretation

The scatter plot between **Total Square Feet** and **Price** shows a positive relationship.

In general, larger houses tend to have higher prices, although there is noticeable variation caused by other property characteristics.

---

## Box Plot Interpretation

The box plot compares house prices across different area types.

Different area types show different median prices and different spreads, indicating that area type influences property prices.

---

## Correlation Heatmap

Pearson correlation was calculated using:

```python
df.corr()
```

The strongest relationship was observed between **price** and **total_sqft**.

Although these variables are strongly correlated, correlation does not imply causation. Other factors such as location, number of bathrooms, amenities, and neighborhood quality may also influence house prices.

---

# Imputation Strategy

For the two most skewed numerical columns, both the mean and median were calculated before imputation.

Because these columns were positively skewed, the **median** was selected for missing value imputation.

After filling missing values, all remaining missing values in those columns were successfully removed.

---

# Spearman Correlation

A Spearman correlation matrix was computed and compared with the Pearson correlation matrix.

The three variable pairs with the largest differences between Pearson and Spearman correlations were identified.

Spearman correlation was used to detect monotonic relationships that Pearson correlation may underestimate.

---

# Grouped Aggregation

Grouped statistics were calculated using:

```python
groupby().agg(['mean','std','count'])
```

The analysis identified:

- Group with the highest average value
- Group with the highest standard deviation
- Ratio between the highest and lowest group means

This helped determine whether the categorical feature carries useful predictive information.

---

# Output Files

The cleaned dataset was saved as:

```
BHP_cleaned.csv
```

This cleaned dataset will be used in Parts 2, 3, and 4.

---

# Summary

During Part 1, the raw housing dataset was cleaned, explored, and visualized.

The dataset is now suitable for machine learning because duplicate rows were removed, incorrect data types were corrected, missing values were handled appropriately, and important relationships between variables were explored using statistical analysis and visualization.
