# Interpretation and Final Thoughts

This project aimed to classify **tumor vs. normal** lung tissue using **T-cell receptor (TRB) CDR3 sequences**, applying deep learning to biological sequence data. Below is a breakdown of the steps we took, why we made certain decisions, and the lessons learned along the way.

---

## 🛠Step-by-Step Workflow and Decisions

### 1. Raw Data Collection & Labeling
- We started with two separate files containing TRB CDR3 sequences from tumor and normal lung tissue samples.
- Each row represented one CDR3 sequence and was labeled with the sample ID and tissue type (`tumor` or `normal`).
- We combined both into a single dataset and added the appropriate labels.

### 2. Exploratory Data Analysis (EDA)
- We explored the number of unique CDR3s per patient.
- Tumor samples had a wide range of CDR3 counts (2–174), while normal samples ranged from 11–181.
- **Decision:** We chose a normalization strategy—fixing 20 CDR3s per patient—either by padding with a special token or by randomly sampling.

### 3. Preprocessing for Deep Learning
- Each CDR3 sequence was tokenized: every amino acid was converted to an integer using a custom vocabulary.
- CDR3s were padded to a fixed length (30 amino acids).
- Each patient was then represented by a 2D matrix of shape `(20 CDR3s × 30 tokens)`.
- We saved the data in a structured `.jsonl` format for downstream modeling.

### 4. Modeling Approaches
We implemented and compared two baseline models:

- **Mean Pooling Model:** Averaged embeddings across each CDR3 and then across all 20 sequences for classification.
- **LSTM Model:** Processed each CDR3 sequence using an LSTM and aggregated the final hidden states to make predictions.

### 5. Training and Evaluation
- We split data into 80% training and 20% validation.
- Trained for up to 100 epochs using binary cross-entropy loss and Adam optimizer.
- Saved the best model based on validation accuracy.

---

## Performance Summary

| Model        | Best Val Acc | Accuracy | Precision (Tumor) | Recall (Tumor) | F1 (Tumor) |
|--------------|--------------|----------|-------------------|----------------|------------|
| Mean Pooling | ~0.54        | 0.58     | 0.56              | 0.74           | 0.64       |
| LSTM Attempt | ~0.56        | N/A      | N/A               | N/A            | N/A        |

- Both models showed moderate performance with accuracy hovering around 0.54–0.58.
- Recall for tumor was higher, suggesting the models leaned toward detecting tumor samples more reliably than normal ones.
- However, precision remained low, indicating many false positives.

---

## Limitations and Challenges

- **Biological complexity:** TCR CDR3 sequences are highly variable and their predictive patterns may not be linearly separable or easy to learn from small datasets.
- **Data imbalance:** Tumor samples were more prevalent, and although we balanced during training, the diversity of tumor sequences could still dominate.
- **Label noise:** Some CDR3s might not be specific to the tumor or normal tissue type, leading to ambiguity.
- **No additional features:** We trained only on raw sequences, without metadata (e.g., HLA type, clinical data), which could be valuable.

---

## How Can We Improve?

1. **Use larger and more diverse datasets**  
   Including more patients would allow the model to generalize better.

2. **Experiment with better architectures**  
   Try:
   - Transformer-based models (e.g., BERT-like attention).
   - CNNs for local motif detection.
   - Hybrid models combining LSTM with attention.

3. **Incorporate metadata**  
   Adding patient-level or sequence-level features (e.g., V/D/J gene usage, HLA type, clonality) could significantly boost performance.

4. **Use pre-trained embeddings**  
   Like `ProtBERT`, `ESM`, or `TAPE` for amino acid representation, which may capture biochemical and structural properties more effectively.

5. **Perform motif enrichment or clustering analysis**  
   Analyze which motifs are common in tumor vs. normal and use these as features.

---

## Final Thoughts

This project was an excellent opportunity to:
- Practice deep learning on biological sequences.
- Implement full pipelines from preprocessing to evaluation.
- Understand the limitations of applying DL to real-world omics data.

While the results were not state-of-the-art, they reflect a **realistic and valuable baseline**. Future improvements are entirely possible—and expected—as data grows and models evolve.
