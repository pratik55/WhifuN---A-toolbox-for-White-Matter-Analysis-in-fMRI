API
===

WhiFuN is a MATLAB toolbox. There is no Python API in this repository.

Instead, WhiFuN functions are documented through MATLAB's built-in help system.
For details on arguments, outputs, and dependencies, use:

.. code-block:: matlab

   help <function_name>

Core Functions
--------------

- ``whifun``

  - Launches the main WhiFuN GUI.

- ``whifun_preproc``

  - Runs the full preprocessing pipeline.

- ``whifun_create_FN_kmeans``

  - Creates WM/GM functional networks using K-means.

- ``whifun_using_other_preproc``

  - Uses externally preprocessed data for FN/FC workflows.

- ``whifun_addpath_and_create_preproc_folders``

  - Sets paths and creates preprocessing folder structure.

- ``whifun_dartel``

  - Runs Dartel-based preprocessing components.

- ``whifun_dartel_normalize_smooth``

  - Applies Dartel-based normalization and smoothing steps.

Example
-------

.. code-block:: matlab

   help whifun_get_FN_kmeans
