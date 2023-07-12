**1. Dropping Rows with Null Values:**

```python
# Dropping rows with null values
df.dropna(inplace=True)
```

**2. Replacing Null Values with Mean:**

```python
# Replace null values with mean
mean = df['column_name'].mean()
df['column_name'].fillna(mean, inplace=True)
```

**3. Replacing Null Values with Median:**

```python
# Replace null values with median
median = df['column_name'].median()
df['column_name'].fillna(median, inplace=True)
```

**4. Replacing Null Values with Mode for Categorical Columns:**

```python
# Replace null values with mode
mode = df['column_name'].mode()[0]
df['column_name'].fillna(mode, inplace=True)
```

**5. Filling Missing Values using Regression (Semi-supervised Learning):**

```python
from sklearn.linear_model import LinearRegression

# Create a DataFrame with non-null values in the target column
train_df = df.dropna(subset=['target_column'])

# Split data into features (X) and target (y)
X_train = train_df.drop('target_column', axis=1)
y_train = train_df['target_column']

# Create a DataFrame with null values in the target column
test_df = df[df['target_column'].isnull()]

# Split data into features (X_test) and missing target (y_test)
X_test = test_df.drop('target_column', axis=1)

# Fit a linear regression model
model = LinearRegression()
model.fit(X_train, y_train)

# Predict the missing values
y_pred = model.predict(X_test)

# Replace null values with predicted values
df.loc[df['target_column'].isnull(), 'target_column'] = y_pred
```
- SImiliarly we can do for categorical column as well.
