# Optimizing-Drug-Response-Prediction-from-RNA-Seq-Data
This project investigates how clustering and weighted ridge regression can improve the external performance of machine learning models that predict drug response from RNA-seq data of perturbed samples. It builds upon the work of Szalai et al., who trained a ridge regression model on the CTRP-L1000-24h dataset. Surprisingly, a model trained on the larger REMATCHED dataset performed worse on the external Mix-seq dataset. This project explores whether reweighting training samples, either directly or via clustering, can improve generalization.

The code is organized to reproduce all results presented in the BEP report. It includes:
Data loading and preprocessing
t-SNE dimensionality reduction
DBSCAN clustering
Weighted ridge regression (with and without clustering)
Evaluation on the Mix-seq dataset
Visualizations (e.g., t-SNE plots)

Two main strategies were explored:
1) Clustering-Based Weighted Ridge Regression
    t-SNE was applied to reduce the dimensionality of the REMATCHED dataset.
    DBSCAN was used to identify clusters.
    Sample weights were assigned based on cluster-level viability metrics (e.g., mean, standard deviation).
2) Direct Weighted Ridge Regression
    Weights were assigned to individual samples based on sample-level metrics without clustering.
All models are based on ridge regression; only the weighting strategy differs.

The following data sets are used:
lm_74709.csv: Gene expression matrix (LINCS-L1000)
siginfo_74709.csv: Signature metadata including viability
lfc_with_viab_calced.csv: Mix-seq log fold change data
meta_with_viab_calced.csv: Mix-seq metadata
cpd_withrep.csv: Compound annotations including MoA
Datasets_used_week_4.pkl: Preprocessed and filtered datasets used for reproducibility
Be aware that most file paths are hardcoded and should be updated for the user.

Requirements: Python 3.8+
Required libraries:
scikit-learn
pandas
numpy
matplotlib
seaborn
plotly
joblib
igraph
leidenalg
tqdm
kneed
Pillow

How to run:
Make sure all required datasets are available in the specified paths.
Run the scripts or notebooks in order:
Data loading and preprocessing
t-SNE and clustering
Weight assignment
Model training and evaluation
Visualization
Note: t-SNE results are saved and reloaded to ensure reproducibility, as they vary between runs.

Results:
The best-performing model achieved a Pearson correlation of 0.5383 on the Mix-seq dataset.
This is an improvement of 0.2201 over the REMATCHED baseline model (0.3182) and 0.1272 over the Szalai model (0.4111).
Clusters enriched for nuclear process inhibition MoAs were particularly informative.

Notes:
The code is written for this Bep project and may require adaptation for other datasets or environments.
For reproducibility, many intermediate results (e.g., t-SNE outputs) are saved and reused.
