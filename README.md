# TesiBaroniMenozzi
Tesi Placche Carotide


The code files are present in the fold ClassificatoriFINAL:
there are two:

- 2D and 2.5D Classification which aims to classify CT images in 2D and 2.5D through single deep networks and through radiomics. This file finds the best classifier-selector-numfeatures through cross validation and then applies the combination to the test set. The trained classifier is saved into the folder "trainedmodels2D" and is named as the network, the selected features needed to perform classification on the test set are saved in the same folder. Using these two files there is no need to perform CV to obtain the test results. 
  
-  2D and 2.5D Combination which aims to classify CT images in 2D and 2.5D through combination of deep networks and radiomics. Features from the best radiomic model and the best model for each neural network were integrated and can be found in the csv file under the "Combinations" folder (named selected_features_{deep network}\_rad_{type image}.csv). Then this set of combined features was then refined using an importance-based filter, which retains features with at least 50% of the importance of the most significant features as measured by the Gini in- dex from a RF (important features are saved as 'important_features{deep network}\_{type image}.csv'. Additionally, the classifier is determined using a single stratified validation set of 27 patients. The trained classifier is saved as trained_classifier_{deep network}_{type image}.pkl

- **2024_12_Baroni_Menozzi_Executive_Summary_02.pdf**: Updated executive summary of the project, providing an overview of the main results and conclusions.  
- **2024_12_Baroni_Menozzi_Tesi_01.pdf**: Preliminary version of the thesis, including detailed analyses, methodology, and research findings.  

## ClassificatoriFINAL

### 2Dand2.5DClassification
- 2D and 2.5D classification of single models + ensembles

### 2Dand2.5DCombination
- 2D and 2.5D classification of combined models

## Combinations

### trained_classifier_name
- Trained classifier combined with radiomics on full/cut images

### selected_features_name
- Contains all the combined features from the network + radiomics in both cut and full cases

### important_features_name
- Contains the indices of features selected based on importance for various cases

## CSVFeatures

### 2D
- Contains CSV files of features extracted from a single slice in cut and full image cases for the 4 networks + radiomics

### 2.5D
- Contains CSV files of features extracted from all slices in cut and full image cases for the 4 networks + radiomics

## Feature Extraction

### PretrainedNetworksFeatureExtraction
- Contains the code for extracting features from the 4 pretrained networks

### Radiomics
- Contains the code for extracting features for radiomics

## Area indexes
- Contains the indices of the slices remaining for each patient after filtering the area at 30% / 50% / 70%


## trainedmodels2D

### CUT/FULL
- Contains the trained classifiers for the 4 pretrained networks

### original_2Dfeatures_name
- Contains the original indices of the features selected by the best model. These indices correspond to the ones found in the CSV files located in CSVFeatures

### selected_features_name
- Contains the indices of features selected after performing correlation and p-value filtering. These indices are not comparable to those in the CSV files in CSVFeatures, as the features remaining after correlation and p-value filtering have their indices reset starting from 0.

## pretrained_Models
- Contains the deep models used to extract deep features

## slice_rimanenti
- Simple CSV file that reports the number of original and filtered slices (by a certain percentage) for each patient
---

## To run the code

### 2Dand2.5DClassification

#### 2D
1. Execute the cells from "Import libraries" to "patients labels load".
2. Load the features:
  - For radiomics: run "Radiomics 2D features load".
  - For deep learning: run "Encoders 2D features load", specifying:
      - network_name among ["VGG", "ResNet", "IncRes", "Inception"]
      - type_image among ["Full", "Cut"]
3. Execute the "split" cell.
4. (Optional) Skip the following cells related to cross-validation if not needed.
5. Run "Test results" (the first cell) to observe the results of pre-trained classifiers if cross-validation is skipped.

#### ENSEMBLE 2D
1. Select the type of slice to consider (Cut or Full) in the first cell.
2. Comment out the line that you do not wish to execute in the second cell
   ```python
   y_preds_combined = np.array([y_pred['IncRes'], y_pred['ResNet'], y_pred['VGG'], y_pred['Inception']]) # Ensemble of pretrained networks only
   y_preds_combined = np.array([y_pred['IncRes'], y_pred['ResNet'], y_pred['VGG'], y_pred['Inception'], y_pred['Rad']])  # Ensemble of pretrained networks only
   ```

#### 2.5D
1. As with 2D, specify the combination of network and image type in the "encoders data" cell.
2. For radiomics, execute the "radiomics data" cell.
3. Execute the next 3 cells to get the final results of the selected combination.

#### ENSEMBLE 2.5D
- Works similarly to the ENSEMBLE 2D case

### 2Dand2.5DCombinations

1. Run the first cells from "import" to "functions for 2D combinations".
2. (Optional) Avoid running all cells in "Execute for creation of csv files, important features and classifier", which are used to create the CSV files with combined features for various cases.

#### 2D
1. Execute all cells in "2D combined start execution", specifying the network type and image type at the beginning
2. (Optional) Run the cell with roc_results and then ignore it, as it serves to print all the ROC curves in the "plot roc multiple" section, which can be skipped.

#### 2.5D
1. As with 2D, specify the image type and network name. Leave the mode parameter as Max to obtain the thesis results.
2. Execute all cells afterward. The cells after "Multiple ROCs" do not need to be executed.

---

## USEFUL LIBRARIES
Below are some libraries and their versions used:

- `Python`                       3.11
- `keras`                        3.4.1
- `Keras-Preprocessing`          1.1.2
- `numpy`                        1.26.4
- `pandas`                       2.1.1
- `pyradiomics`                  3.0.1
- `scikit-image`                 0.21.0
- `scikit-learn`                 1.5.2
- `scikit-learn-extra`           0.3.0
- `SimpleITK`                    2.4.0
- `scipy`                        1.11.2
- `tensorflow`                   2.17.0
- `xgboost`                      2.1.0
