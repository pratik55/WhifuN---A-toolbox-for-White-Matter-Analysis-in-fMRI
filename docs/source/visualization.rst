Visualization
=============

Display FN
----------

The **Display FN** module visualizes WM, GM, or CC functional networks from
WhiFuN-generated clustering maps.

Workflow:

1. Click **Display FN**.
2. Select the FN NIfTI file (for example ``WM_clustering_K<k>.nii`` or
   ``GM_clustering_K<k>.nii``).
3. Choose visualization backend:

   - SPM display, or
   - BrainNet Viewer (included with WhiFuN).

WhiFuN can also generate manuscript-ready FN visuals and stores BrainNet image
outputs in analysis subfolders.

Display FC
----------

The **Display FC** module visualizes FC matrices derived from WhiFuN time-series
outputs.

Supported views include:

- Mean FC across participants
- Standard deviation FC across participants
- Per-participant FC
- Group-wise FC summaries (mean/std) after group assignment

Supported FC types (based on available timeseries) include:

- WM-WM FC
- WM-GM FC
- WM-CC FC
- Atlas-based FC

Additional display features:

- Group splitting via CSV (two-group mode) or manual subject selection
- Data tips for inspecting specific matrix entries
- Save plots as ``.png``
- Frequency-band selection (when band-specific timeseries are available)

FC matrices are shown with color bars representing Pearson correlation values,
and WhiFuN displays associated network maps for interpretation.
