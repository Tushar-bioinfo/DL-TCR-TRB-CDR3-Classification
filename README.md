# DL-TCR-TRB-CDR3-Classification
Tumor vs Normal TCR Classification Using Deep Learning on TRB CDR3 Sequences
This project investigates whether deep learning can distinguish between tumor and normal tissue based on patient-level TRB CDR3 sequences. The aim is to explore the potential of T-cell receptor (TCR) repertoire signatures for tumor classification.

We applied preprocessing, tokenization, padding, and normalization to real immune repertoire data (sourced from dbGaP/GDC). Two modeling strategies were evaluated:
- Mean Pooling with Embedding + Linear Layer
- LSTM-based sequence encoding

Despite modest performance, the project demonstrates a fully reproducible pipeline with thoughtful EDA, deep learning modeling, and suggestions for future improvements.
