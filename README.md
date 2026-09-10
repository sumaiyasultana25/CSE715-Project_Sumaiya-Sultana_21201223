GNN-Based BERT for Understanding Context from Music

Course: Neural Networks and Fuzzy Systems 
Author: Sumaiya Sultana (ID: 21201223)

A hybrid system combining a fine-tuned BERT (DistilBERT) text encoder with a GraphSAGE-based Graph Neural Network (GNN), fused via cross-attention, for multi-label music genre/context understanding on the Free Music Archive (FMA) dataset.

Tasks Completed
 Task 1 — BERT Multi-Label Genre Tagger Test Macro-F1: 0.375 | Test Micro-F1: 0.459 (Note: artist-grouped train/test split used to prevent data leakage — a random split initially produced an inflated 0.928 macro-F1.)
 Task 2 — GraphSAGE on Music Structure Graphs + CNN Baseline GraphSAGE Test Macro-F1: 0.231 | CNN (mel-spectrogram) Test Macro-F1: 0.439
 Task 3 — Cross-Attention GNN–BERT Fusion + Ablation Study Fusion Test Macro-F1: 0.727 (vs. BERT-only 0.340, Early-Concat 0.597)
 Task 4 — Contrastive MusicCaps Alignment (not attempted — bonus/future work)
Repository Contents
File	Description
task-1_ID_21201223.ipynb	Task 1: BERT fine-tuning notebook (Kaggle)
task2-gnn-music-graph_ID21201223.ipynb	Task 2: Graph construction, GraphSAGE, and CNN baseline notebook (Kaggle)
task3-gnn-bert_ID_21201223.ipynb	Task 3: Cross-attention fusion + ablation study notebook (Kaggle)
CSE715 Project_ID-21201223.pdf	Final project report
results/	Evaluation tables, training curves, and t-SNE visualization
Key Results Summary
Task 1: Artist-Leakage Correction
Evaluation Setting	Test Macro-F1	Test Micro-F1
Random split (leaked)	0.928	0.943
Artist-grouped split (corrected)	0.375	0.459
Task 2: GraphSAGE vs. CNN Baseline
Model	Test Accuracy	Test Macro-F1
GraphSAGE (chroma segment graphs)	0.250	0.231
CNN (mel-spectrogram)	0.450	0.439
Task 3: Ablation Study
Model	Val Macro-F1	Test Macro-F1	Val→Test Gap
BERT-only	0.710	0.340	−0.370
GNN-only*	0.128	—	—
Early-Concatenation	0.634	0.597	−0.037
Cross-Attention (Full Fusion)	0.750	0.727	−0.024

*GNN-only predictions collapsed toward the dataset's base label-positivity rate (macro AUC-PR = 0.095); see report for full discussion.

Key Findings
Artist-level data leakage significantly inflates reported performance in music metadata classification — random splits allow models to memorize artist identity rather than learn genre signals.
Feature richness matters more than architecture: the CNN outperforms the GNN in Task 2 primarily because it sees full mel-spectrograms while the GNN sees only 12-dim averaged chroma per segment.
The weaker modality improves generalization of the stronger one: despite the GNN branch being individually weak, its inclusion in the fusion model dramatically reduces overfitting compared to BERT-only (val→test gap of −0.024 vs. −0.370).

How to Run:

All notebooks were developed and run on Kaggle with a single NVIDIA T4 GPU, using the FMA: Free Music Archive Small & Medium dataset. To reproduce:

Open each notebook in Kaggle.
Attach the FMA dataset as an input.
For Task 3, attach the Task 1 and Task 2 notebooks' outputs as additional inputs (pretrained checkpoints are loaded from there).
Run all cells top to bottom.
Report
See CSE715 Project_ID-21201223.pdf for the full write-up, including methodology, equations, discussion, limitations, and references.
