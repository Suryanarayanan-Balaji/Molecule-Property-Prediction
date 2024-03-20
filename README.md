# Speeding up molecular analysis using Support Vector Machines

<img src='https://github.com/Suryanarayanan-Balaji/GPT-MolBERTa/assets/112913550/54a810e7-3dc2-46c1-94e2-0a1774f30b21' width="250" height='400' align="right">

This project aims to accelerate molecular analysis through the application of Support Vector Machines (SVMs) in cheminformatics. Leveraging Simplified molecular-input line-entry system (SMILES) representations and molecular fingerprints, the project employs machine learning techniques to facilitate tasks such as virtual screening, QSAR modeling, and molecular property prediction. Utilizing the Quantum Mechanics Dataset 8 (QM8) as a benchmark dataset and framework, the project evaluates the performance of machine learning models in various molecular informatics and drug discovery tasks. You can find more information about the project here.

# How It's Made

For this project, I first obtained the QM 8 dataset, which consists of a column on SMILES and 12 sets of labels. Before conducting any processing, I verified if each SMILES has a corresponding molecule. Subsequently, I created a new column in the QM8 dataframe, where authentic SMILES were retained, and non-corresponding ones were replaced with an 'NA' string. I then filtered the non-NA values out before dropping the new column. Following that, I generated 209 properties for each SMILES molecule, which I further processed using principal component analysis. I also conducted outlier analysis using the 1.5 Interquartile Range method, dropping the values which do not meet this criteria.

After conducting the data processing, I commenced machine learning, using support vector regression (SVR). Since this was a multi-label problem, I fitted individual models for each label, obtained the relevant metric (Mean Absolute Error (MAE)) and averaged them across all 12 labels. This gave me a single MAE value to benchmark with other models. In an effort to improve performance, I conducted K-fold Cross Validation and Hyperparameter Tuning, which allowed the model to outperform several neural network models. 

# Lessons Learned

The major lesson I learned was how to handle multi-label regression/classification problems in an elegant way. While the model.fit method in sklearn allows for multi-label fits where individual models are initialized for each different label and the overall performance is averaged across all labels, the Support Vector Regression model does not have this ability. As a result, I had to manually wrap the SVR model using the Multi-Output Regressor class to allow for this parallel processing. This allowed for smooth processing of multi-label problems. 
