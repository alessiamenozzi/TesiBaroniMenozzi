# TesiBaroniMenozzi
Tesi Placche Carotide


The code files are present in the fold ClassificatoriFINAL:
there are two:

- 2D and 2.5D Classification which aims to classify CT images in 2D and 2.5D through single deep networks and through radiomics. This file finds the best classifier-selector-numfeatures through cross validation and then applies the combination to the test set. The trained classifier is saved into the folder "trainedmodels2D" and is named as the network, the selected features needed to perform classification on the test set are saved in the same folder. Using these two files there is no need to perform CV to obtain the test results. 
  
-  2D and 2.5D Combination which aims to classify CT images in 2D and 2.5D through combination of deep networks and radiomics. Features from the best radiomic model and the best model for each neural network were integrated and can be found in the csv file under the "Combinations" folder (named selected_features_{deep network}\_rad_{type image}.csv). Then this set of combined features was then refined using an importance-based filter, which retains features with at least 50% of the importance of the most significant features as measured by the Gini in- dex from a RF (important features are saved as 'important_features{deep network}\_{type image}.csv'. Additionally, the classifier is determined using a single stratified validation set of 27 patients. The trained classifier is saved as trained_classifier_{deep network}_{type image}.pkl


Libraries versions: Python 3.11, Keras 3.3.3, scikit-learn 1.5.2, TensorFlow 2.16.1, and Pyradiomics 3.0.1.
