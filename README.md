# SA-AKI 28-Day In-Hospital Mortality Risk Calculator (24 h version)

Single-file, browser-based calculator for 28-day in-hospital mortality in
patients with sepsis-associated acute kidney injury (SA-AKI), using variables
measured within 0–24 h of ICU admission.

## What it shows

- **Machine-learning model** — Gaussian process classifier (25 features),
  ABscore-best model.
- **Bedside scorecard** — 10 variables, integer points 0–34.
- Both probabilities on one 0–100% axis, with a shaded range and a concordance
  note. The range is **not** a validated ensemble.
- Clinical **reference values** under each input.
- An **Extrapolation** warning when an input lies outside the observed training
  range; in that case the ML estimate is unreliable and the scorecard should be
  used.

## Files

| File | Required | Description |
| --- | --- | --- |
| `index.html` | yes | Entire application, including the embedded model data (about 3 MB) |
| `.nojekyll` | yes (GitHub Pages) | Disables Jekyll processing |

No other files are needed. `index.html` works when opened directly
(double-click) and when served over HTTP or GitHub Pages.

## Deploying to GitHub Pages

1. Create a **public** repository.
2. Upload `index.html` and `.nojekyll` to the repository root.
3. **Settings → Pages → Build and deployment**: source = *Deploy from a branch*,
   branch = `main`, folder = `/ (root)`. Save.
4. Open `https://<username>.github.io/<repository>/`.

## Re-generating

The editable page template is `../code/web_index_template.html`. After changing
it:

1. `Rscript ../code/29_export_web_model.R`
2. `python ../code/30_embed_web_js.py`
3. Inline `meta.js` and `model.js` into the template and save as `index.html`.

## Disclaimer

Research and educational use only. Not medical advice; final decisions must be
made by clinicians using the full clinical picture.
