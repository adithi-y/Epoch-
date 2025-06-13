# Emotion Classification

## Problem Statement
The PS was to classify emotions from image data, where the main challenge was leveraging both labeled and unlabeled data. 
In a lot of real-world scenarios, getting access to large-scale labeled datasets is highly impractical. 
This project uses semi-supervised learning techniques to improve classification performance with very less labeled data.

## Methodology
### Data Preprocessing
- Standardized and balanced the dataset to reduce the imbalance in class representation.
- Initially attempted downsampling of overrepresented classes (neutral) but there was a large reduction in the amount of data.
- Implemented data augmentation techniques to improve representation of scarce classes. But that did not help the resultant metrics so it has been commented.

### Feature Extraction
To build an efficient feature space for emotion classification, this code used **Singular Value Decomposition (SVD)** and **Principal Component Analysis (PCA)**.

- **Combining Labeled and Unlabeled Data** :  Since PCA does not inherently require labels, both labeled and unlabeled datasets were combined to form a richer feature space. This ensured that the principal components identified by PCA were based on a more generalized distribution of data rather than being constrained by the less labeled samples.

- **SVD Implementation** :  SVD was used as an initial step to reduce dimensionality while preserving important variance in the dataset. It helped capture dominant patterns inherent in the images.

- **PCA for Feature Selection** :  PCA was then applied to extract the most influential components from the combined dataset.
- - Ensuring better principal component extraction by providing PCA with a larger dataset.
- - Balancing between computational efficiency and retaining image details while selecting features after decomposition.



### Model Training
- Trained a Support Vector Machine (SVM) classifier using hyperparameter tuning and cross-validation.
- Got the optimal kernel, gamma, and other parameters, with linear kernel giving the best performance.
- Fine-tuned the SVM model using validated parameters.

## Results
### Overall Accuracy: 77.5%

| Emotion   | Precision | Recall | F1-Score | Support |
|-----------|----------|--------|----------|---------|
| Disgust   | 1.00     | 0.92   | 0.96     | 12      |
| Happiness | 0.93     | 1.00   | 0.97     | 14      |
| Surprise  | 1.00     | 0.88   | 0.94     | 17      |
| Neutral   | 0.82     | 0.64   | 0.72     | 14      |
| Fear      | 0.60     | 0.60   | 0.60     | 5       |
| Anger     | 0.47     | 0.78   | 0.58     | 9       |
| Contempt  | 0.40     | 0.67   | 0.50     | 3       |
| Sadness   | 0.33     | 0.17   | 0.22     | 6       |

- **Macro Average:** Precision = 0.69, Recall = 0.71, F1-Score = 0.69
- **Weighted Average:** Precision = 0.80, Recall = 0.78, F1-Score = 0.78
