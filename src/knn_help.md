# KNN Package Documentation

The KNN (K-Nearest Neighbors) package is a powerful tool for performing KNN classification and regression tasks. It provides a set of functions that allow you to fit a model, make predictions, get scores, summarize the model, and plot the scores.

Please report any issues or suggestions on the Gretl mailing list or GitHub page: https://github.com/atecon/knn .


# Public Functions

### `knn_fit(train_data, train_labels, n_neighbors, opts[null])`

This function fits the KNN model to the training data.

*Parameters:*

- `y`: *series*, The training data to fit the model on.
- `xlist`: *list*, The features to use for the KNN algorithm.
- `n_neighbors`: *int* or *matrix*, The number of neighbors to use for the KNN algorithm. If an integer is provided, a single KNN model is fitted. If a matrix is provided, multiple KNN models are fitted with different numbers of neighbors.
- `opts[null]`: *bundle*, Optionally, a bundle of options to pass to the KNN algorithm.

The `opts` bundle can contain the following options:

- `distance_type`: *string*, The distance metric to use for the KNN algorithm. Default is "euclidean". Possible values are the ones supported by Gretl's built-in function `distance()` (see `help distance`).
- `class_prediction`: *string*, The method to use for predicting classes in a classification task. Default is "majority". <!-- Possible values are-->

  + "majority"
<!--  + "probability" (only for binary classification, currently). -->

  Majority returns the most common class among the neighbors.<!--, while probability returns the proportion of neighbors that belong to the class most common among the neighbors.-->

- `scoring_regression`: *string*, The method to use for scoring the model in a regression task. Default is "rmse". Possible values are:

  + "me"

  + "rmse"

  + "mae"

  + "mape"

  + and others supported by Gretl's built-in function `fcstats()` (see `help fcstats`).

- `scoring_classification`: *string*, The method to use for scoring the model in a classification task. Default is "PRC" referring to precision which is the number of hits over the sum of hits plus false, h/(h+f).
<!-- Default is "FSC" referring to the F1-score which balances recall and precision equally and reduces to the simpler equation 2TP/(2TP + FP + FN). -->
  Alternatives are:


  + "POD": Prob. of detection

  + "POFD": Prob. of false detection

  + "HR": Hit rate

  + "FAR": False alaram rate

  + "CSI": Critical success index

  + "OR": Odds ratio

  + "BIAS": Bias score

  + "TSS": Hanssen-Kuipers score (POD - POFD)

  + "HSS": Heidke skill score

  + "ETS": Equitable threat score

  + "PRC": Precision

  + "FSC": F-Score

- `splitters`: *string*, The method to use for splitting the data into training and test sets. Default is "none" implying that the data is not split and no cross-validation is performed. Possible values are:

  + "none": no cross-validation is performed.

  + "kfold": perform k-fold cross-validation with the number of folds specified by the `kfold_nsplits` parameter (default: 5).

  + "loo": perform leave-one-out cross-validation; only for regression.

  + "recwin": perform recursive window cross-validation with the window size specified by the "win_size" parameter (default: 10).

  + "rolwin": perform rolling window cross-validation with the window size specified by the "win_size" parameter (default: 10).

- `stdize_features`: *bool*, Whether to standardize the features before fitting the model. Default is "TRUE".


**Returns:**

A fitted KNN model object stored in a `bundle`. The bundle includes the following elements:

- `depvar`: *string*, The dependent variable used for fitting the model.
- `features`: *matrix*, The features used for fitting the model; if `stdize_features` is set to `TRUE`, the features are standardized.
- `mean_scores`: *matrix*, The mean scores achieved by the model on the validation data for each number of neighbors (only if cross-validation is performed). Rows represent the number of neighbors used, and columns represent the scoring metrics.
- `n_training_sets`: *int*, The number of training sets used for cross-validation (only if cross-validation is performed).
- `nobs`: *int*, Number of observations in the training and validation data.
- `optimal_k`: *int*, The optimal number of neighbors selected by the cross-validation procedure (only if cross-validation is performed).
- `optimal_score`: *scalar*, The optimal score achieved by the model on the validation data (only if cross-validation is performed).
- `parnames`: *string array*, The names of the features used for fitting the model.
- `sample_t1`: *int*, The index of the first observation in the training set.
- `sample_t2`: *int*, The index of the last observation in the training set.
- `Scores`: *matrices*, Array of matrices containing the scores achieved by the model on the validation data. Each page refers to a different number of neighbors (as specified by `n_neighbors`) evaluated. Rows represent the k-fold splits, and columns represent the scoring metrics.
- `type`: *string*, The type of the model (classification or regression).
- `uhat`: *matrix*, The residuals of the model (only in case of no cross-validation); rows: no. of observations, columns: no. of neighbors evaluated.
- `yhat`: *matrix*, The fitted values of the model (only in case of no cross-validation); rows: no. of observations, columns: no. of neighbors evaluated.



### `knn_predict(model, X)`

This function uses a fitted KNN model to make predictions on the test data. The function requires that you either have requested to train a model with a single number of neighbors or have selected the optimal number of neighbors using cross-validation before, as the model object must contain the optimal number of neighbors. Otherwise, the function will return an error.

*Parameters:*

- `model`: *bundle*, The fitted KNN model object.
- `X`: *numeric*, A list or matrix of the test data to make predictions on.

**Returns:**

- A matrix of predictions.


### `knn_scores(actual, pred, model)`

This function calculates the scores of the model prediction.

*Parameters:*

- `actual`: *series* or *matrix*, The actual data.
- `pred`: *series* or *matrix*, The predicted data.
- `model`: The fitted KNN model.

**Returns:**

A *matrix* holding various accuracy scores.


### `knn_summary(model)`

This function provides a summary of the KNN model.

*Parameters:*

- `model`: *bundle*, The fitted KNN model.

**Returns:**

- A summary of the model.


### `knn_plot_score(model, filename[null])`

This function generates a plot showing the mean performance (across all cross-validation iterations) of the KNN model as a function of the number of neighbors. Only available if cross-validation is performed. The plot shows the mean of the selected metric (e.g., RMSE, MAE, etc.) across all cross-validation iterations for each number of neighbors evaluated

*Parameters:*

- `model`: The fitted KNN model.
- `filename`: *string*, The name of the file to save the plot to. If not provided, the plot is displayed in the Gretl GUI.

**Returns:**

- A plot showing the model's performance.


### `knn_plot_cvscores(model, filename[null])`

This function generates a plot showing the distribution of the performances across folds as a function of the number of neighbors. Only available if cross-validation is performed. The plot shows a boxplot of the selected metric (e.g., RMSE, MAE, etc.) across folds for each number of neighbors evaluated.

*Parameters:*

- `model`: The fitted KNN model.
- `filename`: *string*, The name of the file to save the plot to. If not provided, the plot is displayed in the Gretl GUI.

**Returns:**

- A plot showing the model's performance.

# Change Log

- v0.1 (June 2024): Initial release.
