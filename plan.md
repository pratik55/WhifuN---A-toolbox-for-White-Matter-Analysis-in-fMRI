# WhiFuN Documentation Update Plan

## Background

The current docs are based on an old version (v1) of WhiFuN and also contain significant **Read the Docs tutorial template leftovers** (`lumache.py`, `usage.rst`, `api.rst`, `pyproject.toml`). WhiFuN 3.2 is the current version and has been substantially redesigned. This plan captures every change needed to bring the documentation up to date.

**Sources used:**
- GitHub README: https://github.com/Brain-Connectivity-Lab/WhiFuN/tree/WhiFuN_3.2
- Published paper: Jain et al. (2025), *Imaging Neuroscience*, DOI: 10.1162/IMAG.a.3, PMC12319995
- WhiFuN Manual PDF: https://github.com/Brain-Connectivity-Lab/WhiFuN/blob/WhiFuN_3.2/WhiFuN%20Manual.pdf

---

## File Action Summary

| File | Action |
|---|---|
| `docs/source/conf.py` | Edit: update release/version to 3.2 |
| `README.rst` | Edit: replace template with WhiFuN description |
| `pyproject.toml` | Edit: update name/authors/description |
| `lumache.py` | **Delete** |
| `docs/source/index.rst` | Rewrite |
| `docs/source/getting_started.rst` | Significant rewrite |
| `docs/source/setup.rst` | Major rewrite |
| `docs/source/preprocessing_and_qc.rst` | Major rewrite |
| `docs/source/functional_networks.rst` | Major rewrite |
| `docs/source/usage.rst` | Complete replace → scripting guide |
| `docs/source/api.rst` | Fix/replace → MATLAB `help` reference |
| `docs/source/visualization.rst` | **New file** |
| `.readthedocs.yaml` | Fix YAML schema error (`version: 2`) |

---

## Detailed Changes Per File

---

### 1. `docs/source/conf.py`

- `release` → `'3.2'`
- `version` → `'3.2.0'`

---

### 2. `README.rst`

Replace the Read the Docs tutorial placeholder text with an actual WhiFuN project description. The README should briefly describe:
- What WhiFuN is (GUI-based MATLAB toolbox for WM and GM functional connectivity analysis)
- Link to the GitHub repository
- Link to the paper (Jain et al., 2025)
- Link to the Read the Docs documentation

---

### 3. `pyproject.toml`

- `name` → `whifun`
- `authors` → `[{name = "Pratik Jain", email = "pratik.pradip.jain@gmail.com"}]`
- `description` → `"WhiFuN - A toolbox for White Matter Functional Network analysis in fMRI"`

---

### 4. `lumache.py`

**Delete entirely.** This is a Read the Docs tutorial sample module with no relation to WhiFuN.

---

### 5. `docs/source/index.rst` — Rewrite

**Current issues:**
- Uses generic v1 description with `[cite: X]` reference tags scattered throughout
- toctree includes `usage` (Lumache leftover)
- Does not mention WhiFuN Version 3 or any new features

**Changes:**
- Replace overview paragraph with a proper WhiFuN Version 3 description:
  - GUI-based MATLAB toolbox
  - Automated preprocessing of WM and GM fMRI
  - Construction of WM/GM Functional Networks using K-means
  - WM-FC and GM-FC computation
  - Statistical and visualization tools
  - Based on SPM12
- Add a "What's new in Version 3" section covering:
  - Simplified scripting (`whifun_preproc`, `whifun_create_FN_kmeans`)
  - All functions are self-documented via MATLAB `help` command
  - New QC plots (seed-based correlation for DMN, auditory, and visual networks)
  - Support for data preprocessed by other pipelines (`whifun_using_other_preproc`)
  - Dartel-based MNI normalization
- Update toctree:
  - Remove `usage` (Lumache leftover)
  - Add `visualization` (new page)
  - Add `scripting` (new page for v3 scripting guide, replaces `usage`)
- Remove all `[cite: X]` tags from any text
- Keep contact information for Pratik Jain and Bharat Biswal (update if emails changed)

---

### 6. `docs/source/getting_started.rst` — Significant rewrite

**Current issues:**
- Does not specify MATLAB version requirement
- Toolbox list is from v1 (missing Bioinformatics, missing Optional Parallel Computing)
- WhiFuN download instructions point to an old or unspecified location
- Installation steps do not match v3 workflow

