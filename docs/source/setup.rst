Setup
=====

The Folder paths for where the MRI data is stored and where the outputs of WhiFuN will be stored is provided in the Setup. [cite: 27]

Output Folder
-------------
Output Folder is an empty folder where the quality control plots and results of WhiFuN will be stored. [cite: 28] Click the Outputs folder button or alternatively paste the path of the Outputs folder in the text box besides the Output folder button. [cite: 29]

Subject Data Folder
-------------------
Subject Data Folder is where the raw MRI data is present. [cite: 31] This folder should contain subfolders that correspond to data of Subjects. [cite: 32] Every subfolder should contain anatomical MRI scan and the fMRI scan. [cite: 33] Once the Subject Data Folder is selected, WhiFuN will tell the number of folders identified in the Subject Data Folder. [cite: 35]

Data Structure
--------------
Most fMRI datasets use the Brain Imaging Data Structure (BIDS) (https://bids.neuroimaging.io/). [cite: 40] If the dataset that is to be preprocessed and analyzed is in BIDS format, then the checkbox besides the Subject Data Folder should be checked. [cite: 41] If, however, the dataset is not in BIDS format then uncheck the BIDS checkbox. [cite: 42] 

WhiFuN can process deviation from BIDS format if every subject folder has an anatomical folder and a functional folder that are in the same folder. [cite: 45, 46]
