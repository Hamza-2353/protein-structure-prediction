# 🧬 Protein Structure Prediction & Analysis using AlphaFold2

**Course Assignment — Bioinformatics**  
**Student:** Muhammad Uzair Khan  
**Instructor:** Tanveer Ahmad  
**Date:** April 2026

---

## Overview

This repository contains the complete assignment for predicting and analyzing the 3D structure of **Human Lysozyme C (PDB: 1REX)** using **AlphaFold2** via the **ColabFold** pipeline (MMseqs2 backend).

AlphaFold2 is a deep learning model developed by DeepMind that predicts protein 3D structure from amino acid sequence alone. At CASP14 (2020), it achieved a median GDT_TS of **92.4** — compared to ~40–50 for the best conventional methods over 26 years of progress — marking a paradigm shift in computational biology.

---

## Target Protein

| Property | Value |
|---|---|
| **Protein name** | Human Lysozyme C |
| **PDB ID** | [1REX](https://www.rcsb.org/structure/1REX) |
| **UniProt** | P61626 |
| **Length** | 130 amino acids |
| **Organism** | *Homo sapiens* |
| **Function** | Cleaves β-1,4 glycosidic bonds in bacterial peptidoglycan |
| **Crystal resolution** | 1.5 Å |

**FASTA Sequence (Chain A):**
```
>1REX_A|Human Lysozyme C|Homo sapiens
KVFERCELARTLKRLGMDGYRGISLANWMCLAKWESGYNTRATNYNAGDRSTDYGIFQINS
RYWCNDGKTPGAVNACHLSCSALLQDNIADAVACAKRVVRDPQGIRAWVAWRNRCQNRDV
RQYVQGCGV
```

---

## Repository Structure

```
protein-structure-prediction/
│
├── AlphaFold2_Lysozyme_1REX_Assignment.ipynb   ← Main notebook (run this)
├── README.md                                    ← This file
├── REPORT.md                                    ← Written analysis & results
└── requirements.txt                             ← Python dependencies (reference)
```

---

## How to Run

### Option 1 — Google Colab (Recommended)

1. Click the badge below to open directly in Colab:

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/YOUR_GITHUB_USERNAME/protein-structure-prediction/blob/main/AlphaFold2_Lysozyme_1REX_Assignment.ipynb)

2. Go to **Runtime → Change runtime type → GPU (T4)**
3. Go to **Runtime → Run all**
4. Wait ~15–20 minutes for the prediction to complete
5. Results (PDB files, plots, ZIP) will download automatically

### Option 2 — Manual Upload

1. Go to [colab.research.google.com](https://colab.research.google.com)
2. **File → Upload notebook** → select `AlphaFold2_Lysozyme_1REX_Assignment.ipynb`
3. Set runtime to **GPU** and run all cells

---

## Pipeline Steps

```
Input Sequence (1REX FASTA)
        │
        ▼
MMseqs2 MSA Search          ← Fast homology search via ColabFold API
        │
        ▼
Evoformer (48 blocks)       ← Transformer processing MSA + pair representations
        │
        ▼
Structure Module (8 blocks) ← Converts representations to 3D coordinates
        │
        ▼
5 Model Predictions         ← Ranked by mean pLDDT score
        │
        ▼
Amber Relaxation            ← Energy minimisation of best model
        │
        ▼
Output: PDB + pLDDT + PAE   ← Structure + confidence metrics
```

---

## Expected Results

| Metric | Expected Value | Interpretation |
|---|---|---|
| Mean pLDDT | > 90 | Very high confidence |
| PAE (mean) | < 5 Å | Low inter-residue error |
| MSA depth | > 500 sequences | Deep alignment — good signal |
| GDT vs crystal | ~90–95 | Near-experimental accuracy |

---

## Confidence Metrics Explained

### pLDDT (per-residue Local Distance Difference Test)
Measures AlphaFold2's confidence in local structure at each residue (0–100):

| Score | Colour | Meaning |
|---|---|---|
| > 90 | 🔵 Dark Blue | Very high confidence |
| 70–90 | 🩵 Light Blue | High confidence |
| 50–70 | 🟡 Yellow | Low confidence |
| < 50 | 🟠 Orange | Very low — likely disordered |

### PAE (Predicted Aligned Error)
Measures confidence in the **relative position** of every pair of residues. Dark green = low error = high confidence. Especially useful for multi-domain proteins.

---

## Tools & References

| Tool | Purpose | Citation |
|---|---|---|
| [AlphaFold2](https://github.com/deepmind/alphafold) | Structure prediction | Jumper et al., *Nature* 2021 |
| [ColabFold](https://github.com/sokrypton/ColabFold) | Fast MSA + AF2 interface | Mirdita et al., *Nature Methods* 2022 |
| [MMseqs2](https://github.com/soedinglab/MMseqs2) | MSA generation | Steinegger & Söding, *Nature Biotechnology* 2017 |
| [RCSB PDB](https://www.rcsb.org) | Sequence & structure source | Berman et al., *Nucleic Acids Res.* 2000 |

### Full References
1. Jumper, J. et al. Highly accurate protein structure prediction with AlphaFold. *Nature* **596**, 583–589 (2021).
2. Mirdita, M. et al. ColabFold: Making protein folding accessible to all. *Nature Methods* **19**, 679–682 (2022).
3. Abramson, J. et al. Accurate structure prediction of biomolecular interactions with AlphaFold 3. *Nature* **630**, 493–500 (2024).
4. RCSB PDB entry 1REX. https://www.rcsb.org/structure/1REX
5. Lecture slides: *AlphaFold 2.0: Theory, Architecture and Scope* — Instructor: Tanveer Ahmad (April 2026).

---

## Acknowledgements

- [ColabFold](https://github.com/sokrypton/ColabFold) by Sergey Ovchinnikov, Milot Mirdita & Martin Steinegger
- AlphaFold2 by the DeepMind team
- KOBIC & Söding Lab for MMseqs2 server resources

---

*Assignment submitted for the Bioinformatics course — Department of Bioinformatics & Computational Biology*
