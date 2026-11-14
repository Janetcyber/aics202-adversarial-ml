# AICS-202 Adversarial Machine Learning: Lab Evidence

Student: Janet Anya Okewu-Ihezie
Course: ICDFA AICS-202, Adversarial Machine Learning

## Status
All four laboratory notebooks have been run. Analyses are in the analysis folder and screenshots are in the evidence folder. The PDF report is submitted separately.

## Environment
- Machine: Dell laptop, Windows 10
- Python: 3.13.12
- Libraries: see requirements.txt (full list in pip_freeze.txt)
- Random seed: 42 (data split and models)
- Dataset: scikit-learn digits (1,797 images, 64 features). 1,347 training and 450 test records, stratified 75/25.

## How to run
```
py -m venv .venv
.\.venv\Scripts\python.exe -m pip install -r requirements.txt
.\.venv\Scripts\python.exe -m pip install notebook
.\.venv\Scripts\python.exe -m notebook
```
Open each notebook and use Kernel, then Restart Kernel and Run All Cells.

## Results (from my own runs)
| Lab | Result |
|---|---|
| 01 Baseline | Clean test accuracy 0.962 (433 of 450). Most frequent confusion: true 8 predicted as 1 (4 times). |
| 02 FGSM | Accuracy 0.907, 0.791, 0.624, 0.516 and 0.204 at epsilon 0.03, 0.07, 0.10, 0.12 and 0.18. At epsilon 0.10, 29% of pixel changes were smaller than epsilon (24.3% clipped, 4.7% zero gradient). |
| 03 Poisoning | Accuracy 0.962, 0.960, 0.958 and 0.933 with 0, 5, 10 and 20% of training labels changed (random corruption only). |
| 04 Defence | Baseline: clean 0.962, FGSM 0.516, PGD 0.489. Augmented training (epsilon 0.10): 0.940, 0.284, 0.260. Smaller augmentation epsilons (0.03, 0.05) were also tested and did not beat the baseline under attack. Decision: reject as tested. |

## Evidence index
| ID | Evidence | Location |
|---|---|---|
| E01 | Baseline accuracy, confusion matrix, threat model | evidence/E01 files, Lab 01 notebook |
| E02 | FGSM table, curves, image pairs, clipping check | evidence/E02 files, Lab 02 notebook, analysis/Lab02_Analysis.md |
| E03 | Corruption results, chart, hash check, integrity plan | evidence/E03 files, Lab 03 notebook, analysis/Lab03_Analysis.md |
| E04 | Clean, FGSM and PGD comparison, variants, decision memo | evidence/E04 files, Lab 04 notebook, analysis/Lab04_Analysis.md |

## Scope and safety
Only the built-in scikit-learn digits dataset and locally trained models were used. No external systems were tested. Results apply to this small controlled setup and are not a certification of model security.

## AI assistance declaration
I used Claude (Anthropic) for explanations, step-by-step guidance and draft wording. I ran all code myself, and all reported results come from my own runs.