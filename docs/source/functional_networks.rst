Construct and Analyze Functional Networks
=========================================

This module is applied after preprocessing and includes WM/GM functional
network construction, atlas-based FC workflows, and downstream FN/FC analysis.

White Matter and Gray Matter Functional Networks
------------------------------------------------

WhiFuN first creates group masks and then applies K-means clustering on
voxel-level connectivity profiles to derive WM and GM functional networks (FNs).

WM/GM Group Mask Construction
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

WM Group Mask
^^^^^^^^^^^^^

A WM voxel is included when at least the **WM group threshold** of participants
(default 100%) have WM probability above the **individual WM probability
threshold** (default 0.6).

Notes:

- High WM group threshold reduces GM contamination risk in WM analysis.
- Voxels missing data in more than 20% of participants are excluded.

GM Group Mask
^^^^^^^^^^^^^

A GM voxel is included when at least the **GM group threshold** of participants
(default 20%) are classified as GM, and the voxel is not already in the WM
mask.

Additional handling:

- Subcortical regions from atlas definitions can be retained in GM workflows.
- Voxels missing data in more than 20% of participants are excluded.

Voxel-Level Functional Connectivity Matrix
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

After masks are created, WhiFuN computes voxel-level FC from selected
participants and uses this matrix as input for clustering.

To manage memory, WhiFuN may use subsampled feature sets (Peer et al., 2017):

- WM: feature subsampling (for example, approximately every alternate voxel)
- GM: stronger subsampling for larger masks

WhiFuN automatically decides whether full or subsampled FC should be used based
on available RAM.

K-means Clustering
~~~~~~~~~~~~~~~~~~

WhiFuN performs K-means over a user-defined K range (default: 2 to 22).
If lower and upper K are identical, cross-validation can be skipped and
clustering runs directly at that K.

Algorithm notes:

- Input: voxel-wise FC feature matrix
- Distance metric: correlation-based similarity
- Multiple random initializations are evaluated
- Solution with lowest distortion is retained

Outputs include:

- ``WM_clustering_K<K>.nii`` and ``GM_clustering_K<K>.nii``
- ``network_avgts_wm_K<K>.mat`` and ``network_avgts_gm_K<K>.mat``

Finding the Optimal K (Cross-Validation)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

WhiFuN computes cross-validation stability and distortion across K values.
The user can set the number of CV folds (default: 4).

Typical workflow:

1. Split features into CV folds.
2. Run K-means independently per fold and K.
3. Convert cluster solutions to adjacency matrices.
4. Compute Dice overlap between folds.
5. Plot average Dice coefficient and distortion versus K.

An optimal K generally has:

- locally high average Dice (stable clustering), and
- low distortion (compact clusters).

Corpus Callosum (CC) Functional Networks
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

If **Corpus Callosum networks** is enabled in the WM-FN panel, WhiFuN creates
CC subnetworks maximally associated with WM-FNs.

Summary of the CC procedure:

1. Identify CC voxels from atlas mask (Mori atlas).
2. For each CC voxel, evaluate association with WM-FN time series
   (partial-correlation-based winner-take-all framework).
3. Compute participant-level statistics and assign each voxel to the strongest
   WM-FN association.

Outputs are saved under ``<output_folder>/Analysis/Corpus_Callosum_FN`` and
include:

- ``CC_network_from_WM_K<K>.nii``
- ``network_avgts_cc_K<K>.mat``
- CC voxelwise signals and CC atlas mask files

Output Files from WM/GM FN Construction
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

WhiFuN stores:

- Group masks in ``<output>/Analysis/Group_Masks``
- WM FNs in ``<output>/Analysis/WM_FN``
- GM FNs in ``<output>/Analysis/GM_FN``
- Network-average time series as ``network_avgts_*.mat``
- Dice/distortion grid-search plots as ``.png``
- BrainNet image sets for generated FNs

Atlas-Based Functional Connectivity
-----------------------------------

Use Atlas-FC when FC should be computed from atlas ROIs instead of voxel-wise
FN labels.

Supported atlas inputs:

- Built-in JHU atlases
- Custom atlas files (``.nii`` or ``.nii.gz``)

Workflow:

1. Select atlas.
2. Optionally save QC images for regions with missing/NaN voxel data.
3. Run Atlas FC to extract per-ROI average time series for each participant.

Outputs:

- ``<atlas_name>_reg_ts.mat`` in ``<output>/Analysis/Atlas_FC``
- Resliced atlas (if atlas dimensions differ from functional image dimensions)

Extract Time Series in Frequency Bands
--------------------------------------

WhiFuN can extract atlas/FN/CC average time series in user-defined frequency
bands.

Workflow:

1. Select atlas (or use FN/CC outputs).
2. Specify number of bands.
3. Define each band range and band name.
4. Run average time-series extraction.

Outputs:

- ``<atlas_or_network_name>_<band_name>_reg_ts.mat``
- Filter response plots in the corresponding ``Filters`` folder

Creating FC Matrices from Average Time Series
---------------------------------------------

WhiFuN computes Pearson correlation across all selected FN/ROI time series,
producing participant-level FC matrices.

These matrices can be used directly for:

- group comparisons,
- behavior/covariate modeling, and
- graph-theoretic analyses (for example, Brain Connectivity Toolbox workflows).

Analyze Functional Networks and Connectivity
--------------------------------------------

Compare FNs
~~~~~~~~~~~

Compares two FN sets using Dice overlap.

- Input: two NIfTI label maps
- Output: ``n1 x n2`` Dice matrix

Typical use case: compare WhiFuN WM-FNs to JHU-DTI-81 for network labeling.

Check FN Symmetry
~~~~~~~~~~~~~~~~~

Quantifies hemispheric symmetry of networks.

WhiFuN provides:

- left-vs-right pairwise Dice matrix across networks, and
- global symmetry score for the full FN map (Peer et al., 2017 style metric).

Higher Dice indicates stronger interhemispheric symmetry.

Statistics
~~~~~~~~~~

WhiFuN runs FC statistics using MATLAB ``regstats`` with covariates from a CSV.

CSV format:

- Column 1: subject ID (must match folder names)
- Remaining columns: numeric covariates (group, age, sex coding, behavior, etc.)

Features include:

- FC-type selection (WM/GM/CC/atlas depending on available timeseries)
- Variable selection from CSV
- Significance threshold (alpha; default 0.05)
- Plot all connections or only significant ones
- Multiple-comparison correction:

  - FDR (Benjamini-Hochberg via MATLAB ``mafdr``)
  - Bonferroni

- Data tips and plot export
- Frequency-band-specific statistics (when band-limited timeseries are available)
