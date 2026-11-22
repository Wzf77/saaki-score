# SA-AKI 28-Day In-Hospital Mortality Risk Calculator (24 h version)

A browser-based calculator for 28-day in-hospital mortality in patients with
sepsis-associated acute kidney injury (SA-AKI), using variables measured within
0–24 h of ICU admission.

It shows **two probabilities side by side**:

- **Machine-learning model** — Gaussian process classifier (GPC, 25 features),
  the ABscore-best model (temporal holdout AUROC 0.760; eICU-CRD external
  model-selection cohort AUROC 0.716).
- **Bedside scorecard** — 10 variables, integer points 0–34 (holdout AUROC
  0.706; eICU AUROC 0.667).

The two probabilities are intentionally **not blended into a single number**:
the ML model uses all 25 variables, the scorecard only 10 with integer bins, and
an average of the two had lower discrimination than the ML model alone in both
the temporal holdout (0.752 vs 0.760) and eICU (0.711 vs 0.716). The page instead
shows both on one 0–100% axis, with a shaded range and a concordance message.

## Usage

All calculations run locally in the browser; no patient data are uploaded,
transmitted, or stored. The model files must be served over HTTP
(`python -m http.server 8000`) or GitHub Pages; opening `index.html` via
`file://` cannot load them.

## Files

| File | Description |
| --- | --- |
| `index.html` | Single-page application; no backend required |
| `meta.json` | Feature order, labels, units, standardization constants, scorecard configuration |
| `gpc_model.json` | GPC support vectors (10,917 × 25), weights, kernel width |
| `verify_set.csv` | 200 eICU cases with expected ML and scorecard probabilities |
| `.nojekyll` | Disables Jekyll processing on GitHub Pages |

## Deploying to GitHub Pages

1. Create a **public** repository and upload all files here to the root.
2. **Settings → Pages → Build and deployment**: source = *Deploy from a branch*,
   branch = `main`, folder = `/ (root)`.
3. Open `https://<username>.github.io/<repository>/`.

## Re-generating the model files

Run `Rscript ../code/29_export_web_model.R`. It verifies the browser-side kernel
formula against `predict(..., type = "prob")` on 200 eICU cases and stops if the
maximum absolute difference is ≥ 1e-8.

## Disclaimer

Research and educational use only. Not medical advice; final decisions must be
made by clinicians using the full clinical picture.
