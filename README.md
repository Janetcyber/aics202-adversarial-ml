# AICS-202 Adversarial Machine Learning: Lab Evidence

Student: Janet Anya Okewu-Ihezie
Course: ICDFA AICS-202, Adversarial Machine Learning

## Status
Lab 01 notebook and evidence complete. Written analysis in progress. Labs 02 to 04 to be added.

## Environment
- Machine: Dell laptop, Windows 10
- Python: Python 3.13.12
- Dependencies: see requirements.txt (full list in pip_freeze.txt)
- Random seed: 42

## How to run
py -m venv .venv
.\.venv\Scripts\python.exe -m pip install -r requirements.txt
.\.venv\Scripts\python.exe -m pip install notebook
.\.venv\Scripts\python.exe -m notebook

## Lab 01 results (from my own run)
- Dataset: 1,797 images, 64 features
- Train and test records: 1,347 and 450
- Clean test accuracy: 0.9622
- Most frequent confusion: true 8 predicted as 1 (4 times)
- Evidence: see the evidence folder (E01 files)

## Scope and safety
Only the built-in scikit-learn digits dataset and locally trained models were used. No external systems were tested.

## AI assistance declaration
I used Claude (Anthropic) for explanations, step-by-step guidance and draft wording. I ran all code myself, and all results above come from my own runs.
