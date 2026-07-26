# Residency-Day-2-Project-Deliverable-3-Classification-Clustering-and-Pattern-Mining
# Deliverable 3: Classification, Clustering, and Pattern Mining

## Project Overview

This project applies classification, clustering, hyperparameter tuning, and association rule mining to the Wisconsin Breast Cancer dataset. The dataset contains 569 observations, 30 numerical tumor features, and a diagnosis label. Among the observations, 357 are benign and 212 are malignant. No missing values were found. For classification, malignant cases were coded as the positive class. The data were divided into 80% training data and 20% testing data using stratified sampling.

## Classification Insights

Two classification models were developed: a Decision Tree and a Support Vector Machine (SVM). The Decision Tree achieved an accuracy of 91.23%, an F1 score of 0.8750, and an ROC-AUC score of 0.9005. It correctly classified 69 benign and 35 malignant cases. However, it incorrectly classified seven malignant observations as benign.

The SVM was tuned using GridSearchCV with five-fold stratified cross-validation. The best hyperparameters were an RBF kernel, `C = 10`, and `gamma = 0.01`. The tuned SVM achieved an accuracy of 99.12%, an F1 score of 0.9880, and an ROC-AUC score of 0.9970. It correctly classified all 72 benign cases and 41 of the 42 malignant cases. Therefore, the tuned SVM was the strongest classification model.

## Clustering Insights

K-Means clustering was applied to the 30 standardized tumor features. Models with two through six clusters were evaluated using silhouette scores. The two-cluster solution produced the highest silhouette score of 0.3450 and was selected as the final model.

Cluster 0 contained 189 observations, including 175 malignant and 14 benign cases. Its malignant rate was approximately 92.59%. This group displayed relatively high measurements for mean concave points, worst concave points, mean concavity, worst perimeter, and worst concavity.

Cluster 1 contained 380 observations, including 343 benign and 37 malignant cases. Its malignant rate was approximately 9.74%. This group generally displayed lower tumor concavity, concave-point, and perimeter measurements. The clustering results therefore identified a broadly higher-risk group and a lower-risk group, although the silhouette score and mixed diagnoses show that the groups were not perfectly separated.

Principal Component Analysis was used to visualize the clusters in two dimensions. The first two principal components explained approximately 63.24% of the variation in the original variables.

## Pattern-Mining Insights

An Apriori-style association rule mining method was applied after selected continuous tumor measurements were converted into high and low categories using their median values. The analysis used minimum support of 0.10, minimum confidence of 0.70, and lift greater than 1.

The strongest rule connected high worst area and high worst concavity with a malignant diagnosis. It had support of 0.3427, confidence of 0.8784, and lift of 2.3575. This means that approximately 87.84% of records with both characteristics were malignant, and malignancy was about 2.36 times more likely for those records than in the overall dataset.

Other strong rules combined high mean concavity with high worst area, high worst concavity with high worst radius, and high mean concavity with high worst radius. Overall, high tumor size, perimeter, concavity, and concave-point measurements were repeatedly associated with malignant diagnoses.

## Practical Relevance and Real-World Applications

The tuned SVM could support early risk identification by flagging cases that require additional clinical review. Its high malignant-class recall is particularly relevant because false-negative predictions may delay further testing. However, the model should assist healthcare professionals rather than independently determine a diagnosis.

The Decision Tree could be useful when model interpretability is more important than maximum accuracy. Its decision structure can help analysts understand which measurements influence classification outcomes.

The clustering results could support patient segmentation by grouping observations according to similar tumor characteristics. Healthcare organizations could use this information to identify higher-risk profiles, prioritize diagnostic resources, and investigate unusual cases.

Association rules provide understandable combinations of measurements associated with malignancy. These rules could support clinical screening dashboards or alert systems. For example, a record with both high worst area and high worst concavity could be highlighted for closer examination.

## Challenges and Solutions

### Class Imbalance

The dataset contained more benign than malignant observations. This imbalance could cause the models to favor the majority class. The problem was addressed by using stratified train-test splitting and class-balanced classification models. F1 score and ROC-AUC were also evaluated in addition to accuracy.

### Different Measurement Scales

The dataset included measurements with substantially different numerical ranges. Distance-based methods such as SVM and K-Means can be dominated by larger-scale variables. StandardScaler was therefore applied before SVM training and clustering. Scaling was performed inside the SVM pipeline to prevent data leakage.

### Hyperparameter Selection

SVM performance depends on values such as `C` and `gamma`. Selecting these values manually could produce a biased or poorly performing model. GridSearchCV with five-fold stratified cross-validation was used to evaluate several parameter combinations systematically.

### Selecting the Number of Clusters

K-Means requires the number of clusters to be specified in advance. Models containing two through six clusters were compared using silhouette scores. The two-cluster model was selected because it produced the highest score. However, the final score of 0.3450 indicates moderate separation, so the clusters should not be interpreted as definitive diagnostic groups.

### Continuous Data in Association Rule Mining

Association rule mining requires categorical items, while the tumor measurements were continuous. Selected variables were converted into high and low categories using their median values. This produced interpretable rules but also reduced numerical detail. Alternative discretization approaches could be evaluated in future work.

### Medical Interpretation

Strong statistical performance does not guarantee clinical validity. The dataset is relatively small, and the models were tested on only 114 observations. The findings should therefore be validated using external datasets before deployment. The models must be used as decision-support tools under professional medical oversight.

## Conclusion

The tuned SVM produced the strongest classification performance, while the Decision Tree provided a more interpretable baseline. K-Means identified higher-risk and lower-risk tumor profiles, and association rule mining revealed understandable combinations of measurements linked to malignant diagnoses. Together, the methods demonstrate how supervised learning, unsupervised learning, and pattern mining can support cancer-risk analysis while also showing the importance of scaling, tuning, validation, and careful clinical interpretation.
