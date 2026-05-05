Welcome to WhiFuN's Documentation!
==================================

WhiFuN (White Matter Functional Networks) is a GUI-based MATLAB toolbox for
automated preprocessing of fMRI images, robust construction of White Matter (WM) and Gray Matter (GM)
Functional Networks (FNs), computation of WM and GM Functional Connectivity (FC), and downstream FC
analysis.

WhiFuN GUI is designed so you can
run the workflow from setup to analysis without writing code, while also
supporting script-based workflows for automation.

What's New in Version 3
-----------------------

- Simplified scripting:

  - ``whifun_preproc`` for end-to-end preprocessing
  - ``whifun_create_FN_kmeans`` for WM/GM FN creation

- Self-documentation for all functions via MATLAB ``help``.
- Expanded QC plots, including seed-based correlation QC for default mode,
  auditory, and visual networks.
- Support for data preprocessed by other tools via
  ``whifun_using_other_preproc``.
- Dartel-based MNI normalization support.

.. toctree::
   :maxdepth: 2
   :caption: Contents:

   getting_started
   setup
   preprocessing_and_qc
   functional_networks
   visualization
   scripting
   api

Contact Information
-------------------

* **Pratik Jain**: jainpratik412@gmail.com; pj44@njit.edu
