# K-Nearest Neighbors (KNN) Package

This package provides a simple implementation of the K-Nearest Neighbors (KNN) algorithm in Gretl. The public functions provided by this package are:

- `knn_fit`
- `knn_predict`
- `knn_scores`
- `knn_summary`

Please note that this package is a simple implementation of the KNN algorithm and may not include all features of more comprehensive machine learning libraries.

## `knn_fit`

This function fits the KNN model to the provided data.

**Syntax:**
```gretl
knn_fit(xlist, ylist, opts)
```

**Parameters:**
- `xlist`: A list of predictor variables.
- `ylist`: The target variable.
- `opts`: An optional bundle of options for the KNN algorithm.

**Returns:**
A bundle containing the fitted KNN model.

## `knn_predict`

This function uses a fitted KNN model to make predictions on new data.

**Syntax:**
```gretl
knn_predict(model, newdata)
```

**Parameters:**
- `model`: A fitted KNN model.
- `newdata`: New data for which to make predictions.

**Returns:**
A list of predicted values.

## `knn_scores`

This function calculates performance metrics for a fitted KNN model.

**Syntax:**
```gretl
knn_scores(model, actual, predicted)
```

**Parameters:**
- `model`: A fitted KNN model.
- `actual`: The actual target values.
- `predicted`: The predicted target values.

**Returns:**
A bundle containing various performance metrics.

## `knn_summary`

This function provides a summary of a fitted KNN model.

**Syntax:**
```gretl
knn_summary(model)
```

**Parameters:**
- `model`: A fitted KNN model.

**Returns:**
A string containing a summary of the model.

