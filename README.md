# DL-TCR-TRB-CDR3-Classification
Tumor vs Normal TCR Classification Using Deep Learning on TRB CDR3 Sequences
This project investigates whether deep learning can distinguish between tumor and normal tissue based on patient-level TRB CDR3 sequences. The aim is to explore the potential of T-cell receptor (TCR) repertoire signatures for tumor classification.

We applied preprocessing, tokenization, padding, and normalization to real immune repertoire data (sourced from dbGaP/GDC). Two modeling strategies were evaluated:
- Mean Pooling with Embedding + Linear Layer
- LSTM-based sequence encoding

Despite modest performance, the project demonstrates a fully reproducible pipeline with thoughtful EDA, deep learning modeling, and suggestions for future improvements.


---

## Methodology

- **Input:** Patient-level CDR3 sequences (`Sample ID`, `CDR3`, `label`)
- **Tokenization:** Each amino acid is mapped to an integer token
- **Padding:** All CDR3s padded to 22 amino acids
- **Normalization:** Exactly 20 CDR3s per patient (downsample or pad)
- **Labeling:** `Tumor` vs `Normal` (binary classification)

---

## Models

### 1. Mean Pooling Baseline
- Embedding → Mean of all CDR3 embeddings → Dense layer
- Achieved ~59% accuracy, F1 ~0.58

### 2. LSTM-Based Model *(optional)*
- Sequence → LSTM → Final hidden → Dense layer
- Slightly worse performance; limited by data size and variability

---

##  Exploratory Data Insights

- CDR3 sequence lengths range from 6 to 22 AAs (median ~14)
- Tumor/Normal samples have 20–70 unique CDR3s per patient
- Tokenization preserves biological granularity while enabling modeling

---

## Limitations & Learnings

- Limited number of normal samples (n ≈ 277)
- No clear predictive signal learned from short TRB CDR3s
- Still, this project is valuable for understanding end-to-end deep learning workflows on immunogenomic data

---

## Future Directions

- Try attention-based models (e.g., Transformers)
- Tune hyperparameters with Optuna
- Include V/D/J gene features
- Use larger cohort from other cancer types (if available)

---

## Resources & Links

- Blog write-up: _Coming soon_
- Data source: [GDC Data Portal](https://portal.gdc.cancer.gov/)
- Author: [Tushar Singh]([https://your-website-link.com](https://tushar-bioinfo.github.io/learning-bioinformatics/)])