**Changes:**

#### MATLAB Version
- Add: "MATLAB R2022a or later is recommended"

#### MATLAB Toolboxes
- **Required:**
  - Image Processing Toolbox
  - Signal Processing Toolbox
  - Statistics and Machine Learning Toolbox
  - Bioinformatics Toolbox *(new — needed for `mafdr` FDR correction)*
- **Optional:**
  - Parallel Computing Toolbox *(new — improves performance)*
- Note: All can be downloaded via MATLAB's Add-Ons feature. Link: https://www.mathworks.com/help/matlab/matlab_env/get-add-ons.html

#### SPM12 Download
- Same download link: https://www.fil.ion.ucl.ac.uk/spm/software/spm12/
- Same setup steps — keep as-is

#### WhiFuN Download
- Download from: https://github.com/Brain-Connectivity-Lab/WhiFuN
- Use the green **Code** button → **Download zip** (~24 MB disk space)
- Unzip contents to a local folder

#### Adding WhiFuN to MATLAB Path
Two methods (both should be documented):
- **Option A (Recommended — persists across MATLAB sessions):** MATLAB Home tab → Environment → Set path → Add Folder → select the WhiFuN folder containing `whifun.m` → Save → Close
- **Option B (Command window — temporary):**
  ```matlab
  addpath('<path to WhiFuN folder>')
  ```

#### Launching WhiFuN
- Once paths are set, type `whifun` in the MATLAB command window and press Enter
- The main GUI window will open

---

### 7. `docs/source/setup.rst` — Major rewrite

**Current issues:**
- "Subject Data Folder" is now called "Participant Data Folder"
- No mention of the GUI's 6 subsections
- No Data Check module
- Non-BIDS format instructions are incomplete
- No Save/Load Parameters section

**Changes:**

#### GUI Overview
The WhiFuN GUI is divided into 6 subsections:
1. **Setup and Check Data** — folder paths and data validation
2. **Preprocessing** — all preprocessing parameters and execution
3. **Functional Networks (FNs) and Functional Connectivity (FC)** — create WM/GM FNs, compute atlas-FC
4. **Analyzing the FC and FNs** — statistics, compare FNs, check symmetry
5. **Visualization** — display FNs and FC matrices
6. **Save/Load Parameters** — save and reload session parameters

#### Output Folder
- Click the **Outputs folder** button or paste the path into the adjacent text field
- All QC plots and results will be saved here

#### Participant Data Folder
- Renamed from "Subject Data Folder" in v1
- Click the **Participant Data Folder** button or paste the path
- This folder must contain one subfolder per participant

#### BIDS Format
- If the dataset follows BIDS, check the **BIDS** checkbox
- WhiFuN will automatically locate anatomical and functional scans

#### Non-BIDS Format
- Uncheck the **BIDS** checkbox
- A dialog opens requiring the following fields:
  - **Intermediate Folder** — folder between participant folder and image folders (e.g., `session_1` or `session_1/MRI`)
  - **Functional Folder Name** — folder containing the functional image (e.g., `rest_1`)
  - **Anatomical Folder Name** — folder containing the T1 anatomical image (e.g., `anat_1`)
  - **Functional Image Name** — name of the `.nii` or `.nii.gz` functional file (use `*` as wildcard for participant-specific filenames, e.g., `sub-*`)
  - **Anatomical Image Name** — name of the `.nii` or `.nii.gz` anatomical file (same wildcard rule)
- Click **Submit** when done; WhiFuN will report if any files are missing

#### Selecting Participants
- Check **All folders are participants** to process every subfolder
- Or manually select a subset of participant folders
- WhiFuN displays the count of participants to be processed

#### Run Data Check
- Click **Run Data check** before preprocessing
- WhiFuN checks:
  - Missing anatomical or functional scans
  - Consistency of voxel size across images
  - Consistency of TR (temporal resolution) across images
  - Consistency of number of volumes (time points)
- Outputs: histogram and bar plot of parameters across all participants, and a `participant_list.csv` file
- A **"Data check completed successfully"** message confirms readiness

#### Save/Load Parameters
- All folder paths and parameters are automatically saved as a `.mat` file in the output folder
- Load them again using the **Load Parameters** button to avoid re-entering settings

