# TesiBaroniMenozzi
Tesi Placche Carotide


The code files are present in the fold ClassificatoriFINAL:
there are two:
- 2D and 2.5D Classification which aims to classify CT images in 2D and 2.5D through single deep networks and through radiomics. This file finds the best classifier-selector-numfeatures through cross validation and then applies the combination to the test set. By just specifying the classifier to use, the selected features for classification are saved, so you can also not perform CV and just see the results on the test set
-  2D and 2.5D Combination which aims to classify CT images in 2D and 2.5D through combination of deep networks and radiomics


In this study, the following software and libraries were used: Python 3.11, Keras 3.3.3, scikit-learn 1.5.2, TensorFlow 2.16.1, and Pyradiomics 3.0.1.
