# biostat_707_final
Final project for BIOSTAT 707. 

# Health Data Project
By: Sydney Shimizu (sydney.shimizu@duke.edu) and Tirzah Asir (tirzah.asir@duke.edu)

## Goals
Our goal is to test whether unsupervised clustering of METABRIC gene expression recovers the PAM50 breast cancer subtypes, whether those clusters are stable under resampling, and how well regularized and tree-based models predict the subtype from a small gene set.

## Roles
Sydney: Missingness plots and exploratory analysis, PCA, k-means clustering, lasso model + calibration, writing up sections on data + PCA + k-means + lasso

Tirzah: Hierarchical clustering, comparison of clusters with PAM50, random forest model, writing up sections on hierarchical clustering, stability, the forest and the baselines

For more information, please see our comprehensive doc titled [METABRIC_Subtypes.pdf](METABRIC_Subtypes.pdf), thanks! :)

# Non-Health Data Project
By: Ahmed Hussain (ahmed.hussain1@duke.edu) and Yaoyang Li (yaoyang.li@duke.edu)

## Goals
Our goal is to test how well student background, early click activity, and assessment submissions from the first 28 days predict whether students pass, fail, or withdraw in the Open University Learning Analytics Dataset (OULAD). We will compare regularized and tree-based models, evaluate discrimination and calibration, and test performance over time, across courses, and across demographic subgroups while preventing information leakage.

## Roles
Ahmed: Table widening and concatenation, clickstream features and exploratory analysis, gradient boosting, temporal and cross-course tests, writing up sections on data + click features + boosting

Yaoyang: Remaining data transformations, missingness handling and leakage controls, baseline and elastic-net models, evaluation and calibration, subgroup and sensitivity analyses, writing up sections on preprocessing + validation + interpretation

Both: Agree on the analysis setup and shared validation splits, review each other's code, and prepare the report and presentation

For more information, please see our comprehensive doc titled [OULAD.pdf](OULAD.pdf), thanks! :)
