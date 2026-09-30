# Data Availability Statement — drop-in replacement

Replace the current sentence in the manuscript:

> "The data that support the findings of this study are available from the corresponding author
> upon reasonable request. The XGBoost training pipeline, SHAP analysis, baseline comparison
> scripts and figure-generation code will be deposited in a public GitHub repository upon
> acceptance."

## Option A — once the Zenodo DOI exists (use this before submission if possible)

> The code that supports the findings of this study — the XGBoost training pipeline, Mackenzie
> (1981)/TEOS-10/EOF baseline comparisons, SHAP analysis, and the LLM tactical-interpretation
> layer — is openly available on Zenodo at https://doi.org/10.5281/zenodo.23066120 (Powsi et al.,
> 2026). The underlying in-situ and satellite observational data are publicly available from the
> Argo float network (argo.ucsd.edu) and the World Ocean Database
> (ncei.noaa.gov/products/world-ocean-database); the compiled and quality-controlled dataset used
> in this study is available from the corresponding author upon reasonable request.

## Option B — if you must submit before minting the DOI

> The code that supports the findings of this study — the XGBoost training pipeline, baseline
> comparisons, SHAP analysis, and the LLM tactical-interpretation layer — will be made openly
> available on Zenodo upon acceptance, with a permanent DOI. The underlying in-situ and satellite
> observational data are publicly available from the Argo float network (argo.ucsd.edu) and the
> World Ocean Database (ncei.noaa.gov/products/world-ocean-database); the compiled dataset used in
> this study is available from the corresponding author upon reasonable request.

Notes:
- Ocean Engineering's own author guide asks specifically for a Data Availability Statement, and
  reviewers increasingly check that the stated repository actually resolves — so Option A is
  preferable if your timeline allows getting the DOI first (Zenodo mints a DOI within minutes of
  upload).
- Once you archive on Zenodo, also add the in-text citation "(Powsi et al., 2026)" for the code to
  the **References** list in the same author-year format as your other entries, e.g.:
  `Powsi, I.J., Miah, R., Alam, M.K., 2026. Bay of Bengal SSP Reconstruction Code (Version 1.0.0) [Software]. Zenodo. https://doi.org/10.5281/zenodo.23066120`
- If you'd rather not name the corresponding-author-on-request path for the compiled dataset, you
  can instead deposit the CSV itself on Zenodo (as a separate or combined deposit) and cite that
  DOI directly — this is the strongest option for reviewer reproducibility, since it removes the
  "upon request" friction entirely.
