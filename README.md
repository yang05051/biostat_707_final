# biostat_707_final
Final project for BIOSTAT 707. 

METABRIC Subtypes Proposal
By: Sydney Shimizu and Tirzah Asir
Objective
Our goal is to test whether unsupervised clustering of METABRIC gene expression recovers the PAM50 breast cancer subtypes, whether those clusters are stable under resampling, and how well regularized and tree-based models predict the subtype from a small gene set.
Data
We will be using the METABRIC breast cancer gene expression and clinical data, on cBioPortal (study). From the study data, we will use three elements:

Gene expression: Microarray expression for thousands of genes, one row per tumour sample. cBioPortal provides both log-scale intensities and z-scores; we will choose one and standardize genes ourselves so that scaling stays a documented choice.
PAM50 label: The CLAUDIN_SUBTYPE column in the clinical table. It also contains claudin-low and unclassified patients, so we will decide how to treat those classes before any modelling and report the class counts.
Clinical variables: Variables like ER and HER2 status, age, tumour size, grade, and the cohort a patient belongs to. We will use these for exploratory purposes and check that the clusters don’t just follow a technical variable.

Unit of Analysis: Patient, and each patient has one sample. This study has 2,509 patients: 79% have expression data and subtype label. The patients without expression data are also missing subtype label and 16 other clinical variables, so we will be excluding these patients in our analysis.

Outcome: PAM50 subtype (located in the CLAUDIN_SUBTYPE) column

Predictors: Gene expression (the z-score matrix with thousands of genes per matrix)
Exploratory Data Analysis
We downloaded and loaded the data before writing this proposal, so the project does not depend on anything we have not yet seen. In a Python notebook we have already done the following…
Downloaded the data
Read in the data
Identified the primary outcome and key predictors
Plotted missingness
Investigated the structure of the data using PCA and k-means (k=4) on five marker genes (ESR1, PGR, ERBB2, MK167, and GATA3). 
Methods
The table shows how each element of the course workflow appears in this project. Python (pandas, scikit-learn) in Jupyter notebooks, with the environment managed by pixi so the whole analysis reruns from one command, as in the checkpoints.
Required element
Our plan
Exploratory analysis
Distribution and variance of genes; class balance; PCA and heatmaps colored by PAM50 subtype, cohort and ER status; correlation among genes; outlying samples.
Missing-data handling
Count missing values by gene, patient and clinical variable. Exclude patients without expression or a subtype label and describe them. Drop genes missing in more than a set fraction (the cut-off chosen from the missingness plot) and impute the rest with the training-fold median, inside each fold.
Validation without leakage
Patient-level folds stratified by subtype; nested cross-validation for tuning; every preprocessing step refit inside training folds. 
Regularized model
Multinomial lasso or elastic net (scikit-learn logistic regression) predicting PAM50 subtype from the gene data; the penalty picks a small gene set and is tuned in inner folds.
Tree-based model
Random forest (scikit-learn) on the same filtered genes; number of genes tried per split and minimum node size tuned inside training folds; permutation importance for interpretation.
Baseline
Two: always predict the most common subtype, and a nearest-centroid classifier on the 50 PAM50 genes (the published-style approach) with centroids estimated inside training folds. The centroid classifier should do very well because the labels came from those genes; that shows the ceiling and the circularity.
Discrimination
One-vs-rest AUROC for each subtype and the macro average, balanced accuracy and a confusion matrix, also by cohort and ER status. For clusters: ARI and NMI against PAM50.
Calibration
Per-subtype reliability plots, multiclass log loss and Brier score, and calibration slope and intercept per subtype. Recalibrate inside the training folds if the models are miscalibrated.
Clustering and stability (Aims 1 and 2)
PCA, then k-means and Ward hierarchical clustering for k = 2 to 10, with k chosen by silhouette score and the elbow in within-cluster variance and k = 5 reported for the PAM50 comparison. Stability from 100 to 200 subsamples of 80% of patients, drawn without replacement: ARI against the full-data partition, per-cluster agreement and a consensus matrix.
Real structure versus artifact
Negative control: shuffle each gene separately across patients and rerun the same pipeline. Sensitivity: rerun without the 50 PAM50 genes, with other gene counts and with another number of components.



Division of Work

Phase
Sydney Shimizu
Tirzah Asir
Set-up
Data download and alignment; missingness and exploratory analysis
Repository, pixi environment and report skeleton; evaluation functions (ARI, NMI, resampling loop) tested on simulated data
Structure
PCA; k-means clustering
Hierarchical clustering; comparison of clusters with PAM50
Evidence
Negative controls and sensitivity runs; lasso model and its calibration
Stability by resampling; random forest, baselines and discrimination
Write-up
Sections on data, PCA, k-means, controls and the lasso
Sections on hierarchical clustering, stability, the forest and the baselines
Together
Decisions on genes, k range and label classes; discussion and limitations; fresh-clone test with a README that gives the commands and run time; final presentation
Same

