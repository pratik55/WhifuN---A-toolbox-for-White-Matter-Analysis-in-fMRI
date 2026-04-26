Preprocessing & Quality Control
===============================

Preprocessing
-------------
**Nuisance Regression**
To reduce noise, WhiFuN regresses out unwanted signals from every voxel in the brain. [cite: 148] Users can choose between regressing the mean CSF signal for a faster computation or using principal component analysis (PCA) to regress the dominant CSF signal components. [cite: 149] Friston’s 24 motion parameters can also be regressed out. [cite: 151, 152]

**Temporal Filtering**
After Regression, the voxel time series from every voxel is filtered using a Butterworth bandpass filter of second order in the range specified by the user (default 0.01 to 0.15 Hz). [cite: 157]

**Smoothing**
Smoothing is performed using a Gaussian kernel with Full with half maximum (FWHM) that can be specified by the user. [cite: 164] To completely avoid that WM and GM signals mix, WM and GM signals are separately smoothed. [cite: 161, 162]

**Normalization**
Normalization is performed after smoothing, where images are transformed from the subject’s native space to the standard MNI space with a voxel size specified by the user (default: 3 mm). [cite: 166, 167]

Quality Control (QC)
--------------------
Once the preprocessing is complete, the user is recommended to go through the quality control plots generated after most preprocessing steps. [cite: 181] These quality control plots are saved in ``<Output_folder_path>/Quality_Control``. [cite: 182]

WhiFuN automatically excludes subjects with excessive head motion, requiring no additional action from the user. [cite: 192] The user must check the initial position and orientation of the images with that of the MNI space. [cite: 183]
