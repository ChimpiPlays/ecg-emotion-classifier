# ECG Emotion Classifier

This repository contains a **minimal, ready-to-run baseline** for **ECG-based emotion detection** using classic machine learning.
It includes preprocessing (filtering, normalization), feature extraction (time/frequency domain, simple HRV proxies),
model training (SVM, RandomForest), and evaluation with a **synthetic sample dataset** so you can test immediately.

> Replace the synthetic data in `data/raw` with your real ECG samples when ready.
> The code accepts per-sample CSV files named as `<label>_<id>.csv` with one column named `ecg`.

## Project Structure
```
ecg-emotion-classifier/
├─ data/
│  ├─ raw/                 # Put your raw ECG CSV files here (label_id.csv with 'ecg' column)
│  └─ processed/           # Auto-generated features and splits
├─ models/                 # Saved trained models (.pkl)
├─ notebooks/              # (optional) experiments
├─ results/                # Metrics, confusion matrices
├─ src/
│  ├─ feature_extraction.py
│  ├─ preprocess.py
│  ├─ train.py
│  └─ evaluate.py
├─ requirements.txt
└─ README.md
```

## Quickstart
1) (Optional) Create a virtual environment and install requirements:
```bash
pip install -r requirements.txt
```

2) **Preprocess & extract features** (reads `data/raw/*.csv` and writes `data/processed/features.csv`):
```bash
python src/preprocess.py
```

3) **Train models** (saves best model to `models/best_model.pkl` and metrics to `results/`):
```bash
python src/train.py
```

4) **Evaluate** on the held-out test split:
```bash
python src/evaluate.py
```

## Input Data Format
Place ECG samples as **CSV files** in `data/raw/` with filenames like:
```
happy_001.csv, angry_002.csv, neutral_003.csv, ...
```
Each file should contain **one column named `ecg`** with the ECG time series values (floats).  
Example (first 5 rows):
```
ecg
0.103
0.115
0.097
...
```

## Notes
- The included synthetic dataset is **only for demonstration**. Replace it with real ECG to get meaningful results.
- Feature extraction includes basic statistics, simple frequency-domain energy in bands, and a naive peak-based HRV proxy.
- Update labels list in `preprocess.py` if your label set differs.

## License
MIT
