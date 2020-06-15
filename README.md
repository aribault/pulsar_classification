# Pulsars classification

In this project, I used a [dataset](https://www.kaggle.com/pavanraj159/predicting-a-pulsar-star) found on Kaggle that contains data about real and fake [pulsars](https://en.wikipedia.org/wiki/Pulsar). Pulsars are a special kind of neutron star, which are one of the two possible outcomes of a supernova explosion (the other being a black hole). Neutron stars are extremely dense objects, and their magnetic fields are immensely strong. After a supernova collapses, the resulting neutron star rotates at very high speed because of the conservation of angular momentum, and the enormous loss of mass compared to the pre-explosion supernova. 

This very fast rotating, intense magnetic field is detectable all the way across the universe. From a given point, the signal received over the whole electromagnetic spectrum from such a neutron star is periodic, it "pulses": hence the name, pulsar. Aggregating this periodic signal over many wavelengths gives us the first half of our dataset, the *integrated profile* of the pulsar. The first four features of our data are respectively the mean, the standard deviation, the kurtosis and the skewness of this profile.

The other part of our data is made of the same statistics of another curve, the "Dispersion measure signal-to-noise" curve (DM-SNR). Accross different wavelengths, the signal received from the pulsar across space is distorted by the particles that interfere with the photons that travel the distance between the pulsar and Earth. The agreggation of this distorsion over the electromagnetic spectrum gives us our second curve.

Given these 8 features, my task was to distinguish the real pulsars of the dataset (approx. 10% of the data) from fake ones that were generated randomly. Given the imbalance between the two classes, I chose the f1-score function as the evaluation function of my models, along with the accuracy.

In order to visualize the data, I frequently used during this project a 2-D PCA projection of the data along the two dimensions that explained the most of the features.

![2D PCA projection of the data](https://github.com/aribault/pulsars_prediction/blob/master/scripts/2d_pca_data.png)
