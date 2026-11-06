# Sensor Time-Series Classification

Research code for stress, affective-descriptor and activity classification using CNN, BiLSTM and attention models. The repository retains the experiment notebooks and local datasets; manuscript and Overleaf sources are excluded.

## Main code

| File | Purpose |
| --- | --- |
| `codes/wesad_corrected.py` | Corrected WESAD preprocessing and pilot/model builders |
| `codes/wesad_suite.py` | Resumable WESAD subject-independent evaluation suite |
| `Wesad_Colab_Run.ipynb` | Colab launcher for the corrected WESAD suite |
| `MuSe_Corrected_Colab.ipynb` | Corrected supplementary MuSe descriptor experiment |
| `UTD1_Experiment.ipynb` | Original UTD-MHAD experiment and ablations |
| `Wesad_Corrected_Pilot.ipynb` | Corrected WESAD pilot notebook |

Original experiment notebooks (`Wesad1_Experiment.ipynb`, `Muse1_Experiment.ipynb`, `Swell_KW_1_Experiment.ipynb`, `Copy_of_BTP_UTD (1).ipynb`) and the other files in `codes/` are retained for provenance. They use older protocols and are not interchangeable with the corrected evaluations. Notebook execution outputs have been cleared for source control; original executed notebooks are in the local cleanup backup.

## Setup

Use Python 3.11 or newer with a compatible TensorFlow release, or open the Colab notebooks in Google Colab.

```powershell
python -m venv .venv
.\.venv\Scripts\python.exe -m pip install -r requirements.txt
```

Run from the repository root:

```powershell
.\.venv\Scripts\python.exe -u codes/wesad_suite.py
```

See `results/WESAD_RUN_GUIDE.md` for subject splits, runtime settings, progress tracking and resume behavior. Do not start duplicate workers against the same results folder. A stale status file is not proof that a run is currently active or complete.

The MuSe Colab notebook defaults to `MyDrive/MuSe_paper2/muse_v3.csv`. To use temporary Colab storage, upload the CSV to `/content`, set `CSV_PATH = Path('/content/muse_v3.csv')`, remove the Drive mount, and set `OUT = Path('/content/muse_results') / stamp`. Download the results archive before the session ends.

## Datasets and results

See `datasets/README.md` for the local layout. All existing dataset files are preserved. WESAD recordings exceed ordinary GitHub file limits and are excluded from Git; obtain them separately or explicitly configure Git LFS before publishing them. Smaller local datasets remain eligible for Git tracking. Dataset ownership and licenses remain with their respective providers.

Existing checkpoints, predictions, cache files and run records remain in `results/` locally and are excluded from Git. Preserve them when resuming or validating experiments.

## Interpretation

- MuSe labels are constructed from valence/arousal predictors. Its scores describe a supplementary label-aligned descriptor task, not independent emotion recognition.
- The original UTD implementation processes 20 joint-indexed steps containing flattened coordinate histories. Attention is over those encoded positions, not frame times.
- The original SWELL notebook does not establish participant-independent evaluation with verified participant identifiers.
- Use corrected run artifacts and their exact protocols for reporting; do not mix scores from different fits or splits.
