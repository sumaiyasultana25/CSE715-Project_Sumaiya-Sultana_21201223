# Results Summary

## Task 1: BERT Multi-Label Genre Classifier

### Artist-Leakage Correction
| Evaluation Setting | Test Macro-F1 | Test Micro-F1 |
|---|---|---|
| Random split (leaked) | 0.928 | 0.943 |
| **Artist-grouped split (corrected)** | **0.375** | **0.459** |

### Example Predictions
| Text | True Genres | Predicted Genres |
|---|---|---|
| Nummer Da Luminous – Bleached Dream – Untitled-3 | Electronic | Experimental, Electronic, Drone |
| Deadly Combo – Unattainable – Can I Get A Clap | Hip-Hop | Rock, Hip-Hop |
| SHOMOMOSE – [EPV_103] | Experimental, Electronic, Noise | Experimental, Electronic, Ambient Electronic |

See `task1_curves.png` for training/validation loss and F1 curves.

---

## Task 2: GraphSAGE vs. CNN Baseline

| Model | Test Accuracy | Test Macro-F1 |
|---|---|---|
| GraphSAGE (chroma segment graphs) | 0.250 | 0.231 |
| **CNN (mel-spectrogram)** | **0.450** | **0.439** |

See `task2_gnn_curves.png` (GraphSAGE training curves) and
`task2_gnn_vs_cnn.png` (head-to-head comparison across epochs).

---

## Task 3: GNN–BERT Fusion — Ablation Study

| Model | Val Macro-F1 | Test Macro-F1 | Val→Test Gap |
|---|---|---|---|
| BERT-only | 0.710 | 0.340 | −0.370 |
| GNN-only* | 0.128 | — | — |
| Early-Concatenation | 0.634 | 0.597 | −0.037 |
| **Cross-Attention (Full Fusion)** | **0.750** | **0.727** | **−0.024** |

*GNN-only predictions collapsed toward the dataset's base label-positivity
rate (macro AUC-PR = 0.095, near the random-ranking baseline for this label
distribution).

### Qualitative Case Studies
- **Perfect match**: "The Very Most – ePop017 – Congrizzle 4evzzz" →
  True = {Rock, Punk, Indie-Rock}, Predicted = {Rock, Punk, Indie-Rock}
- **Partial match**: "KINGS OF THE CITY – No Guts EP – The Devil" →
  True = {Hip-Hop, Rap}, Predicted = {Hip-Hop}
- **Complete miss**: "Loretta Kelley – Live Golden Festival 2010 –
  Ruske-Sara, telespringar" → True = {International}, Predicted = {Folk}

See `task3_tsne.png` for the t-SNE visualization of fused embeddings, colored
by genre.
