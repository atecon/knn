# KNN Package Documentation

The KNN (K-Nearest Neighbors) package is a powerful tool for performing KNN classification and regression tasks. It provides a set of functions that allow you to fit a model, make predictions, get scores, summarize the model, and plot the scores.

Please report any issues or suggestions on the [GitHub page](https://github.com/atecon/knn) or Gretl mailing list.


# Public Functions

### `knn_fit(train_data, train_labels, n_neighbors)`

This function fits the KNN model to the training data.

*Parameters:*

- `y`: *series*, The training data to fit the model on.
- `xlist`: *list*, The features to use for the KNN algorithm.
- `n_neighbors`: *int* or *matrix*, The number of neighbors to use for the KNN algorithm. If an integer is provided, a single KNN model is fitted. If a matrix is provided, multiple KNN models are fitted with different numbers of neighbors.
- `opts[null]`: *bundle*, Optionally, a bundle of options to pass to the KNN algorithm.

The `opts` bundle can contain the following options:

- `distance_type`: *string*, The distance metric to use for the KNN algorithm. Default is "euclidean". Possible values are the ones supported by Gretl's built-in function `distance()` (see `help distance`).
- `class_prediction`: *string*, The method to use for predicting classes in a classification task. Default is "majority". Possible values are

  + "majority"
  + "probability".

  Majority returns the most common class among the neighbors, while probability returns the proportion of neighbors that belong to the class most common among the neighbors.

- `scoring_regression`: *string*, The method to use for scoring the model in a regression task. Default is "rmse". Possible values are:

  + "me"

  + "rmse"

  + "mae"

  + "mape"

  + and others supported by Gretl's built-in function `fcstats()` (see `help fcstats`).

- `scoring_classification`: *string*, The method to use for scoring the model in a classification task. Default is "TSS" referring to the Hansen-Kuipers Score. Alternatives are:


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

  + "kfold": perform k-fold cross-validation with the number of folds specified by the `kfold_nsplits` parameter (default: 5).

  + "loo": perform leave-one-out cross-validation.

  + "recwin": perform recursive window cross-validation with the window size specified by the "win_size" parameter (default: 10).

  + "rolwin": perform rolling window cross-validation with the window size specified by the "win_size" parameter (default: 10).

- `stdize_features`: *bool*, Whether to standardize the features before fitting the model. Default is "TRUE".


**Returns:**

A fitted KNN model object stored in a `bundle`. The bundle includes the following elements:

- `nobs`: *int*, Number of observations in the training and validation data.
- `optimal_k`: *int*, The optimal number of neighbors selected by the cross-validation procedure (only if cross-validation is performed).
- `optimal_score`: *scalar*, The optimal score achieved by the model on the validation data (only if cross-validation is performed).
- `sample_t1`: *int*, The index of the first observation in the training set.
- `sample_t2`: *int*, The index of the last observation in the training set.
- `features`: *matrix*, The features used for fitting the model.
- `mean_scores`: *matrix*, The mean scores achieved by the model on the validation data for each number of neighbors (only if cross-validation is performed). Rows represent the number of neighbors used, and columns represent the scoring metrics.
- `depvar`: *string*, The dependent variable used for fitting the model.
- `parnames`: *string array*, The names of the features used for fitting the model.
- `type`: *string*, The type of the model (classification or regression).
- `Scores`: *matrices*, Array of matrices containing the scores achieved by the model on the validation data for each number of neighbors (only if cross-validation is performed). Rows represent the k-fold splits, and columns represent the scoring metrics. Each matrix corresponds to a different number of neighbors.


### `knn_predict(model, X)`

This function uses a fitted KNN model to make predictions on the test data.

*Parameters:*

- `model`: *bundle*, The fitted KNN model object.
- `X`: *numeric*, A list or matrix of the test data to make predictions on.

**Returns:**

- A matrix of predictions.


### `knn_scores(actual, pred, model)`

This function calculates the accuracy score (for classification tasks) or the mean squared error (for regression tasks) of the KNN model.

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

This function generates a plot showing the mean performance (across all cross-validation iterations) of the KNN model as a function of the number of neighbors.

*Parameters:*

- `model`: The fitted KNN model.
- `filename`: *string*, The name of the file to save the plot to. If not provided, the plot is displayed in the Gretl GUI.

**Returns:**

- A plot showing the model's performance.


# Change Log

- v0.1 (June 2024): Initial release.
