# Cluster_group - quick script for automated clustering, visualization, and analysis of cross correlation coefficients between cryo-EM maps 
# TL;DR
This tool is just a shorthand for comparing and clustering different maps in your cryo-EM workflow.

## Use Cases:
1. You just ran a 3D classification/heterogeneous refinement job and want to quickly compare classes in your final volume series.
2. You have already grouped your particles into classes and want to compare them to each other (this might be worth using if you have a lot of classes, or if you are looking for intermediate states in a time-resolved cryo-EM project).
# Problem
There are many times in the cryo-EM data processing workflow where you may want to split a particle set between a series of classes in 3D (Heterogeneous refinement, 3D Variability Analysis, 3D Classification, etc.) in order to regroup similar particles. Typically, that process looks something like this:
![](https://i.ibb.co/SKpgP4N/Untitled-1.png)

On the face, this makes a lot of sense. Stratify a bunch to find all the things that are structurally different between particles in your set, then regroup based on visual similarity of classes. Rinse and repeat until you're satisfied with the similarity between your classes.

But what if we wanted a quantitative way to compare maps to each other and an automated means of clustering our classes by similarity? That's what this tool will give you.

# Required inputs:
The following must be placed in a single directory which you will provide to the script.
1. A series of .mrc files (your maps).
2. The script itself.
3. A .csv file containing the custom name you want to assign to each file. **The header line must read *'original_filename,customname_1'***
	A. An example csv is below:
```
original_filename,custom_name
filename_1,customname_1
filename_2,customname_2
filename_3,customname_3
filename_4,customname_4
```
*The tool will read the first .csv file it finds in the directory you supply, so make sure that your input csv is the only one in the specified directory.*
# Script Outputs
1. similarity_matrix_heatmap.png - correlation scores (0<x<1) for all pairs of maps.
2. similarity_matrix.csv - same data as the png
3. dendrogram.png - hierarchical clustering diagram
4. cluster_results.csv - cluster results for set of maps
5. cluster_x_3d_diagram - alignment of cluster members (one for each cluster)
# Example
This example uses maps from the numerous pre-cleavage, cleavage intermediate (and bound target), and post-cleavage states of Cas9 in the paper by *Das et. al (2023)*.
1. similarity_matrix_heatmap.png - correlation scores (0<x<1) for all pairs of maps.
![](https://i.ibb.co/zf0T7Gh/similarity-matrix-heatmap.png)
2. similarity_matrix.csv - same data as the png
|1|0.0983|0.3062|0.09|0.2794|0.0325|
|0.0983|1|0.1154|0.1603|0.1011|0.1554|
|0.3062|0.1154|1|0.102|0.2599|0.0506|
|0.09|0.1603|0.102|1|0.0857|0.0444|
|0.2794|0.1011|0.2599|0.0857|1|0.0383|
|0.0325|0.1554|0.0506|0.0444|0.0383|1|
3. dendrogram.png - hierarchical clustering diagram
![](https://i.ibb.co/C1rWNR5/dendrogram.png)
4. cluster_results.csv - cluster results for set of maps
|Custom_Name|Cluster_Label|
|Cleavage Intermediate 1|1|
|Pre-cleavage|2|
|Cleavage Intermediate 2|1|
|Post-cleavage 2|0|
|Target bound|1|
|Post-cleavage 1|2|
5. cluster_x_3d_diagram - alignment of cluster members (one for each cluster)
![](https://i.ibb.co/zFLbSyG/cluster-0-3d-average.png_)
![](https://i.ibb.co/VYdRsK5/cluster-1-3d-average.png)
![](https://i.ibb.co/1TzH064/cluster-2-3d-average.png)
