Setup
=====

The Setup section defines where WhiFuN reads participant MRI data from and
where all outputs are written.

GUI Overview
------------

The WhiFuN GUI is divided into six subsections:

1. **Setup and Check Data**
2. **Preprocessing**
3. **Functional Networks (FNs) and Functional Connectivity (FC)**
4. **Analyzing the FC and FNs**
5. **Visualization**
6. **Save/Load Parameters**

Output Folder
-------------

The output folder is where WhiFuN saves quality control plots and analysis results.

- Click **Outputs folder** and select an empty folder, or
- Paste the folder path in the adjacent text field.

This path is referred to as ``<Output_folder_path>`` in the documentation.

Participant Data Folder
-----------------------

The participant data folder contains one subfolder per participant, and each
participant must have both anatomical and functional MRI data.

- Click **Participant Data Folder** (called **Subject Data Folder** in the current
  GUI/manual) and select the dataset root, or
- Paste the path in the adjacent text field.

WhiFuN reports how many folders it detects in this directory.

Selecting Participants
----------------------

- If all subfolders are participants, check **All folders are participants**
  (manual label may appear as **All folders are Subjects**).
- Otherwise, use participant selection to choose only specific folders.

WhiFuN then shows the total number of selected participants.

Data Structure
--------------

BIDS Format
~~~~~~~~~~~

If the dataset follows BIDS, check the **BIDS** checkbox next to the data folder.
WhiFuN uses the expected BIDS structure to locate files.

Non-BIDS Format
~~~~~~~~~~~~~~~

If data is not BIDS, uncheck **BIDS**. WhiFuN opens a details window where you
must provide:

- **Intermediate Folder(s):** folder(s) between subject folder and anat/func folders
  (for example ``session_1`` or ``MRI/3T/session_1``)
- **Functional Folder Name:** folder containing the functional image
- **Anatomical Folder Name:** folder containing the anatomical image
- **Functional Image Name:** functional image base name (omit ``.nii``/``.nii.gz``;
  wildcards like ``*`` are supported)
- **Anatomical Image Name:** anatomical image base name (omit extension;
  wildcards supported)

Notes:

- WhiFuN auto-detects ``.nii`` vs ``.nii.gz``.
- If ``.nii.gz`` is found, WhiFuN unzips and processes it.
- Review the resolved anatomical/functional file paths before submitting.

Run Data Check
--------------

After setup, click **Run Data check**.

WhiFuN validates:

- Missing anatomical/functional files
- Voxel sizes (anatomical and functional)
- Number of functional volumes
- TR consistency (from NIfTI header)

Outputs are saved under ``<Output_folder_path>/Quality_Control``:

- ``Q1a_scanning_parameters`` (bar plots)
- ``Q1a_scanning_parameters_histogram`` (histograms)

The data check report indicates missing files and TR issues. A successful run
reports that data check completed successfully.

Subject Info
------------

After data check, **Subject Info** shows extracted metadata (e.g., voxel size,
TR, volume count, error flags, exclusion flags). If a TR is missing from header,
you can manually enter it and save changes.

Save/Load Parameters
--------------------

WhiFuN saves setup and preprocessing parameters to ``parameters.mat`` in the
output folder after data check.

- Use **Load Parameters** to restore a previous session configuration.
- Use **Save Parameters** to save/overwrite parameter files as needed.
