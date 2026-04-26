Construct and Analyze Functional Networks
=========================================

White matter and Gray Matter Functional Networks
------------------------------------------------
This module is applied to the fully preprocessed rsfMRI images. [cite: 266] Group masks are created first to identify the WM or GM voxels across the subjects. [cite: 267] The K-means algorithm clusters the voxels in WM and GM to create the WM and GM-FNs based on voxel based FC. [cite: 268]

WhiFuN requires the user to specify a K-value range (default 2 to 22). [cite: 275] A cross-validation approach is applied to determine the optimal number of clusters (K). [cite: 278]

Atlas based Functional Connectivity
-----------------------------------
If users have a predefined atlas and they wish to compute the FC matrix using the atlas, WhiFuN’s Atlas-FC module can be used. [cite: 298] WhiFuN will compute the average time series corresponding to every region in the atlas for every subject which can be used to compute the FC matrix using Pearson Correlation. [cite: 306]

Extract Time series in frequency band
-------------------------------------
Users can extract the average time series in a particular frequency band, to study the frequency specific characteristics. [cite: 310] 

Analyze Functional Networks
---------------------------
This module analyses the FNs and FC created during the Construct FNs and FC module by finding significant connections using statistical tests in FCs, checking how symmetric the FNs are across the two hemispheres or comparing the FNs computed by WhiFuN with any other predefined atlas to understand the network labels. [cite: 317]
