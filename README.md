# CovidDrugDiscovery
## Project Overview
- Trained machine learning model to predict inhibition of SARS-2 Coronavisus by small molecules
- Created descriptors of each molecule relevant to drug discovery
- Optimized random forest model for prediction
### Code and Resources
Python Version: 3.7
Packages: pandas, numpy, sklearn, matplotlib, seaborn, pickle
Organic Chemistry: rdkit
For Requirements: `conda env create -f drugdiscovery.yml`
## Data
Data for 1669 small molecules was taken from the CHEMBL databse. Each molecule was assigned a Hit score between 0 and 1 basd on ability to inhibit Coronavirus infection of Human Renal Cortical Epithelial Cells.
Scores greater than 0.6 are considered hits.

## Data Processing
The rdkit package was used to generate relevant physical descriptors of a molecule based on their molecular formula. The following descriptors were calculated for each molecule:

|       Feature       |             Description            |
|---------------------|------------------------------------|
| Number of Atoms     | Number of Atoms in the Molecule    | 
| Formal Charge       | Electric charge on the Molecule    | 
| Heavy Atoms         | Number of Heavy Atoms              | 
| Molar Refractivity  | Polarizability of Molecule         | 
| Rotatable Bonds     | Number of Rotatable Bonds          | 
| MW                  | Molecular Weight of Molecule       | 
| LogP                | Partition Coefficient of Molecule  | 
| NumHDonors          | Number of Hydrogen Bond Donors     | 
| NumHAcceptors       | Number of Hydrogen Bond Acceptors  | 
| SAmapping           | Topological Surface Area           | 
| Number of Rings     | Number of Rings in Molecule        | 

## EDA

Almost all the predictors are approximately normally distributed with some righ skewed outliers. 

![Target Distribution](https://github.com/ethankim00/CovidDrugDiscovery/blob/master/target_distribution.png?raw=true)

The Hit scores are also normally distributed with only 13 drugs exceeding the cutoff to be considered a hit. 


![Feature Correlatins](https://github.com/ethankim00/CovidDrugDiscovery/blob/master/feature_correlations.png?raw=true)

A number of features are highly correlated in ways that make sense based on their physical interpretation. Therefore a number of the most highly correlated features were dropped from the final model. 

## Modeling

I fit a multivariable linear model as a baseline for comparison. I then fit a random forest regression model with hyperparameter tuning using GridSearchCV with 3 fold cross validation. Overall, the best predictor was the random forest with `n_estimators = 120`, `max_depth = 8` and `max_features = log2`

### Model Comparison

## Conclusions

The model correctly places Remdesivir, a antiviral known to be effective above the hit cutoff. 
This method uses primarily chemical descriptors of a molecule and thus has difficulty predicting how a drug will perform in the complex biological interactions involved in viral inhibition. Future work could focus on using known molecule - protein motif interactions or known moleculal functions in biological pathways to predict efficacy as a viral inhibitor. 

## Sources
- [CHEMBL Database](ebi.ac.uk/chembl/g/#browse/activities/filter/src_id%3A52)

Inspiration
- [Ken Jee](https://www.youtube.com/channel/UCiT9RITQ9PW6BhXK0y2jaeg)
- [Data Professor](https://www.youtube.com/c/DataProfessor/featured)