---

### 8. `docs/source/preprocessing_and_qc.rst` — Major rewrite

**Current issues:**
- Very high-level descriptions with no parameter details
- Missing several preprocessing steps entirely (realignment, co-registration, skull stripping)
- QC section is vague (2–3 paragraphs instead of 9 detailed plot descriptions)
- Incorrect or absent default parameter values

**Changes:**

#### Preprocessing Parameters
All parameters are configurable in the Preprocessing section of the GUI before clicking **Run Preprocessing**:

| Parameter | Default | Description |
|---|---|---|
| Volumes to discard | 10 | Initial volumes discarded to allow magnetization to stabilize |
| Maximum FD threshold | 5 mm | Participant excluded if any volume exceeds this FD value |
| Mean FD threshold | 0.2 mm | Participant excluded if mean FD exceeds this value |
| FD outlier threshold | 0.2 mm | Participant excluded if >20% of volumes exceed this value |
| CSF regression | Mean CSF signal | Options: Mean CSF (default), PCA (first N components, default 5), or None |
| Friston's 24 motion parameters | Enabled (checkbox) | Regresses 6 params + squares + derivatives + squared derivatives |
| Smoothing method | WM/GM separately | Options: Separate (default), All voxels together, None |
| Smoothing FWHM | 4 mm | Full-width half-maximum of the Gaussian smoothing kernel |
| Temporal filtering | Enabled | Butterworth bandpass filter |
| Filter range | 0.01 – 0.15 Hz | Upper limit of 0.15 Hz captures WM-specific frequency content |
| Normalization voxel size | 3 mm | Output voxel size in MNI space |

The **Overwrite existing files** checkbox allows reprocessing from scratch; without it, WhiFuN skips completed steps automatically.

#### Preprocessing Pipeline (Step by Step)

**Step 1: Discard Initial Volumes**
- Removes the first N volumes (default 10) from the functional image to allow magnetization to reach steady state.

**Step 2: Realignment and Framewise Displacement**
- SPM `Realign (estimate and reslice)` aligns all functional volumes to the first volume.
- Translational (x, y, z in mm) and rotational (pitch, roll, yaw in radians) parameters saved to `rp_<filename>.txt`.
- Framewise Displacement (FD) computed as the sum of pairwise differences between consecutive translational and converted rotational parameters (brain radius assumed = 50 mm).
- Participants are **automatically excluded** if:
  - Maximum FD > 5 mm (default), or
  - Mean FD > 0.2 mm (default), or
  - More than 20% of volumes have FD > 0.2 mm (default)

**Step 3: Tissue Segmentation**
- SPM `Segment` classifies each voxel as WM, GM, or CSF.
- Skull stripped using SPM `ImCalc`.
- Deformation field generated for subsequent MNI normalization.

**Step 4: Co-registration**
- SPM `Co-registration (estimate)` aligns the anatomical T1 image to the mean functional image.
- Required so that WM/GM/CSF masks derived from the anatomical scan correctly map onto the functional image.

**Step 5: Nuisance Variable Regression**
- CSF voxels identified using tissue probability map threshold of 0.95.
- Regression options: mean CSF time series (default) or first N principal components (default 5) of all CSF voxels.
- Friston's 24 motion parameters optionally regressed (6 params + squares + derivatives + squared derivatives).

**Step 6: Temporal Filtering**
- Butterworth bandpass filter of 2nd order.
- Default range: 0.01 to 0.15 Hz.
- Upper cutoff of 0.15 Hz is used because WM BOLD signals can exhibit meaningful fluctuations up to ~0.10 Hz.

**Step 7: Smoothing**
- Default: WM and GM are smoothed **separately** to prevent signal mixing across tissue boundaries.
- Gaussian kernel with user-specified FWHM (default 4 mm), applied via SPM `smooth`.
- Voxels not identified as WM or GM (e.g., CSF in sulci) will appear as gaps; a large number of holes may indicate poor anatomical image quality.

**Step 8: Normalization to MNI Space**
- SPM `Normalize (write)` transforms images from native space to MNI space.
- Deformation field from segmentation is used.
- Default output voxel size: 3 mm isotropic.
- Expanded bounding box: `[-90 -126 -72; 90 90 108]` to include all brain tissue.

