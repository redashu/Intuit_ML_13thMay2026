# Hyperparameter Tuning (Decision Tree)

## 1. Big Idea: What Are Hyperparameters?

Hyperparameters are settings you choose **before** training a model. They control how the model learns.

### Parameters vs Hyperparameters

| Type | Meaning |
|---|---|
| Parameters | Learned by the model during training |
| Hyperparameters | Set manually before training |

### Example

```python
DecisionTreeClassifier(max_depth=5)
```

Here, `max_depth` is a **hyperparameter**.

## 2. Real-World Analogy

Think of cooking:

| Thing | ML Equivalent |
|---|---|
| Recipe outcome | Model prediction |
| Cooking settings | Hyperparameters |

Examples of cooking settings:

- Oven temperature
- Cooking time
- Spice amount

These settings affect final quality, just like hyperparameters affect model performance.

## 3. Why Hyperparameter Tuning Matters

If `max_depth = 100`, a decision tree can become too complex and **overfit**.

If `max_depth = 1`, the tree can be too simple and **underfit**.

### Goal of tuning

Find the best hyperparameter combination for strong **generalization** on unseen data.

## 4. Important Decision Tree Hyperparameters

| Hyperparameter | Meaning |
|---|---|
| `max_depth` | Maximum tree depth |
| `min_samples_split` | Minimum samples required to split a node |
| `min_samples_leaf` | Minimum samples required in a leaf |
| `criterion` | Split quality function (`gini` or `entropy`) |
| `max_features` | Number of features considered per split |

## 5. Visual Understanding

| Case | Description | Effect |
|---|---|---|
| Underfitting | Too simple | Poor learning |
| Good fit | Balanced complexity | Good generalization |
| Overfitting | Memorizes training data | Poor unseen performance |

## 6. How to Find Good Hyperparameters

Two common approaches:

- Grid Search
- Random Search

### Grid Search

Grid Search checks **all** combinations in a predefined grid.

Example:

- `max_depth = [3, 5, 7]`
- `min_samples_split = [2, 4]`

Combinations tested:

| max_depth | min_samples_split |
|---|---|
| 3 | 2 |
| 3 | 4 |
| 5 | 2 |
| 5 | 4 |
| 7 | 2 |
| 7 | 4 |

Grid Search is:

- Exhaustive
- Systematic
- Computationally expensive

### Random Search

Random Search tests random combinations instead of every combination.

Example: if the full space has 100 combinations, Random Search may test only 10.

Why it works well:

- Not all hyperparameters are equally important
- It often finds good solutions much faster

### Industry rule of thumb

| Dataset size | Preferred method |
|---|---|
| Small | Grid Search |
| Large | Random Search |

## 7. When Tuning Matters Most

Hyperparameter tuning is especially useful when:

- The model is overfitting
- The model is underperforming
- The dataset is complex
- You are optimizing for production
- You are in a competition (for example, Kaggle)

When tuning may matter less:

- Very simple datasets
- Already excellent performance
- Early-stage small business prototypes

## 8. Key Industry Insight

Well-tuned models can outperform more advanced algorithms with poor tuning.

## 9. Practical Flow (Decision Tree)

### Scenario

Suppose your current decision tree accuracy is **78%**.

Question: can tuning improve it?

Yes.

### Step 1: Train an untuned model

```python
from sklearn.tree import DecisionTreeClassifier
from sklearn.metrics import accuracy_score

model = DecisionTreeClassifier(random_state=42)
model.fit(X_train, y_train)

y_pred = model.predict(X_test)
accuracy = accuracy_score(y_test, y_pred)

print("Untuned Accuracy:", accuracy)
```

At this point, default hyperparameters are used.

## 10. Grid Search Implementation

### Step 2: Import `GridSearchCV`

```python
from sklearn.model_selection import GridSearchCV
```

### Step 3: Define parameter grid

```python
param_grid = {
    "max_depth": [3, 5, 7, 10],
    "min_samples_split": [2, 4, 6],
    "criterion": ["gini", "entropy"],
}
```

Grid Search will test all combinations in this grid.

### Step 4: Create `GridSearchCV`

```python
grid_search = GridSearchCV(
    estimator=DecisionTreeClassifier(random_state=42),
    param_grid=param_grid,
    cv=5,
    scoring="accuracy",
    n_jobs=-1,
)
```

Important options:

| Parameter | Meaning |
|---|---|
| `cv=5` | 5-fold cross-validation |
| `scoring="accuracy"` | Evaluation metric |
| `n_jobs=-1` | Use all CPU cores |

Cross-validation splits data into 5 parts and rotates train/validation folds for more reliable evaluation.

### Step 5: Train Grid Search

```python
grid_search.fit(X_train, y_train)
```

This trains many models, compares them, and selects the best hyperparameters automatically.

### Step 6: View best parameters

```python
print(grid_search.best_params_)
```

Example output:

```python
{
    "criterion": "entropy",
    "max_depth": 5,
    "min_samples_split": 4,
}
```

### Step 7: View best CV score

```python
print(grid_search.best_score_)
```

### Step 8: Get best model

```python
best_model = grid_search.best_estimator_
```

### Step 9: Predict with tuned model

```python
y_pred_tuned = best_model.predict(X_test)
```

### Step 10: Compute tuned accuracy

```python
tuned_accuracy = accuracy_score(y_test, y_pred_tuned)
print("Tuned Accuracy:", tuned_accuracy)
```

Expected teaching impact:

| Model | Accuracy |
|---|---|
| Untuned | 78% |
| Tuned | 84% |

## 11. Random Search Implementation

### Step 11: Import `RandomizedSearchCV`

```python
from sklearn.model_selection import RandomizedSearchCV
```

### Step 12: Run Random Search

```python
random_search = RandomizedSearchCV(
    estimator=DecisionTreeClassifier(random_state=42),
    param_distributions=param_grid,
    n_iter=5,
    cv=5,
    random_state=42,
    n_jobs=-1,
)
```

### Grid vs Random

| Grid Search | Random Search |
|---|---|
| All combinations | Random combinations |
| Slower | Faster |
| Exhaustive | Approximate |

## 12. Modern Industry Practice

In real projects, teams often use:

- Random Search
- Bayesian Optimization
- Optuna
- Hyperopt

Reason: full Grid Search becomes expensive as the search space grows.