Getting Started
===============

WhiFuN is a MATLAB-based toolbox for white matter and gray matter fMRI analysis.
For Version 3, ``MATLAB R2022a`` or later is recommended.

Prerequisites
-------------

Required MATLAB toolboxes
~~~~~~~~~~~~~~~~~~~~~~~~~

- Image Processing Toolbox
- Signal Processing Toolbox
- Statistics and Machine Learning Toolbox
- Bioinformatics Toolbox (required for ``mafdr`` FDR correction)

Optional MATLAB toolbox
~~~~~~~~~~~~~~~~~~~~~~~

- Parallel Computing Toolbox (recommended for faster processing)

All toolboxes can be installed through MATLAB Add-Ons:
https://www.mathworks.com/help/matlab/matlab_env/get-add-ons.html

Install SPM12
-------------

1. Download SPM12 from:
   https://www.fil.ion.ucl.ac.uk/spm/software/spm12/
2. Add SPM12 to your MATLAB path using one of the methods below.

**Option A (recommended, persistent):**

- MATLAB ``Home`` tab -> ``Environment`` -> ``Set Path``
- Click ``Add Folder``
- Select the SPM folder containing ``spm.m``
- Click ``Save`` -> ``Close``

**Option B (temporary, command window):**

.. code-block:: matlab

   addpath('<path to spm12 folder>')

Download WhiFuN
---------------

1. Go to: https://github.com/Brain-Connectivity-Lab/WhiFuN
2. Click the green ``Code`` button -> ``Download ZIP``
3. Extract the ZIP to a local folder (about 24 MB disk space)

Add WhiFuN to MATLAB Path
-------------------------

After extraction, add the WhiFuN folder (the one containing ``whifun.m``)
to the MATLAB path.

**Option A (recommended, persistent):**

- MATLAB ``Home`` tab -> ``Environment`` -> ``Set Path``
- Click ``Add Folder``
- Select the WhiFuN folder containing ``whifun.m``
- Click ``Save`` -> ``Close``

**Option B (temporary, command window):**

.. code-block:: matlab

   addpath('<path to WhiFuN folder>')

Launch WhiFuN
-------------

Once SPM12 and WhiFuN paths are added, run:

.. code-block:: matlab

   whifun

The main WhiFuN GUI will open.

.. image:: /docs/WhiFuN_GUI.png