#### Post-Preprocessing Tools
Available under the **Tools** tab after preprocessing completes:
- **Determine Framewise Displacement Thresholds** — visualize participant rejection counts at different FD thresholds
- **Manually coregister participants** — for cases where automatic co-registration fails
- **Delete preprocessing from a particular step** — re-run preprocessing from any intermediate step for selected participants

#### Quality Control (QC) Plots
QC plots are saved to `<Output_folder>/Quality_Control` and should be reviewed for every participant.

**QC Plot 1: Initial Orientation**
- Raw anatomical and functional images displayed with their contours over the MNI template.
- **Action required:** If the image is far from MNI or oriented differently, manually reorient it and reset the origin to the anterior commissure before preprocessing.

**QC Plot 2: Motion Parameters and FD**
- Global mean signal (raw), 6 motion parameters, pairwise variance, and FD with threshold lines.
- **Action required:** Observe which participants were excluded and verify the thresholds are appropriate for your cohort.

**QC Plot 3: Tissue Segmentation**
- GM (red), WM (green), and CSF (blue) tissue probability maps overlaid on the same image; contours drawn over MNI template.
- **Action required:** Check for tissue misclassification. Discard participants with brain lesions or poor image quality.

**QC Plot 4: Co-registration**
- Anatomical image with functional image; contour of anatomical overlaid in red.
- **Action required:** Verify alignment. If misaligned, use the "manually coregister participants" tool.

**QC Plot 5: CSF Mask**
- CSF mask (threshold 0.95) overlaid on the functional image.
- **Action required:** Confirm alignment. If no voxels meet the threshold, recheck the anatomical image and consider discarding the participant.

**QC Plot 6: Effects of Regression and Temporal Filtering**
- Global signal before and after regression; global signal before and after filtering.
- **Action required:** Observation only. Confirm that motion-related trends and artifacts are removed.

**QC Plot 7: Effects of Separate WM/GM Smoothing**
- Shows gaps (holes) in the cortex where voxels were classified as neither WM nor GM.
- **Action required:** A small number of holes is normal (CSF in sulci). A large number may indicate poor anatomical quality — consider discarding the participant.

**QC Plot 8: Normalized Image**
- Normalized functional image with its contour over the MNI reference template.
- **Action required:** Verify spatial alignment with MNI. If alignment is poor, check co-registration and segmentation steps.

**QC Plot 9: Time Series Check**
- Global signal, 6 motion parameters, CSF signals, preprocessed global signal, and DVARS (pairwise variance), all plotted together with correlation matrices.
- **Action required:** Check that the preprocessed global signal is not significantly correlated with any noisy signal. Exclude participants with residual correlations.

---

### 9. `docs/source/functional_networks.rst` — Major rewrite

**Current issues:**
- High-level v1 descriptions with `[cite: X]` tags
- Missing algorithm details (K-means specifics, cross-validation, CC FNs)
- No Atlas-FC section
- No Analyzing FNs subsections (Compare FNs, Check Symmetry, Statistics)

**Changes:**

#### WM/GM Group Mask Construction

**WM Group Mask:**
- Only voxels where at least **WM group threshold %** (default 100%) of participants have WM probability > **individual WM probability threshold** (default 0.6) are included.
- The 100% default ensures no GM voxels contaminate the WM mask.
- Voxels missing data in >20% of participants are excluded.

**GM Group Mask:**
- All voxels where at least **GM group threshold %** (default 20%) of participants are classified as GM, and that are not already in the WM mask.
- Subcortical regions from the Harvard-Oxford Atlas are always included in the GM mask, even if SPM classified them as WM (due to high iron content).
- Voxels missing data in >20% of participants are excluded.

#### Voxel-Level Functional Connectivity Matrix
- A correlation matrix of size N×N is computed (N = number of voxels in the mask).
- To manage memory:
  - WM: every alternate voxel is used as a feature → matrix size N × (N/2)
  - GM: every 3rd voxel is used as a feature → matrix size N × (N/3)
  - WhiFuN automatically determines whether subsampling is needed based on available RAM.

