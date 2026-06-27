# Description of the Model

**ML models**. Those included three gradient boosting models (LGBM,
XGBoost, CatBoost), a linear model (BayesianRidge), two light LGBM
stacking estimators on top of the gradient boosting models (with and
without BayesianRidge, respectively), Pytorch Tabular with GANDALF
backend, TabICL, and TabPFN. For Pytorch Tabular and all three gradient
boosting models, parameters were tuned using Optuna; BayesianRidge, the
stacking estimators, TabICL and TabPFN were used with the stock
parameters. Base models were run independently, and their predictions
were aggregated using NNLS.

**Chemical representations**. Those were obtained by extracting
CheMeleon embeddings and augmenting them with rdkit2d descriptors.
CheMeleon model was fine-tuned on the single concentration data using
the full system training (no encoder freeze). Additionally, several
variants of multi-task fine-tuning (pEC50, single concentration, and
counter-assay data) have been tested, but none was found to outperform
fine-tuning on the single concentration data alone.

**Data**. Only the data provided by the PXR challenge were used.
Augmenting those data with ChEMBL chemicals was found to actually
degrade the ML performance. ML training and inference on Analog set 2
was performed using splitting the set into multiple parts and focusing
the training set for each part independently, as described in \[1\].

# Performance comments

**ML models**. The two stacking estimators consistently got negligible
NNLS weights. The weights for the other ML models varied but stayed
comparable to one another.

# References

1. https://arxiv.org/abs/2602.23303 .
