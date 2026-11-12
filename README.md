# Customer Segmentation Using RFM Analysis and K-Means Clustering

## Project Overview

This project focuses on customer segmentation using transactional retail data. The goal is to identify distinct customer groups based on their purchasing behavior and develop data-driven business strategies to improve customer retention, increase purchase frequency, and maximize revenue.

The project applies **RFM Analysis (Recency, Frequency, Monetary)** and **K-Means Clustering** to segment customers into meaningful groups.

## Objectives

- Analyze customer purchasing behavior using transactional data.
- Perform data cleaning and exploratory data analysis.
- Calculate Recency, Frequency, and Monetary metrics..
- Transform and scale features to prepare them for clustering.
- Apply K-Means clustering to identify customer segments.
- Evaluate clustering performance using multiple metrics.
- Visualize customer segments using PCA.
- Develop actionable business recommendations for each segment.

## Tools & Technologies

- **Python** – Data analysis and machine learning
- **Polars** – Data manipulation and preprocessing
- **NumPy** – Numerical computations
- **Matplotlib** – Data visualization
- **Scikit-learn** – Feature scaling, PCA, and K-Means clustering
- **Jupyter Notebook** – Interactive analysis

## Dataset

This project uses the first part of the **Online Retail II** dataset from the UCI Machine Learning Repository.

- **Source:** [UCI Machine Learning Repository – Online Retail II](https://archive.ics.uci.edu/dataset/502/online+retail+ii)
- **Creator:** Daqing Chen
- **Time Period Used:** December 1, 2009 – December 9, 2010
- **Original Records Used:** 525,461
- **Features:** 8

The dataset contains transactional records from a UK-based online retailer, including invoice details, product information, quantities, prices, customer IDs, and countries.

After data cleaning and preprocessing, customer-level RFM analysis was performed on **4,314 unique customers**.

**Dataset Citation:**

Chen, D. (2012). *Online Retail II* [Dataset]. UCI Machine Learning Repository. https://doi.org/10.24432/C5CG6D

## Project Workflow

### 1. Data Cleaning & Preprocessing

The dataset was inspected and prepared for analysis through the following steps:

- Identified and removed 13,283 duplicate records.
- Identified missing values in Customer ID.
- Removed records with missing Customer ID, as customer-level segmentation requires customer identification.
- Examined negative quantities and retained the original records separately from the RFM analysis.
- Excluded negative-quantity transactions from RFM calculations to focus on actual purchases.
- Investigated zero-value transactions and identified test-product records.

### 2. Exploratory Data Analysis (EDA)

Exploratory analysis was performed to understand the dataset's structure and purchasing patterns.

Key areas included:
- Transaction and customer distributions.
- Purchase quantities and monetary values.
- Negative and zero-value transactions.
- Distribution and skewness of RFM metrics.

### 3. RFM Analysis

Three customer-level metrics were calculated:

| Metric | Definition |
|---|---|
| Recency | Number of days since the customer's most recent purchase |
| Frequency | Number of unique invoices per customer |
| Monetary | Total monetary value of customer purchases |

The reference date was set to **December 10, 2010**, one day after the latest invoice date in the analyzed data.

### 4. Feature Transformation & Scaling

The distributions of Frequency and Monetary showed substantial positive skewness.

Log transformation was applied to Frequency and Monetary to reduce skewness. Recency was retained in its original form.

Two scaling techniques were evaluated:

- StandardScaler
- RobustScaler

RobustScaler was selected for the final clustering model based on the comparative evaluation results.

### 5. K-Means Clustering

K-Means models with different numbers of clusters (k = 2 to 10) were evaluated.

The following metrics were used:

- **Inertia:** Measures within-cluster sum of squared distances.
- **Silhouette Score:** Evaluates cluster cohesion and separation.
- **Davies-Bouldin Index:** Measures similarity between clusters.
- **Calinski-Harabasz Index:** Evaluates the ratio of between-cluster dispersion to within-cluster dispersion.

The final model used:

- Algorithm: K-Means
- Number of clusters: 3
- Scaler: RobustScaler
- Random State: 42
- Number of Initializations: 10

### 6. Model Evaluation

The selected model achieved the following results:

| Metric | Score |
|---|---:|
| Silhouette Score | 0.4160 |
| Davies-Bouldin Index | 0.8176 |
| Calinski-Harabasz Index | 4416.21 |

The results indicate a reasonable clustering structure, with three customer groups exhibiting distinct purchasing behaviors.

### 7. PCA Visualization

Principal Component Analysis (PCA) was used to reduce the three-dimensional scaled RFM feature space to two dimensions for visualization.

| Component | Explained Variance |
|---|---:|
| PC1 | 69.91% |
| PC2 | 24.87% |
| **Total** | **94.78%** |

The two principal components preserve approximately 94.78% of the total variance, providing a useful two-dimensional representation of the customer segments.

## Customer Segmentation Results

The final K-Means model identified three customer segments:

| Customer Segment | Customers | Customer Share | Average Recency | Average Frequency | Average Monetary |
|---|---:|---:|---:|---:|---:|
| At-Risk Customers | 967 | 22.42% | 249.52 | 1.46 | 442.32 |
| Occasional Customers | 1,963 | 45.50% | 53.90 | 2.09 | 594.63 |
| High-Value Customers | 1,384 | 32.08% | 33.71 | 9.90 | 5,204.66 |

### Segment 1: At-Risk Customers

- Represent 22.42% of the customer base.
- Have the highest average Recency (approximately 250 days).
- Show low purchase frequency and monetary value.

**Recommended Strategy:**
- Targeted win-back campaigns.
- Personalized discounts and reactivation offers.
- Product recommendations based on previous purchases.

### Segment 2: Occasional Customers

- Represent 45.50% of the customer base.
- Have an average purchase frequency of approximately 2.09 invoices.
- Contribute 13.27% of total revenue.

**Recommended Strategy:**
- Encourage repeat purchases.
- Introduce loyalty incentives.
- Apply cross-selling and personalized product recommendations.

### Segment 3: High-Value Customers

- Represent 32.08% of the customer base.
- Have the highest purchase frequency and monetary value.
- Generate 81.87% of total revenue.

**Recommended Strategy:**
- VIP loyalty programs.
- Exclusive offers and early access to new products.
- Personalized promotions and customer retention initiatives.

## Key Business Insights

1. **High-Value Customers drive the majority of revenue.** Although they represent only 32.08% of customers, they generate 81.87% of total revenue.

2. **Occasional Customers represent the largest segment.** Accounting for 45.50% of customers but contributing only 13.27% of revenue, this group offers an opportunity to increase purchase frequency and customer value.

3. **At-Risk Customers show limited recent engagement.** They account for 22.42% of customers and contribute 4.86% of revenue, making targeted reactivation campaigns a potential retention strategy.

### Overall Business Recommendation

The business should prioritize retaining High-Value Customers, increasing the purchase frequency of Occasional Customers, and selectively reactivating At-Risk Customers.

Since High-Value Customers generate approximately 82% of total revenue, protecting this segment should be a major customer retention priority.

## Conclusion

This project demonstrates how RFM analysis and unsupervised machine learning can be combined to identify meaningful customer segments from transactional retail data.

By applying data preprocessing, feature transformation, scaling, K-Means clustering, and PCA, the analysis identified three distinct customer groups with different purchasing behaviors and business value.

The resulting segments provide actionable insights that can support customer retention, targeted marketing, and revenue optimization strategies.

---

*This project was developed as part of my data analytics and machine learning portfolio.*