#### K-means Clustering
- The FC matrix is the input; rows are voxels (data points), columns are features.
- Distance metric: Pearson correlation.
- K-means runs **10 repetitions** with different random initializations; the solution with the lowest distortion is kept.
- Output: every voxel in the mask is assigned to one of K clusters (Functional Networks).
- WM-FNs stored as `WM_clustering_K<K>.nii`; GM-FNs stored as `GM_clustering_K<K>.nii`.
- Average BOLD time series per FN per participant stored as `network_avgts_wm_K<K>.mat` / `network_avgts_gm_K<K>.mat`.

#### Finding the Optimal K (Cross-Validation)

WhiFuN uses a cross-validation approach to help select the best number of clusters (K):

1. The FC matrix is split into `ncv = 4` sub-folds by selecting a subset of features.
2. K-means is run independently on each sub-fold for every K in the specified range (default 2–22).
3. An **adjacency matrix** is created for each clustering result: `Adj(i,j) = 1` if voxels i and j are in the same cluster, else 0.
4. **Dice coefficients** are computed between adjacency matrices from different sub-folds; the average Dice coefficient is plotted against K.
5. A **distortion** value (average distance from voxels to their cluster center) is also plotted against K.
6. **Optimal K** has a locally high average Dice coefficient and a low distortion value (elbow point). The user selects K from these two plots.

#### Corpus Callosum (CC) Functional Networks
CC-FNs identify which sub-regions of the corpus callosum are most strongly connected to each WM-FN:

1. CC voxels (from the Mori atlas) are removed from the WM group mask.
2. For each CC voxel, partial correlation with each WM-FN time series is computed, controlling for all other K−1 WM-FNs.
3. Fisher-z transformation is applied to the partial correlation values.
4. A one-sample t-test (across participants) yields a t-statistic per CC voxel per WM-FN.
5. Each CC voxel is assigned to the WM-FN with the **maximum t-statistic** (winner-take-all).
6. Output: `cc_networks_from_WM_K<K>.nii` and `cc_avg_ts_<K>.mat`.

#### Atlas-Based Functional Connectivity
- Several JHU atlases (Mori et al., 2008; Oishi et al., 2009) are included in WhiFuN.
- Users can also load any custom atlas in NIfTI format (`.nii` or `.nii.gz`).
- WhiFuN extracts the average BOLD time series for each atlas ROI for every participant.
- Time series are saved as `<atlas_name>_reg_ts.mat`.
- **Frequency band filtering:** time series filtered to a user-specified frequency band can also be saved as `<atlas_name>_<frequency_band>_avgts.mat`.

#### Creating the FC Matrix
- Pearson correlation is computed between all pairs of average FN/ROI time series.
- Produces an n×n matrix (n = number of FNs or atlas ROIs) per participant.
- Can be used as input to the Brain Connectivity Toolbox for graph-theoretic analysis.

#### Compare FNs
- Located in the **Analyzing the FC and FNs** section of the GUI.
- Computes Dice coefficients between two user-specified sets of FNs.
- Output: an n1×n2 matrix of Dice coefficients (n1 = FNs in set 1, n2 = FNs in set 2).
- **Use case:** label WM-FNs by comparing them against the JHU-DTI-81 atlas; label GM-FNs by comparing against Yeo 7 networks.

#### Check FN Symmetry
- Quantifies interhemispheric symmetry of FNs.
- **All FNs at once:** uses the Peer et al. (2017) method — adjacency matrices created separately for left and right hemispheres; Dice coefficient between the two is the symmetricity score.
- **Per-FN:** Dice coefficients computed between each left-hemisphere FN and each right-hemisphere FN; displayed as a matrix plot.
- High Dice coefficient = high symmetry.

#### Statistics
- Applies a General Linear Model (GLM) using MATLAB's `regstats` to FC values.
- **Input:** a CSV file with participant identifier in column 1 and covariates (group, age, sex, behavioral scores, motion parameters, etc.) in subsequent columns.
- **Multiple comparison correction:** False Discovery Rate (FDR) using the Benjamini-Hochberg method via MATLAB's `mafdr`, or Bonferroni correction.
- **Output:** t-value matrix for every FC connection; statistically significant connections are highlighted.
- Default significance level (alpha): 0.05 (user-configurable).

---

### 10. `docs/source/usage.rst` — Complete replace

**Current content:** Lumache Python library installation and `get_random_ingredients()` example — entirely wrong.

**Replace with a WhiFuN scripting guide for Version 3:**

