# Bay of Bengal Sound-Speed Profile Reconstruction — Code Release

Physics-constrained XGBoost reconstruction of sound-speed profiles in the Bay of Bengal, with
SHAP-based explainability and an LLM tactical-interpretation layer.

Code accompanying: *A Dual-Layer AI Framework for Real-Time Sound Speed Profile Reconstruction and
Acoustic Risk Mapping in the Bay of Bengal*, Israt Jahan Powsi, Rayhan Miah, Md Khorshed Alam,
submitted to Ocean Engineering, 2026.

Department of Physics, University of Barishal, Barishal-8254, Bangladesh.
Corresponding author: Md Khorshed Alam (dmkalam@bu.ac.bd).

This repository reproduces the physics-constrained XGBoost sound-speed-profile (SSP) reconstruction
model, the Mackenzie (1981) / TEOS-10 / EOF baselines, the SHAP feature-attribution analysis, and the
LLM tactical-interpretation layer reported in the manuscript.

## Authors

- Israt Jahan Powsi — [ORCID: 0009-0008-0484-897X](https://orcid.org/0009-0008-0484-897X)
- Rayhan Miah — [ORCID: 0009-0006-0900-590X](https://orcid.org/0009-0006-0900-590X)
- Md Khorshed Alam (corresponding author) — [ORCID: 0000-0002-3925-4900](https://orcid.org/0000-0002-3925-4900)

Department of Physics, University of Barishal, Barishal-8254, Bangladesh.

## Repository contents

```
notebooks/
  core_pipeline.ipynb   # Data loading, XGBoost model, baselines (Table 2), SHAP,
                         # LLM interpretation layer (Section 3.5), automated
                         # consistency checks
requirements.txt        # Python dependencies
LICENSE                 # MIT License
CITATION.cff            # Machine-readable citation metadata
README.md               # This file
```

## Data availability

This code expects a compiled CSV (`Bay_of_Bengal_Reconstructed_Full.csv`) combining Argo float
profiles, World Ocean Database records, and co-located satellite SST/SSH/CO2 products, as described
in Section 2.1 of the manuscript. Raw source data are publicly available from their original
repositories (Argo, World Ocean Database) but are not redistributed here. Set the environment
variable `SSP_DATA_PATH` to point the notebook at your local copy, or place the file alongside the
notebook under its default name.

## Environment setup

```bash
python -m venv venv
source venv/bin/activate       # Windows: venv\Scripts\activate
pip install -r requirements.txt
```

## API key (LLM interpretation layer only)

Section 3.5 of the notebook calls the Groq API (Llama-3.1-8B-Instruct). Get a free key at
console.groq.com/keys and set it as an environment variable — never hardcode it in the notebook:

```bash
export GROQ_API_KEY="your-key-here"        # macOS/Linux
setx GROQ_API_KEY "your-key-here"          # Windows
```

Sections 1–2 (baselines, Table 2) run without any API key.

## Reproducing the reported results

Run `notebooks/core_pipeline.ipynb` top to bottom:

1. **Setup** — installs dependencies.
2. **Feature correlation check** — CO2 vs. Actual_SSP correlation (Section 5.2 discussion).
3. **Main model + baselines** — trains XGBoost on the official 80/20 depth-stratified split
   (`random_state=42`) and reproduces Table 2 (XGBoost, Mackenzie 1981, TEOS-10, climatological
   baseline, EOF regression).
4. **LLM tactical-interpretation layer** — generates tactical summaries for 1,000 stratified
   test-set samples via the Groq API.
5. **Automated SHAP-consistency check** — objective, reproducible check of whether each summary
   names the feature with the largest-magnitude SHAP value for that row.
6. **Heuristic content-validity screen** — see "Known limitations" below before relying on this
   step's output.

## Known limitations and disclosures (please read before citing this release)

- **Train/test split.** The 80/20 split is stratified by depth quintile, not grouped by horizontal
  location, so different depths from the same water-column profile can appear on both sides of the
  split. See the manuscript's Limitations discussion; a location-grouped split is left as future
  work.
- **Section 5 ("Heuristic content-validity screen") is an automated, rule-based keyword check, not
  a human expert review.** If earlier drafts of the manuscript describe this step as an "expert
  review," that wording should be corrected before submission, or a genuine human-expert review
  should be conducted and reported in its place.
- This release contains only the pipeline stages that produced the metrics and figures reported in
  the manuscript. Exploratory code (alternative LLM backends, retry scripts, illustrative/synthetic
  demonstration plots not derived from real model output) has been excluded to avoid confusion
  about what was actually used to generate the reported results.

## Citation

If you use this code, please cite both the paper and the software (see `CITATION.cff`):

> Powsi, I.J., Miah, R., Alam, M.K., 2026. A Dual-Layer AI Framework for Real-Time Sound Speed
> Profile Reconstruction and Acoustic Risk Mapping in the Bay of Bengal. *Ocean Engineering*,
> [vol/pages]. https://doi.org/[paper DOI]
>
> Powsi, I.J., Miah, R., Alam, M.K., 2026. Bay of Bengal SSP Reconstruction Code (Version 1.0.0)
> [Software]. Zenodo. https://doi.org/10.5281/zenodo.XXXXXXX

## License

MIT License — see `LICENSE`.
