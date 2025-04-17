# COZI, SEA and scimap analysis for NEP methods comparison

Scimap is a versatile spatial analysis suite and offers a spatial interaction function to infer statistically enriched neighbor preferences (NEP). Scimap outputs scaled normalized interactions as NEP scores and p-values. We forked the scimap repo and adapted the framework to output a z-score and total count normalization (spatial enrichment analysis (SEA)) or a z-score with conditional count normailzation (COZI) here: https://github.com/SchapiroLabor/scimap_COZI. In this repository, we analyse simulated and MI data with scimap, SEA and COZI for the manuscript Schiller et al. (2025) for NEP method comparison here: https://github.com/SchapiroLabor/NEP_comparison

# Usage

## Installation

For running scimap, we created a conda environment with dependencies specified in 
`/envs/env_scimap.yml`

For running COZI or SEA, we created a conda environment with dependencies specified in 
`/envs/env_cozi_sea.yml`. Installing COZI in a conda environment and importing it in Python each take less than one minute. Running COZI with 300 permutations on a sample of 2,000 cells takes under 30 seconds*.

## Tutorial COZI

We created a tutorial notebook with a subset of the simulated data in `/tutorial` to get you started with your own analysis.

## Data

### In silico tissue (IST) data
Simulated .csv data with x, y, and ct annotation columns were used. The asymmetric and symmetric in silico tissue (IST) datasets were generated as described here: https://github.com/SchapiroLabor/NEP_IST_generation. 

### Myocardial infarction (MI) data

Sequential Immunofluorescence data was accessed via Synapse (project SynID : syn51449054): https://www.synapse.org/Synapse:syn51449054. The dataframe with phenotypes was accessed within the project at:  https://www.synapse.org/Synapse:syn65487454.

## Scripts

`/notebooks`:
- `/MI_data`: 
    - `/COZI_scimap_MI_data.ipynb`: This script runs COZI on the MI data using a knn (k=5) as neighborhood definition.  
    - `/SEA_scimap_MI_data.ipynb`: This script runs SEA on the MI data using a knn (k=5) as neighborhood definition.  
    - `/scimap_MI_data.ipynb`: This script runs scimap on the MI data using a knn (k=5) as neighborhood definition.  
    - `/region_ct_abundances_MI_data.ipynb`: This script generates the cell type abundance Figures of the MI dataset (Figure 4cd, Appendix Figure 7b)  
- `/simulated_data`: 
    - `/COZI_scimap_simulated_data.ipynb`: This script runs COZI on the simulated data (asymmetric or symmetric) using a Delaunay triangulation as neighborhood definition.  
    - `/SEA_scimap_simulated_data.ipynb`: This script runs SEA on the simulated data (asymmetric or symmetric) using a Delaunay triangulation as neighborhood definition.  
    - `/scimap_simulated_data.ipynb`: This script runs scimap on the simulated data (asymmetric or symmetric) using a Delaunay triangulation as neighborhood definition. The delaunay neighborhood definition was added to the spatial_interaction.py script in `/spatial_interaction_delaunay.py` and is monkey patched in the script.  

`/scripts`:
- `/spatial_interaction_delaunay.py`: This scripts provides an adapted version of the spatial_interaction.py script in scimap. It includes delaunay graph neighborhood definition and is called from `/scimap_simulated_data.ipynb`.  

`/tutorial`:
- `/COZI_tutorial.ipynb`: This notebook provides a short tutorial on how to run COZI based on the spatial_interaction function of scimap.  
- `/tutorial_data`: This folder contains 9 .csv files of the simulated cohort (see IST data) with a random, weak and strong self-interaction of cell type 0.



*Run on an Apple Silicon M1. Installation works on Windows 11, Ubuntu 22.04, Mac Sonoma 14.2.1. 
