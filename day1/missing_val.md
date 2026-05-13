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