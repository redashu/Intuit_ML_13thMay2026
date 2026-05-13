# Missing Value Imputation

Missing values are commonly filled using:

- Mean
- Median
- Mode

Not variance.

## Correct Understanding

| Technique | Used For | Example |
|---|---|---|
| Mean | Numerical data | Age, Salary |
| Median | Numerical data with outliers | Income, Charges |
| Mode | Categorical data | Gender, City |

## Mean Imputation

Uses the average value.

Example:

```text
10, 20, 30, missing
Mean = 20
```

Fill the missing value with:

```text
20
```

## Median Imputation

Uses the middle value after sorting.

Example:

```text
10, 20, 1000, missing
Median = 20
```

Better when outliers exist.

Very common in industry.

## Mode Imputation

Uses the most frequent value.

Example:

```text
Male, Female, Male, missing
Mode = Male
```

Mostly used for categorical columns.

## Strategies to Handle Missing Values

This is the main conceptual section.

### Strategy 1: Remove Rows

Drop missing records:

```python
df.dropna()
```

Use when:

- few missing records
- dataset is large enough

Problem:

If too many rows are removed, it can cause:

- data loss
- bias
- poor model training

Important real-world caution.

### Strategy 2: Remove Columns

Example: if 90% values are missing, the column may be useless.

```python
df.drop(columns=['column_name'])
```

### Strategy 3: Fill Missing Values (Imputation)

Most common industry approach.

#### Numerical Columns

Mean imputation:

```python
df['Age'].fillna(df['Age'].mean())
```

Use when:

- distribution is roughly normal

Median imputation:

```python
df['Salary'].fillna(df['Salary'].median())
```

Best for:

- skewed data
- outliers

Very common in industry.

#### Categorical Columns

Mode imputation:

```python
df['Gender'].fillna(df['Gender'].mode()[0])
```
