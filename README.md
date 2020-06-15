# Pulsars classification

In this project, I used a [dataset](https://www.kaggle.com/pavanraj159/predicting-a-pulsar-star) found on Kaggle that contains data about real and fake [pulsars](https://en.wikipedia.org/wiki/Pulsar). Pulsars are a special kind of neutron star, which are one of the two possible outcomes of a supernova explosion (the other being a black hole). Neutron stars are extremely dense objects, and their magnetic fields are immensely strong. After a supernova collapses, the resulting neutron star rotates at very high speed because of the conservation of angular momentum, and the enormous loss of mass compared to the pre-explosion supernova. 

This very fast rotating, intense magnetic field is detectable all the way across the universe. From a given point, the signal received over the whole electromagnetic spectrum from such a neutron star is periodic, it "pulses": hence the name, pulsar. Aggregating this periodic signal over many wavelengths gives us the first half of our dataset, the *integrated profile* of the pulsar. The first four features of our data are respectively the mean, the standard deviation, the kurtosis and the skewness of this profile.

The other part of our data is made of the same statistics of another curve, the "Dispersion measure signal-to-noise" curve (DM-SNR). Accross different wavelengths, the signal received from the pulsar across space is distorted by the particles that interfere with the photons that travel the distance between the pulsar and Earth. The agreggation of this distorsion over the electromagnetic spectrum gives us our second curve.

Given these 8 features, my task was to distinguish the real pulsars of the dataset (approx. 10% of the data) from fake ones that were generated randomly. Given the imbalance between the two classes, I chose the f1-score function as the evaluation function of my models, along with the accuracy.

In order to visualize the data, I frequently used during this project a 2-D PCA projection of the data along the two dimensions that explained the most of the features.

![2D PCA projection of the data](https://github.com/aribault/pulsars_prediction/blob/master/scripts/2d_pca_data.png)

I trained the following models on the training set: an RBF kernel SVM, a logistic regression, a random forest, an AdaBoost model, and an XGBoost model. Although all models were pretty close in absolute f1-score (about 0.88) over the test data, the XGBoost proved to be the best by a small but consistent margin over the cross-validation score and the test score (0.894). Ensemble methods were tried (both by voting and by stacking), but no combination of estimators could beat the XGBoost model. 

![XGBoost test confusion matrix](https://github.com/aribault/pulsars_prediction/blob/master/scripts/xgb_confusion_matrix.png)

The graphical representation of the predictions were interesting. A few outliers for the positive class seem to be mixed pretty deep in the middle of the negative samples, and get missclassified over all models. 

![XGBoost test predictions](https://github.com/aribault/pulsars_prediction/blob/master/scripts/xgb_test_results.png)

I also found interesting that the SVM support vectors were located in almost the same spot in this 2-d projection of the data. Below are the predictions of the RBF-SVM over the training data, with the support vectors in black.

![SVM training predictions and support vectors](https://github.com/aribault/pulsars_prediction/blob/master/scripts/predictions/rbf_svm_predictions.png)

As a result of this project, I was very impressed with the results of the XGBoost classifier, since it provided a significant upgrade over all the other models that I tried, which had all about equal performance (exception made of the logistic regression, which was a tad inferior to the other models). Given its simplicity, it is also remarkable that the RBF kernel-SVM manages about the same performance as the more refined random forest and AdaBoost, in particular. 

Final scores on the test data : 

| model               	| f1-score (test) 	| accuracy score (test) 	|
|---------------------	|-----------------	|-----------------------	|
| logistic regression 	| 0.8694          	| 0.9779                	|
| RBF kernel-SVM      	| 0.8827          	| 0.9798                	|
| Random Forest       	| 0.8852          	| 0.9801                	|
| AdaBoost            	| 0.8846          	| 0.9798                	|
| XGBoost             	| 0.8941          	| 0.9812                	|