#### Overview
In addition to the GUI, WhiFuN Version 3 supports scripting for automated batch processing.

#### Preprocessing with a Script
All preprocessing steps can be run with a single function call:
```matlab
whifun_preproc(params)
```
Use `help whifun_preproc` for full documentation of input arguments.

#### Creating WM/GM Functional Networks with a Script
```matlab
whifun_create_FN_kmeans(params)
```
Use `help whifun_create_FN_kmeans` for full documentation.

#### Using Data Preprocessed by Other Tools
If data has been preprocessed by another pipeline (e.g., fMRIPrep, FSL), use:
```matlab
whifun_using_other_preproc(params)
```
This function skips WhiFuN preprocessing and directly proceeds to FN construction.

#### Self-Documentation
All WhiFuN functions are self-documented. To get detailed information on any function's inputs, outputs, and dependencies:
```matlab
help <function_name>
% Example:
help whifun_get_FN_kmeans
```

#### Example Scripts
The following example scripts are included in the WhiFuN repository root:
- `whifun_preprocess_script.m` — basic preprocessing script
- `whifun_preprocess_script_all.m` — preprocessing for all participants
- `basic_script_whifun_post_preproc_fmriprep.m` — post-processing after fMRIPrep
- `basic_script_whifun_preproc_fsl.m` — preprocessing using FSL output
- `Create_WM_FN_script.m` — create WM functional networks

---

### 11. `docs/source/api.rst` — Fix/replace

**Current content:** References a `Krishna` module that does not exist → causes a Sphinx build warning/error.

**Replace with a page explaining the MATLAB-based self-documentation approach:**

Since WhiFuN is a MATLAB toolbox, there is no Python API. All functions are self-documented via MATLAB's `help` system.

Key functions to document (with brief descriptions to be expanded):
- `whifun` — launches the main GUI
- `whifun_preproc` — runs the full preprocessing pipeline
- `whifun_create_FN_kmeans` — constructs WM/GM Functional Networks using K-means
- `whifun_using_other_preproc` — use externally preprocessed data for FN construction
- `whifun_addpath_and_create_preproc_folders` — sets up folder structure
- `whifun_dartel` — Dartel-based preprocessing
- `whifun_dartel_normalize_smooth` — Dartel-based normalization and smoothing

---

### 12. `docs/source/visualization.rst` — New file

**Content:**

#### Display FN
- Located in the **Visualization** section of the GUI.
- Displays WM, GM, or CC Functional Networks.
- Uses SPM or BrainNet Viewer (included in the WhiFuN repository).
- Automatically generates 6 views per FN: Anterior, Posterior, Dorsal, Ventral, Left, Right.
- Images are saved as `.png` files in the output folder for direct use in manuscripts.

#### Display FC
- Displays the Functional Connectivity matrix.
- Options via dropdown menu:
  - **Mean FC** across all participants
  - **Standard deviation FC** across all participants
  - **Per-participant FC** (individual subject)
  - **Per-group FC** (mean/std by group, assigned manually or via CSV)
- Available FC types: WM-WM, WM-GM, WM-CC, Atlas-FC
- Color bar represents Pearson correlation coefficients.
- FN brain maps are shown adjacent to the FC matrix for interpretability.

---

### 13. `.readthedocs.yaml` — Fix schema error

**Current issue:**
```yaml
version: "2"   # ← string, should be integer → causes 2 schema validation errors
```

**Fix:**
```yaml
version: 2
```

---

## Build Validation

After all changes, run a local Sphinx build to verify:
```bash
cd WhifuN---A-toolbox-for-White-Matter-Analysis-in-fMRI
python3 -m venv .venv
.venv/bin/python -m pip install -r docs/requirements.txt
.venv/bin/sphinx-build -n -W -b html docs/source docs/build
```

Target: **0 warnings, 0 errors**.

Known issues to resolve during implementation:
1. `api.rst` currently causes a build warning due to missing `Krishna` module — fixed by replacing with MATLAB `help` reference page.
2. `usage.rst` currently not included in any toctree — fixed by replacing content and adding to `index.rst` toctree as `scripting`.
3. `docs/requirements.txt` pin versions are currently `sphinx==7.1.2` and `sphinx-rtd-theme==1.3.0rc1` — these work but the RC version of the theme could be bumped to a release version if desired.
