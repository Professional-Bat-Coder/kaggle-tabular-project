
**I. OVERVIEW**
This project aims to predict student performance based on interaction features collected during gameplay sessions. The task is formulated as a binary classification problem to determine if a student will correctly answer questions based on their session logs. A Logistic Regression model and a Random Forest classifier were applied to the dataset. The baseline Logistic Regression model ultimately performed best, achieving an accuracy of approximately 65.4% on the local test set. 

**II. SUMMARY OF WORKDONE**

*   **A. DATA**
    *   Type: Tabular CSV files containing gameplay event data, session coordinates, and user behavior metrics. The target is a binary label identifying if the answer was correct.
    *   Size: A subset of 500,000 rows was loaded from the raw dataset to prevent memory crashes.
    *   Split: A stratified split of 64% training, 16% validation, and 20% local test data was utilized.

*   **B. PREPROCESSING / CLEAN UP**
    *   Missing numerical values were filled with 0 (for `hover_duration`) or -1 (for `page`), while missing categorical values were filled with "unknown" to preserve existing information. Remaining NaNs were filled with the median.
    *   Dropped high-cardinality and non-predictive identifier columns (e.g., `session_id_x`, `fqid`, `text`) to reduce noise.
    *   Removed extreme outliers specific to the `elapsed_time` feature using the standard 1.5x IQR method.
    *   One-hot encoded categorical features, specifically `event_name`, `level_group`, and `name`.
    *   Applied standard scaling to numerical features so they possessed zero mean and unit variance.

*   **C. DATA VISUALIZATION**
    *   Feature distributions were mapped before and after cleaning and scaling to ensure transformations were successful.
    *   Histograms and bar charts were plotted to compare feature distributions (such as `elapsed_time` and spatial coordinates) between the correct and incorrect classes.
    *   Correlation heatmaps were generated to check for relationships and potential leaks among numeric features.
    *   Visualizations successfully confirmed that features like `elapsed_time` and `event_name` exhibited distinct variations between classes.

**III. PROBLEM FORMULATION**
*   Input: 31 standardized numerical and one-hot encoded categorical features.
*   Output: Binary label where 0 represents Incorrect and 1 represents Correct.
*   Models: Random Forest Classifier (primary model) and Logistic Regression (baseline model).
*   Metrics: Accuracy and the Kaggle-specified metric, F1-Score.

**IV. TRAINING**
*   Trained locally inside a Jupyter Notebook environment using `scikit-learn`.
*   Data was strictly stratified during the `train_test_split` phase to maintain the natural ~69% (Correct) to 31% (Incorrect) class balance.
*   The Random Forest model was ensembled using 50 estimators.

**V. PERFORMANCE COMPARISON**
*   Random Forest: Reached a Validation Accuracy of ~62.7%, a Validation F1-Score of 0.74, and a Local Test Accuracy of ~63.3%.
*   Logistic Regression: Reached a Local Test Accuracy of ~65.4%.
*   The secondary Logistic Regression model marginally outperformed the primary Random Forest model on the unseen local test data.

**VI. CONCLUSIONS**
*   Logistic Regression provided slightly better generalization than Random Forest for this specific tabular dataset.
*   Time spent on tasks (`elapsed_time`), the type of event clicked, and overall level progression are the most meaningful predictors for determining student success.
*   The cleaning pipeline successfully processed the Kaggle test set to seamlessly generate the final predictions.

**VII. FUTURE WORK**
*   Engineer more complex features from the raw JSON/text event logs rather than dropping them entirely.
*   Perform exhaustive hyperparameter tuning (e.g., GridSearchCV) to optimize the Random Forest depth and increase test accuracy.
*   Experiment with gradient-boosting frameworks like XGBoost.

**VIII. HOW TO REPRODUCE RESULTS**
1.  Clone this repository.
2.  Download the raw dataset from Kaggle and place it in the appropriate local `/data` directory.
3.  Install all required software packages.
4.  Run the notebook sequentially from start to finish to automatically output the final `submission.csv` file.

**IX. OVERVIEW OF FILES IN REPOSITORY**
*   Main Jupyter Notebook containing the preprocessing and modeling code.
*   `submission.csv` containing the final output predictions.
*   README file detailing the project scope.

**X. SOFTWARE SETUP**
*   `pandas`, `numpy`, `matplotlib`, `seaborn`, `scikit-learn`.

**XI. DATA**
*   Predict Student Performance from Game Play Dataset.

**XII. TRAINING**
*   Open the main notebook in Jupyter and run all cells in order.
*   Note that a row limit is placed on the initial `pd.read_csv()` function to load only 500,000 rows to optimize memory and prevent system crashes.

**XIII. PERFORMANCE EVALUATION**
*   Accuracy and F1-score are calculated natively in the notebook, alongside detailed classification reports and visually plotted confusion matrices.
*   The trained model and fitted scaler are automatically applied to the unlabelled Kaggle test set to generate the final `submission.csv`.

**XIV. CITATIONS**
*   Kaggle Project Link: https://www.kaggle.com/competitions/predict-student-performance-from-game-play/data
*   Scikit-learn documentation: https://scikit-learn.org
![](UTA-DataScience-Logo.png)

# Project Title

* **One Sentence Summary** Ex: This repository holds an attempt to apply LSTMs to Stock Market using data from
"Get Rich" Kaggle challenge (provide link). 

## Overview

* This section could contain a short paragraph which include the following:
  * **Definition of the tasks / challenge**  Ex: The task, as defined by the Kaggle challenge is to use a time series of 12 features, sampled daily for 1 month, to predict the next day's price of a stock.
  * **Your approach** Ex: The approach in this repository formulates the problem as regression task, using deep recurrent neural networks as the model with the full time series of features as input. We compared the performance of 3 different network architectures.
  * **Summary of the performance achieved** Ex: Our best model was able to predict the next day stock price within 23%, 90% of the time. At the time of writing, the best performance on Kaggle of this metric is 18%.
