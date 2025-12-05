# DL-TRB-CDR3-Classification
Tumor vs Normal TCR Classification Using Deep Learning on TRB CDR3 Sequences

This project investigates whether deep learning can distinguish between tumor and normal tissue based on patient-level TRB CDR3 sequences. The goal is to understand whether T-cell receptor (TCR) repertoire signatures contain meaningful signals for tumor classification.

We applied preprocessing, tokenization, padding, and normalization to immune repertoire data sourced from dbGaP/GDC. Two modeling strategies were evaluated:

- Mean Pooling with Embedding + Linear Layer  
- LSTM-based sequence encoding  

Despite modest performance, the project demonstrates a fully reproducible workflow with structured EDA, deep learning modeling, and clear avenues for improvement.

---

## Methodology

- **Input:** Patient-level CDR3 sequences (`Sample ID`, `CDR3`, `label`)  
- **Tokenization:** Each amino acid mapped to an integer token  
- **Padding:** All CDR3s padded to a maximum length of 22 amino acids  
- **Normalization:** Exactly 20 CDR3s per patient (downsample or pad)  
- **Labeling:** `Tumor` vs `Normal` (binary classification)

---

## Models

### 1. Mean Pooling Baseline
- Embedding → Mean of all CDR3 embeddings → Dense layer  
- Achieved approx. 59% accuracy (F1 ≈ 0.58)

### 2. LSTM-Based Model
- CDR3 sequence → LSTM → Final hidden state → Dense layer  
- Performance slightly lower than the baseline, limited by dataset size and variability

---

## Exploratory Data Insights

- CDR3 sequence lengths range from 6 to 22 amino acids (median ≈ 14)  
- Tumor and normal samples contain 20–70 unique CDR3s per patient  
- Tokenization preserves biological granularity while enabling neural network modeling  

---

## Limitations & Learnings

- Limited number of normal samples (n ≈ 277)  
- TRB CDR3s may not provide a strong classification signal in isolation  
- Still valuable as an end-to-end example of deep learning applied to immunogenomic data  

---

## Additional Information

- Blog write-up: *Coming soon*  
- Data source: https://portal.gdc.cancer.gov/  
- Author: Tushar Singh — https://tushar-bioinfo.github.io/learning-bioinformatics/
