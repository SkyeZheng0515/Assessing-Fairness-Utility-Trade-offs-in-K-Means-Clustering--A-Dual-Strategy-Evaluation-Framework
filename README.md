# Assessing Fairness in Clustering: A Dual-Strategy Evaluation Framework


## Setup

```bash
pip install -r requirements.txt
```

Download the five datasets and place them under `data/`:

| Dataset | Source |
|---------|--------|
| Adult Income | https://archive.ics.uci.edu/dataset/2/adult |
| COMPAS | https://github.com/propublica/compas-analysis |
| German Credit | https://archive.ics.uci.edu/dataset/144/statlog+german+credit+data |
| Default Credit Card | https://archive.ics.uci.edu/dataset/350/default+of+credit+card+clients |
| Law School (LSAC) | https://github.com/damtharvey/law-school-dataset |

## Algorithms

K-Means  
Fairlet Decomposition  
Balanced Fair K-means (BFKM)  
Cluster-level Centroid Fairness (CCF)  
Post-Processing Based Nearest Foreign Point (PP-NFP)  
Post-Processing Based Gini (PP-Gini)  
Rawlsian K-Means

## Execute

**Step 1 — Run experiments**

```
Strategy1_all_algorithms.ipynb
Strategy2_kmeans_fairlet_bfkm.ipynb
Strategy2_ccf_ppnfp_ppgini_rawlsian.ipynb
```

Each notebook saves results as `.pkl` and `.csv` files under `results/strategy1/` and `results/strategy2/`.

**Step 2 — Compile result tables (manual)**

From the `.csv` output of Strategy 1 and Strategy 2, compile the following four Excel files and place them in `results/normalized/`:

```
results/normalized/S1 Quality.xlsx
results/normalized/S1 Fairness.xlsx
results/normalized/S2 Quality.xlsx
results/normalized/S2 Fairness.xlsx
```

**Step 3 — Run normalization**

```
04_result_normalization.ipynb
```

Reads the four Excel files above and outputs scaled (0-1) to the same `results/normalized/` folder.
