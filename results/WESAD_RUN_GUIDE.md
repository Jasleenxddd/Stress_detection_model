# Corrected complete WESAD suite

Entry point: `codes/wesad_suite.py`. Results: `results/wesad_complete/`.

This is a new evaluation using the Paper 1 topology, not a reproduction of the old small model's scores.
It uses real subjects, three inner validation subjects, training-only scaling, 10-second windows,
50% overlap, polyphase anti-alias downsampling to 70 Hz, and 95% single-class window purity.
The raw dataset is not modified. Every eligible window is retained; no pilot subsampling is used.

The fixed training settings are 100 maximum epochs, validation-loss early stopping with patience 20,
batch size 64, AdamW (0.001 learning rate / 0.004 weight decay), class weighting derived only from
training labels, and one initialization seed (42). This is not a multi-seed study.

## Included evaluations

- Exp1: 15 LOSO folds for HABC and five grouped HABC splits.
- Exp2: five architecture variants on the same fixed subject split; the HABC fit is reused.
- Exp4: all four baseline variants also run on the same 15 LOSO folds. The primary paired test is
  two-sided Wilcoxon with Holm correction across four comparisons; paired t-tests are secondary.
- Exp3: fixed-split HABC test perturbations, SNR 30/20/10/5/0 dB and scalar zero masking
  5/10/15/20/30%, each with five prespecified corruption seeds.
- Exp8/10: confusion matrices and class reports reuse the exact saved fixed-split predictions.

Total: 84 neural-network fits. Full-data training on CPU may take a substantial amount of time.
No cloud services, paid compute, or dataset uploads are used. SWELL is outside this WESAD run.
An overlapping-window random standard split is not introduced to chase the old 96.63% score.

## Progress and resuming

`wesad_complete/status.json` records the current job, epoch, timing, and training/validation losses.
`wesad_complete/suite_stdout.log` and `suite_stderr.log` record background output.
`wesad_complete/process.json` records the launched process ID. Check that process before starting
another worker; do not run duplicate workers against the same output folder.

If the worker has stopped, resume from the project root:

```powershell
.\.venv\Scripts\python.exe -u codes/wesad_suite.py
```

Completed fits are skipped. An interrupted fit restarts from its initial seed; completed folds are preserved.
Code/config/dataset changes are rejected by the run manifest to avoid silently mixing runs.

## Validation and reporting

Each fit saves its subject split, scaler, epoch history, best validation checkpoint, predictions,
sample indices and raw window start positions. On completion, the suite independently recomputes
metrics from saved probabilities, refits each scaler from recorded training subjects, verifies test
identities, checks checkpoint selection and validates all 51 robustness prediction sets.

Final files are `validation.json`, `summary.json`, `significance.json`, `RESULTS.md`, and figures.
Only a `complete` status with passing validation establishes completion. Intermediate metrics are
provisional. Saved p-values do not establish equivalence or remove the dependence between overlapping
LOSO training folds. Corruption repeats quantify perturbation variability, not training-seed variability.
