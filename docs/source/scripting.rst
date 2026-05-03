Scripting
=========

Overview
--------

In addition to the GUI, WhiFuN Version 3 supports script-based workflows for
batch and reproducible processing.

Preprocessing with a Script
---------------------------

Run the full preprocessing workflow with:

.. code-block:: matlab

   whifun_preproc(params)

Use MATLAB help for argument details:

.. code-block:: matlab

   help whifun_preproc

Creating WM/GM Functional Networks with a Script
------------------------------------------------

Create WM/GM functional networks via:

.. code-block:: matlab

   whifun_create_FN_kmeans(params)

Documentation:

.. code-block:: matlab

   help whifun_create_FN_kmeans

Using Data Preprocessed by Other Tools
--------------------------------------

To use data preprocessed in external pipelines (for example fMRIPrep or FSL),
run:

.. code-block:: matlab

   whifun_using_other_preproc(params)

This bypasses WhiFuN preprocessing and proceeds to FN/FC workflows.

Self-Documentation
------------------

All WhiFuN functions are self-documented through MATLAB ``help``.

.. code-block:: matlab

   help <function_name>

Example:

.. code-block:: matlab

   help whifun_get_FN_kmeans

Example Scripts
---------------

The WhiFuN repository includes example scripts such as:

- ``whifun_preprocess_script.m``
- ``whifun_preprocess_script_all.m``
- ``basic_script_whifun_post_preproc_fmriprep.m``
- ``basic_script_whifun_preproc_fsl.m``
- ``Create_WM_FN_script.m``
