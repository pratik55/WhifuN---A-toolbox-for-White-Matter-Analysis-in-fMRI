Preprocessing & Quality Control
===============================

WhiFuN preprocessing combines in-house MATLAB code with SPM12 modules. It
supports fully automated execution with parameter controls in the GUI.

Preprocessing Parameters
------------------------

Configure all parameters before clicking **Run Preprocessing**.

.. list-table::
   :header-rows: 1

   * - Parameter
     - Default
     - Description
   * - Volumes to discard
     - 10
     - Discard initial volumes for signal stabilization
   * - Maximum FD threshold
     - 5 mm
     - Exclude participant if max FD exceeds threshold
   * - Mean FD threshold
     - 0.2 mm
     - Exclude participant if mean FD exceeds threshold
   * - FD outlier threshold
     - 0.2 mm
     - Used with outlier percentage criterion
   * - FD outlier percentage
     - 20%
     - Exclude participant if more than 20% volumes exceed FD threshold
   * - CSF regression
     - Mean CSF
     - Mean CSF, PCA of CSF, or no CSF regression
   * - CSF PCA components
     - User-defined
     - Number of PCA components (when PCA mode selected)
   * - Friston 24 motion regression
     - Enabled (optional)
     - Regress 6 motion params, squares, derivatives, and squared derivatives
   * - Temporal filtering
     - Enabled
     - Butterworth bandpass filtering
   * - Filter range
     - 0.01 to 0.15 Hz
     - Frequency range for temporal filtering
   * - Smoothing mode
     - WM/GM separately
     - Separate, all tissues together, or none
   * - Smoothing FWHM
     - User-defined
     - Gaussian kernel FWHM
   * - Normalization voxel size
     - 3 mm
     - MNI-space output voxel size
   * - Overwrite existing files
     - Off by default
     - Re-run from scratch instead of skipping completed steps

Preprocessing Pipeline (Step by Step)
-------------------------------------

Step 1: Unzip and Discard Initial Volumes
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

WhiFuN unzips ``.nii.gz`` files if needed and discards the first N volumes
(default 10). Setting the value to 0 keeps all volumes.

Step 2: Realignment and Framewise Displacement
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

SPM ``Realign (estimate and reslice)`` aligns all functional volumes to the
first volume. Motion parameters are then used to compute framewise displacement
(FD) following Power et al. (2012).

Participants are excluded if any of these conditions is met:

- Maximum FD > 5 mm (default)
- Mean FD > 0.2 mm (default)
- More than 20% of volumes have FD > 0.2 mm (default)

Step 3: Segmentation, Co-registration, and Mask Extraction
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

WhiFuN performs anatomical segmentation (GM/WM/CSF), skull stripping,
co-registration between functional and anatomical images, and mask extraction,
including CSF mask generation (threshold 0.95).

Step 4: Nuisance Regression
~~~~~~~~~~~~~~~~~~~~~~~~~~~

WhiFuN regresses nuisance signals from voxel time series:

- Mean CSF signal, or
- PCA components from CSF signal space, or
- no CSF regression.

Friston’s 24 motion parameters can also be regressed.

Step 5: Temporal Filtering
~~~~~~~~~~~~~~~~~~~~~~~~~~

A second-order Butterworth bandpass filter is applied (default 0.01 to 0.15 Hz).
You can disable filtering in the GUI.

Step 6: Smoothing
~~~~~~~~~~~~~~~~~

For WM analysis, separate WM/GM smoothing is recommended to avoid tissue signal
mixing. WhiFuN also supports smoothing all tissues together or skipping
smoothing.

Step 7: Normalization to MNI Space
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Normalization uses segmentation deformation fields. Default output is 3 mm
isotropic voxels, with expanded bounding box:

``[-90 -126 -72; 90 90 108]``

This helps ensure full brain coverage in MNI space.

Step 8: Resume vs Overwrite Behavior
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

If preprocessing is interrupted, WhiFuN can resume by skipping completed steps.
To force a full restart for all subjects, enable **Overwrite existing files**.

Post-Preprocessing Tools
------------------------

WhiFuN includes dedicated tools under preprocessing utilities:

- **Determine Framewise Displacement thresholds**
  to inspect rejection counts and tune FD cutoffs.
- **Manually Coregister Subjects**
  to fix failed automatic coregistration in SPM.
- **Delete Preprocessing Files from a Particular Step**
  to re-run selected subjects from an intermediate stage.

Quality Control (QC) Plots
--------------------------

QC plots are saved under ``<Output_folder_path>/Quality_Control`` and should be
reviewed for all participants.

1. **Initial Check**

   - Raw anatomical and functional images with contours over MNI template.
   - Action: reorient/reset origin if grossly misaligned.

2. **Head Motion**

   - Global signal, motion parameters, pairwise variance, and FD.
   - Action: verify motion exclusions and thresholds.

3. **Segmentation**

   - GM (red), WM (green), CSF (blue) overlays and template contour checks.
   - Action: inspect tissue classification quality.

4. **Coregistration**

   - Anatomical-to-functional alignment plot.
   - Action: use manual coregistration tool if misaligned.

5. **CSF Mask QC**

   - CSF mask overlaid on functional image.
   - Action: confirm proper CSF mask placement and sufficient voxels.

6. **Regression/Filtering Effects**

   - Before/after global signal traces for regression and filtering.
   - Action: verify nuisance trend/artifact reduction.

7. **Smoothing Effects**

   - Visual check of separate WM/GM smoothing output.
   - Action: too many cortical holes may indicate poor data quality.

8. **Normalization QC**

   - Normalized functional image contour over MNI template.
   - Action: verify final spatial alignment.

9. **Time-Series Check**

   - Correlations among global signals, motion, CSF, and DVARS-like metrics.
   - Action: consider excluding participants with strong residual noise
     associations.

10. **Error Handling**

   - If a subject fails at any step, WhiFuN writes
     ``<SubjectID>_error_info.txt`` under QC error folders.
