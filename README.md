# Wiring to Molecular Identity

## A Connectivity-Based Machine Learning Proof-of-Concept for Neurotransmitter Prediction in the Drosophila Olfactory System

### Overview

This project asks whether connectivity architecture within the Drosophila olfactory system contains predictive information about neuronal molecular neurotransmitter identity.

The project combines curated neurotransmitter annotations with neuronal connectivity features derived from the Drosophila hemibrain connectome and evaluates whether machine-learning models can distinguish cholinergic (ACh) from GABAergic neurons.

This is a computational proof-of-concept. The observed relationships are associative and should not be interpreted as evidence that connectivity causally determines neurotransmitter identity.

---

## Scientific question

**Can circuit wiring contain predictive information about molecular neuronal identity?**

The project focuses on whether connectivity architecture can provide information about neurotransmitter class in olfactory neurons.

The work is motivated by the broader goal of molecular connectomics: integrating neuronal molecular identity with large-scale circuit connectivity.

---

## Dataset

The final machine-learning dataset contains:

- **165 individual neurons**
- **65 canonical olfactory cell types**
- **16 connectivity features**
- **2 neurotransmitter classes**
  - Acetylcholine (ACh)
  - GABA

Connectivity information was obtained from the Drosophila hemibrain connectome.

Neurotransmitter labels were derived from curated molecular evidence associated with canonical olfactory cell types.

The final dataset contains no missing feature values and no identifier-based label leakage.

---

## Connectivity features

The 16 final features describe:

### Outgoing connectivity

- `outgoing_edges`
- `outgoing_synapses`
- `outgoing_mean_synapses`
- `outgoing_median_synapses`
- `outgoing_max_synapses`
- `outgoing_synapse_sd`

### Incoming connectivity

- `incoming_edges`
- `incoming_synapses`
- `incoming_mean_synapses`
- `incoming_median_synapses`
- `incoming_max_synapses`
- `incoming_synapse_sd`

### Directionality

- `outgoing_incoming_edge_ratio`
- `outgoing_incoming_synapse_ratio`

### Overall connectivity

- `total_edges`
- `total_synapses`

---

## Machine-learning models

The project evaluates:

- DummyClassifier baseline
- Logistic Regression
- Random Forest
- XGBoost

Logistic Regression provides the primary interpretable baseline.

Random Forest and XGBoost provide nonlinear model comparisons.

---

## Validation strategy

Because multiple neurons can belong to the same canonical cell type, ordinary random train/test splitting can lead to overly optimistic estimates.

The primary validation therefore uses:

**5-fold StratifiedGroupKFold**

with:

- stratification by neurotransmitter class
- grouping by canonical cell type
- fixed random state for reproducibility

This prevents neurons belonging to the same canonical cell type from being distributed across training and validation folds.

---

## Primary result

The primary Logistic Regression model achieved:

- **Balanced accuracy: 0.929 ± 0.060**
- **Macro F1: 0.808 ± 0.136**
- **ACh recall: 0.927 ± 0.050**
- **GABA recall: 0.931 ± 0.096**

These results indicate that connectivity features contain predictive information associated with neurotransmitter class within this curated olfactory dataset.

The result should not be interpreted as demonstrating that connectivity causally determines neurotransmitter identity.

---

## Feature interpretation

Held-out permutation importance identified the strongest individual contributions from synaptic-weight distribution features.

The top three features were:

1. `outgoing_mean_synapses`
2. `incoming_max_synapses`
3. `outgoing_median_synapses`

The results suggest that the predictive signal is associated more strongly with patterns of synaptic weighting and connectivity architecture than with simple directional ratios alone.

---

## PCA

Principal-component analysis showed:

- PC1: **68.02%** explained variance
- PC2: **14.48%** explained variance
- PC1 + PC2: **82.50%** explained variance

PCA is used as an exploratory visualization rather than as the primary statistical test.

---

## Robustness analyses

The project includes:

- cell-type-grouped cross-validation
- feature-family sensitivity analysis
- log-transformed feature sensitivity
- synapse-threshold sensitivity
- leakage auditing
- group-preserving permutation testing
- held-out permutation feature importance

The group-preserving permutation analysis produced:

- observed balanced accuracy: **0.929**
- null mean: approximately **0.499**
- empirical p ≈ **0.010**

This result is interpreted cautiously because some permuted validation folds can lack one of the two classes due to the limited number of GABAergic cell types.

---

## Interactive prototype

A Gradio-based interactive prototype is included within the research notebook.

The interface demonstrates how a trained Logistic Regression model can accept the 16 connectivity features and return predicted neurotransmitter probabilities.

The interface is a demonstration of the computational model and does not constitute independent experimental validation.

---

## Reproducibility

The analysis was developed in Python.

The workflow proceeds from:

1. retrieval of olfactory connectivity data
2. retrieval and curation of neurotransmitter annotations
3. neuron-to-cell-type mapping
4. connectivity feature engineering
5. construction of the final ML dataset
6. exploratory analysis
7. baseline modelling
8. grouped cross-validation
9. robustness analysis
10. feature interpretation
11. biological interpretation
12. publication-quality figures and tables
13. interactive model demonstration
14. final scientific audit

---

## Repository structure

```text
wiring-to-molecular-identity/
├── README.md
├── LICENSE
├── CITATION.cff
├── requirements.txt
├── notebook/
│   └── wiring_to_mol_id_final.ipynb
├── data/
│   └── final_olfactory_neurotransmitter_ml_dataset.csv
├── results/
│   ├── figures/
│   └── tables/
└── gui/
```

The GUI is retained as part of the research notebook rather than as a separate permanent deployment.

---

## Limitations

1. The neurotransmitter ground truth is based on curated evidence and is not experimentally generated within this project.
2. The dataset contains substantially more ACh than GABA neurons.
3. Only 12 canonical cell types are GABAergic in the final 65-type molecular dataset.
4. Connectivity features are aggregate representations and do not capture the full biological complexity of neuronal circuits.
5. The analysis is restricted to the selected olfactory neuron population.
6. Machine-learning predictions are associative rather than mechanistic.
7. The interactive GUI is a demonstration interface, not an independent validation experiment.
8. Predictive performance should not be interpreted as proof that connectivity determines molecular identity.

---

## How to cite this project

If this repository, its code, methodology, analyses, or derived results materially contribute to a scholarly publication, presentation, or other research output, please cite the original project.

### Citation

**Dhawan, U. (2026). _Wiring to Molecular Identity: A Connectivity-Based Machine Learning Proof-of-Concept for Neurotransmitter Prediction in the Drosophila Olfactory System_.**

The archival DOI will be added following the Zenodo release.

This repository contains a `CITATION.cff` file with machine-readable citation metadata.

Please also cite the original datasets, connectome resources, and scientific publications from which the underlying data and annotations were obtained.

---

## Citation and attribution

This project is intended to remain attributable to its original author.

If this repository, its code, methodology, analyses, or derived results materially contribute to a scholarly publication, please provide an appropriate citation to this project and its archival DOI once available.

The MIT License applies to the project code. It does not replace the requirement to appropriately acknowledge the scientific sources, datasets, and prior publications underlying the work.

---

## Outputs

The repository contains:

- final machine-learning dataset
- publication-quality figures
- publication-quality tables
- final research notebook
- reproducibility metadata
- scientific documentation

---

## License

The code in this repository is released under the MIT License.

Copyright (c) 2026 Utkarshita Dhawan.

See the `LICENSE` file for the complete license text.
