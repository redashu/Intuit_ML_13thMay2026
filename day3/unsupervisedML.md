# Unsupervised Learning

## The Big Difference: Supervised vs Unsupervised

### Supervised Learning

Uses **labeled data**.

Example:

| Features | Target |
|---|---|
| Experience | Salary |

The model learns an input-to-output mapping.

### Unsupervised Learning

Uses data with **no target column**.

Goal: discover hidden patterns automatically.

## Real-World Analogy

Suppose a company has 10 lakh customers but no labels like:

- Premium
- Regular
- Risky

Can ML automatically group similar customers? Yes. That is **clustering**.

## Most Important Concept

Unsupervised learning tries to answer:

> What hidden structure exists inside data?

## Best Real-World Use Cases

| Use Case | Purpose |
|---|---|
| Customer segmentation | Group customers |
| Fraud anomaly detection | Detect unusual behavior |
| Recommendation systems | Similar user grouping |
| Market basket analysis | Buying pattern discovery |

## Main Topic: K-Means Clustering

### What Is K-Means?

K-Means is a clustering algorithm that groups similar data points together.

### Real-World Example

Suppose a shopping mall wants to group customers based on:

- Income
- Spending score

K-Means may discover:

| Cluster | Customer Type |
|---|---|
| Cluster 1 | Budget shoppers |
| Cluster 2 | Premium customers |
| Cluster 3 | Moderate spenders |

This happens without predefined labels.

### Why Is It Called K-Means?

| Part | Meaning |
|---|---|
| K | Number of clusters |
| Means | Cluster center (average) |

### Core Working Logic

K-Means works by:

- Finding cluster centers
- Grouping points to their nearest center

## K-Means Algorithm Steps

### Step 1: Choose K

Example: K = 3 means create 3 clusters.

### Step 2: Randomly Initialize Centroids

Centroid = cluster center.

### Step 3: Assign Points to Nearest Centroid

Uses distance calculation, usually **Euclidean distance**:

$$
d = \sqrt{(x_2 - x_1)^2 + (y_2 - y_1)^2}
$$

Example:

- A(6, 6)
- B(-6, -6)
- $\Delta x = 12$, $\Delta y = 12$
- $d = \sqrt{12^2 + 12^2} \approx 16.97$

Closer points usually belong to the same cluster.

### Step 4: Recalculate Centroids

Cluster centers are updated using mean position.

### Step 5: Repeat Until Stable

Repeat assignment + centroid update until clusters stop changing.

## Important Understanding

K-Means tries to minimize **within-cluster variance**.

Meaning: points inside each cluster should be similar.

## Main Challenge: Choosing K

Most important practical issue:

How many clusters should exist?

### Solution: Elbow Method

Run K-Means for multiple values, for example:

- K = 1
- K = 2
- K = 3
- K = 4

Measure cluster error using **WCSS** (Within-Cluster Sum of Squares):

$$
\mathrm{WCSS} = \sum (x_i - c_j)^2
$$

Plot K vs WCSS. The elbow point is often the optimal K.

Practical insight:

- Too few clusters -> oversimplification
- Too many clusters -> over-segmentation

## Customer Segmentation Dataset (Best Beginner Lab)

Features:

- Annual Income
- Spending Score

Goal: discover customer groups.

Expected cluster interpretations:

| Cluster Pattern | Meaning |
|---|---|
| High income + high spend | Premium |
| High income + low spend | Conservative |
| Low income + high spend | Impulsive |
| Low income + low spend | Budget |

This has strong business relevance.

## Why Clustering Is Powerful

Businesses often have no labels.

Clustering can still discover hidden customer behavior automatically.

## Important ML Difference

| Supervised | Unsupervised |
|---|---|
| Has target label | No target |
| Predicts output | Finds patterns |
| Example: Salary prediction | Example: Customer segmentation |

## PCA (Dimensionality Reduction)

### What Is Dimensionality?

Suppose a dataset has 500 features.

Problems:

- Slower training
- Difficult visualization
- More noise

### PCA Goal

PCA reduces the number of features while preserving the most important information.

Simple analogy: compressing high-dimensional data into a smaller, meaningful representation.

### Example

Original features:

- Age
- Income
- Spending
- Purchase frequency
- Credit score

PCA may compress this into:

- Principal Component 1
- Principal Component 2

### Why PCA Is Useful

| Benefit | Explanation |
|---|---|
| Faster training | Fewer features |
| Better visualization | 2D plotting |
| Noise reduction | Removes weak variance |
| Memory efficiency | Smaller data |

### Important PCA Concept

PCA preserves **maximum variance**.

PCA identifies directions where data varies most. These directions are called **principal components**.

## Real-World PCA Applications

| Domain | Use |
|---|---|
| Face recognition | Compress images |
| Recommendation systems | Reduce dimensions |
| Finance | Feature compression |
| GenAI embeddings | Vector reduction |

## Transition to Lab

Use this practical transition:

> Let’s use K-Means clustering to perform customer segmentation and discover hidden customer groups automatically.

## Instructor Questions

1. Why does unsupervised learning not need labels?
2. Why is choosing K difficult?
3. Why is PCA useful for high-dimensional data?

## Closing Line

> Unsupervised Learning helps businesses discover hidden patterns when labeled data does not exist.