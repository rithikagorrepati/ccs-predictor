# Adduct-Specific CCS Prediction for Untargeted Metabolomics

## Overview

Collision cross section is a molecular property measured using ion mobility mass spectrometry. It reflects the effective gas-phase size and shape of an ion and provides an additional measurement that can support compound identification in untargeted metabolomics.

A significant gap persists between available experimental CCS reference data and the expansive chemical space encountered in metabolomics.

Conducted in the **Fernández Lab at Georgia Tech**, the goal of this project was to determine how accurately CCS could be predicted from molecular structure for **[M+H]⁺, [M−H]⁻, and [M+Na]⁺** ions.

An adduct-specific approach was used because the relationship between molecular structure and CCS differs depending on the ionized form of the molecule.

> **Note:** This repository is a public overview of the research. Source code, trained models, and molecule-level datasets are not included because public release is subject to laboratory approval and applicable data/model licensing requirements.
---

## Dataset

 **METLIN-CCS**, the experimental resource underlying this work, contains measurements from more than **27,000 molecular standards** and over **185,000 CCS values** across multiple ion types.
 
The final modeling dataset contained:

| Dataset characteristic | Size |
| --- | ---: |
| Molecule/adduct records | **57,402** |
| Adduct classes | **3** |

The modeled adducts were **[M+H]⁺, [M−H]⁻, and [M+Na]⁺**.

Molecular records underwent preprocessing and quality-control steps before model development. A total of **3,822 dimer-related records** were removed from the final modeling dataset.

---

## Leakage-Aware Data Splitting

The same molecular identity can occur in multiple records and if related records are allowed to appear in both training and test data, model performance can be artificially inflated.

The workflow therefore used **molecule-aware grouping during dataset splitting and cross-validation**, keeping records associated with the same molecular identity together.

This provided a more rigorous estimate of performance on molecules not used to train the model.

---

## Results

The three adduct-specific models were evaluated on a frozen held-out test set containing **11,482 molecule/adduct records**.

### Held-Out Test Performance

| Adduct | n | R² | MAE (Å²) | Median RE (%) |
| --- | ---: | ---: | ---: | ---: |
| **[M+H]⁺** | 4,910 | **0.9395** | 2.9092 | **1.1697** |
| **[M−H]⁻** | 3,598 | **0.8848** | 4.2079 | **1.5445** |
| **[M+Na]⁺** | 2,974 | **0.8699** | 3.5760 | **1.3579** |

Across the three adducts, held-out **R² ranged from 0.8699 to 0.9395**, with median relative errors between **1.17% and 1.54%**. The **[M+H]⁺** model showed the strongest overall performance.

Performance differed across adducts, supporting the use of separate adduct-specific models rather than treating all ion types as a single prediction problem.

---

## Project Contribution

I worked on this project **end-to-end under the guidance of my PI, Dr. Facundo M. Fernández, in the Fernández Lab at Georgia Tech**, from data preprocessing and molecular representation through model development, validation, performance analysis, and preparation of research outputs.

---

## Research Dissemination

### ASMS 2026

**Geometry-driven Machine Learning for Accurate Collision Cross Section Predictions in Untargeted Metabolomics Workflows**

American Society for Mass Spectrometry Annual Conference  
San Diego, California, USA

### Metabolomics Society 2026

**Adduct-Specific Machine Learning for Accurate Collision Cross Section Prediction in Untargeted Metabolomics**

Metabolomics Society Annual Meeting  
Buenos Aires, Argentina

---

## Future Direction

The next phase of this research focuses on **extending CCS prediction to lipids**.

---

## Code and Data Availability

This repository is intentionally limited to a **public overview of the research project**.

The following are not included:

- source code from the research workflow,
- trained models or model checkpoints,
- molecule-level CCS records,
- molecular identifiers,
- train/validation/test datasets,
- prediction files,
- and other laboratory research assets.

Public release of the implementation and trained models is subject to **laboratory approval and applicable licensing requirements**.

---

## Reference

Baker, E. S. et al. **METLIN-CCS: an ion mobility spectrometry collision cross section database.** *Nature Methods* 20, 1836–1837 (2023).
