# Gaussian Decomposition of Survival Differences

Statistical analysis pipeline accompanying the manuscript:

> Midlovets K. K., Kybenko D. O., Krasnienkov D. S. **Analysis of mortality dynamics: assessment of the stability and directionality of intergroup differences.**

This repository contains the Python implementation of the analytical framework that combines Kaplan–Meier survival analysis, Savitzky–Golay smoothing, Gaussian decomposition of the survival difference function ΔS(t), and bootstrap-based validation.

---

## What the pipeline does

1. Computes pointwise survival difference ΔS(t) = S₁(t) − S₂(t) between two Kaplan–Meier curves.
2. Smooths ΔS(t) with a Savitzky–Golay filter (window = 7, polyorder = 2).
3. Splits the smoothed signal into positive and negative envelopes.
4. For each envelope, fits a sum of Gaussian components iteratively, selecting the number of components by minimising the Bayesian Information Criterion (BIC).
5. Computes confidence intervals from the covariance matrix of the non-linear least-squares fit.
6. Validates the detected peaks by bootstrap resampling of the underlying survival data.

The pipeline produces:

- A reconstructed ΔS(t) curve with explicit Gaussian components (location μ, amplitude, width σ).
- Goodness-of-fit metrics (MSE, RMSE, R²).
- Bootstrap stability estimates for each peak.
- Publication-quality figures at 600 DPI.

---

## Requirements

- Python ≥ 3.10
- See [`requirements.txt`](requirements.txt) for package versions.

Install with:

```bash
pip install -r requirements.txt
```

---

## How to run

The repository contains a single Jupyter notebook:

- [`gaussian_decomposition_survival.ipynb`](gaussian_decomposition_survival.ipynb)

The notebook was developed in Google Colab and contains a `drive.mount()` cell at the top. To run locally:

1. Remove or skip the first cell (`from google.colab import drive`).
2. Change `INPUT_FILE` paths in cells 2, 5, and 6 to point to your local data file (e.g. `./data/dataset.xlsx`).
3. Execute cells sequentially.

To run in Colab:

1. Open the notebook in Colab.
2. Upload your data file to Google Drive.
3. Update `INPUT_FILE` paths to match your Drive structure.
4. Run all cells.

---

## Input data format

The pipeline expects an Excel file with mortality counts per day for each group. The default loader (`load_data()` in cell 5) reads the following columns:

- `exp_dead_f` / `exp_dead_m` — daily deaths in experimental group, females / males
- `exp_alive_f` / `exp_alive_m` — daily survivors in experimental group, females / males
- `ctrl_dead_f` / `ctrl_dead_m` — daily deaths in control group, females / males
- `ctrl_alive_f` / `ctrl_alive_m` — daily survivors in control group, females / males

The first 3 rows of the input file are treated as a header block and skipped.

---

## Files

| File | Description |
|---|---|
| `gaussian_decomposition_survival.ipynb` | Main analysis notebook |
| `requirements.txt` | Python package dependencies |
| `LICENSE` | MIT licence |
| `.gitignore` | Standard Python and Jupyter ignore rules |
| `README.md` | This file |

---

## Citation

If you use this code in your research, please cite the accompanying manuscript:

```
Midlovets K. K., Kybenko D. O., & Krasnienkov D. S. (2026). Analysis of mortality dynamics:
assessment of the stability and directionality of intergroup differences. [Journal name, in review].
```

---

## Licence

This code is released under the MIT Licence. See [`LICENSE`](LICENSE) for details.

---

## Contact

- Kostiantyn K. Midlovets — midlovetskon@gmail.com
- Danylo O. Kybenko — d.kibenko@gmail.com
- Dmytro S. Krasnienkov — krasnenkovd@gmail.com

D. F. Chebotarev State Institute of Gerontology, National Academy of Medical Sciences of Ukraine
