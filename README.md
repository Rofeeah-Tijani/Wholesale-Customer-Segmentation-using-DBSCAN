# Wholesale-Customer-Segmentation-using-DBSCAN

This project performs customer segmentation on the UCI Wholesale Customers Dataset using DBSCAN clustering. The analysis focuses on identifying groups of similar customers based on their spending patterns across product categories

----

# Dataset Overview

The dataset contains information about wholesale customers, including the following attributes:

| Feature          | Description                                   |
|-----------------|-----------------------------------------------|
| Channel          | Customer channel (1 = Horeca, 2 = Retail)    |
| Region           | Customer region (integer-coded)             |
| Fresh            | Annual spending on fresh products            |
| Milk             | Annual spending on milk products             |
| Grocery          | Annual spending on grocery products          |
| Frozen           | Annual spending on frozen products           |
| Detergents_Paper | Annual spending on detergents and paper products |
| Delicassen       | Annual spending on delicatessen products    |

# Data Preprocessing

Before clustering, the dataset was carefully explored and cleaned:

1️⃣. Exploratory Steps:

Checked the shape of the dataset to understand its size.

Used info() to inspect data types and missing values.

Used describe() to examine summary statistics and detect anomalies or extreme values.

2️⃣. Feature Selection:

Dropped Channel and Region columns.

Reason: These are categorical variables, and DBSCAN uses distance metrics which work best with numeric, continuous features. Removing them ensures clustering focuses purely on spending behavior.

3️⃣. Standardization:

All remaining features (Fresh, Milk, Grocery, Frozen, Detergents_Paper, Delicassen) were standardized (zero mean, unit variance).

Reason: Prevents features with larger numeric ranges from dominating the clustering algorithm. Each category contributes equally to distance calculations.

-----

# DBSCAN Parameter Selection

Epsilon (eps) Selection using K-Distance Graph:

Computed distance to the k-th nearest neighbor, with k = minPts.

Plotted distances in ascending order and identified the “knee” point, which indicates a natural separation between dense regions and sparse noise points.

<img width="984" height="645" alt="Screenshot (508)" src="https://github.com/user-attachments/assets/62e670c1-5ba1-4e39-872d-6709cc6ee747" />


Minimum Points (minPts) Selection:

Chose minPts = number of features + 1 = 7.

Reason: Ensures that clusters have at least one more point than the data dimensionality, balancing cluster detection and noise filtering.

-----

# Cluster Mean Analysis

Below are the average spending per cluster for key categories:

| Cluster | Fresh   | Milk   | Grocery | Frozen | Detergents_Paper | Delicassen |
|---------|--------:|-------:|--------:|-------:|----------------:|-----------:|
| -1      | 30,161 | 26,872 | 33,576  | 12,380 | 14,612          | 8,185      |
| 0       | 11,270 | 4,949  | 6,921   | 2,698  | 2,410           | 1,257      |


<img width="1374" height="747" alt="Screenshot (509)" src="https://github.com/user-attachments/assets/ddbec050-8375-4d3b-b0e1-e50f7b896bc1" />


-----

# Interpretation:

Cluster -1:

Extremely high spending across all categories.

Likely large wholesale chains or high-volume customers.

Represent potential outliers relative to smaller clients.

Cluster 0:

Moderate spending in all categories.

Likely smaller businesses such as restaurants, cafés, or small retailers.

----

# Essence of the Cluster Column:

The Cluster column allows segmentation of customers into meaningful groups for targeted marketing, pricing strategies, and inventory planning. Noise points (-1) indicate exceptional customers who may require special attention or individualized service.

----

# Key Takeaways

Standardization is crucial for distance-based clustering to ensure fair contribution of all features.

K-distance graph is an effective way to choose eps in DBSCAN, capturing dense clusters while separating outliers.

Choosing minPts = number of features + 1 balances cluster detection with noise filtering.

Cluster means provide clear insights into customer behavior, highlighting high-value vs. moderate-value clients.

DBSCAN is particularly effective here because it identifies non-spherical clusters and outliers, unlike k-means.
