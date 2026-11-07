# SA-AKI 28-Day In-Hospital Mortality Risk Calculator

A browser-based calculator for 28-day in-hospital mortality in patients with sepsis-associated acute kidney injury (SA-AKI). It combines an ExtraTrees machine-learning model (17 features) with a simplified integer scorecard (9 variables).

## Usage

The application is entirely client-side. All calculations run locally in the browser; no patient data are uploaded, transmitted, or stored.

Requirements: Chrome or Edge 80+ (for `DecompressionStream` support).

## Files

| File | Description |
| --- | --- |
| `index.html` | Single-page application entry point; no backend required |
| `forest.bin.gz` | ExtraTrees forest (gzip-compressed binary; decompressed in the browser) |
| `meta.json` | Feature order, standardization parameters, and decision threshold |
| `verify_set.csv` | Verification cases used by the in-page self-test |
| `.nojekyll` | Disables Jekyll processing on GitHub Pages |

## Deploying to GitHub Pages

1. Create a **public** repository and upload all files in this directory to the repository root.
2. In **Settings → Pages → Build and deployment**, set **Source** to `Deploy from a branch`, **Branch** to `main`, and **Folder** to `/ (root)`. Save.
3. Wait 1–2 minutes, then open `https://<username>.github.io/<repository>/`.
4. Optional custom domain: add a file named `CNAME` containing the domain (without `http://`), then create a CNAME DNS record pointing to `<username>.github.io`.

## Updating the deployed site

The live repository is <https://github.com/Wzf77/saaki-score/tree/main>.

### Option A — GitHub web interface

1. Open <https://github.com/Wzf77/saaki-score/tree/main>.
2. Choose **Add file → Upload files**.
3. Drag the updated `index.html` (and any other changed files) into the page.
4. Commit the changes to `main`.
5. GitHub Pages redeploys in 1–2 minutes. Hard-refresh the site if the browser serves a cached copy.

### Option B — Git command line

```bash
git clone https://github.com/Wzf77/saaki-score.git
cd saaki-score
# copy the updated files into this directory
git add index.html README.md
git commit -m "Translate UI to English and refine design"
git push origin main
```

Do not delete `.nojekyll`, `forest.bin.gz`, `meta.json`, or `verify_set.csv`; the application needs them at the repository root.

## Updating the model

After retraining, regenerate `forest.bin.gz`, `meta.json`, and `verify_set.csv` from the training pipeline, then replace the corresponding files in the repository. If the feature order or scorecard bins changed, update `index.html` as well. Commit the changes to `main`; GitHub Pages redeploys automatically.

## Disclaimer

This tool is intended for research and educational demonstration only. It does not constitute medical advice, and final clinical decisions must be made by clinicians using the full clinical picture.
