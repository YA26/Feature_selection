# FeatureSelector: Automatically computing correlation and association metrics
- **FeatureSelector** is a library useful to check whether two distributions are correlated or associated. 
- It is accessible via **```pip install VariableSelection```**
- Variables types are **automatically detected**(categorical and numerical)

## Dependencies
- Python(version>=3.6)
- DataTypeIdentifier
- scikit-learn
- seaborn

## Four metrics available:
  The following metrics have been calculated on this dataset:
  
  ![alt_text](img/data.jpg) 
  
  - **Pearson's correlation coefficient:** Correlations between numerical variables
  
  ![alt_text](img/corrcoef.jpg)
  ![alt_text](img/corrcoefmatrix.png)
 
  - **Cramer's V**: Cramer's V between categorical variables
  
  ![alt_text](img/cramersv.jpg)
  ![alt_text](img/cramersvmatrix.png)
  
  - **Theil's U/Entropy coefficient/Uncertainty coefficient**: Assymetric measure calculated for pairs of categorical variables
  
  ![alt_text](img/theilsu.jpg)
  ![alt_text](img/theilsumatrix.png)
  
  - **Out-of-bag score**: Assymetric measure computed with a random forest(classifier or regressor). It is useful to detect both linear and non-linear relationships between all type of variables
  
  ![alt_text](img/outofbagscore.png)

## Coding example:
```python
from pandas import read_csv
from os.path import join
from VariableSelection.feature_selector import FeatureSelector
"""
############################################
############  MAIN OBJECT  ################
############################################
"""
data = read_csv(join("data", "loan_approval.csv")) 
feature_selector = FeatureSelector(data)

"""
############################################
############ DATA RETRIEVAL  ###############
############################################
"""
entropy_coef_matrix = feature_selector.get_entropy_coef_matrix()
cramer_v_matrix = feature_selector.get_cramer_v_matrix()
corr_coef_matrix = feature_selector.get_corr_coef_matrix()
oob_matrix = feature_selector.get_oob_score_matrix(n_estimators=100, 
                                                   additional_estimators=100, 
                                                   min_samples_split=30)
"""
############################################
############ MATRICES DISPLAY  #############
############################################
"""
feature_selector.show_matrix_graph(corr_coef_matrix, "Corr coef matrix")
feature_selector.show_matrix_graph(cramer_v_matrix, "Cramer's v matrix")
feature_selector.show_matrix_graph(entropy_coef_matrix, "Entropy coef_matrix")
feature_selector.show_matrix_graph(oob_matrix, "Out of bag error matrix")
```
## Reference:
  Wikipedia
