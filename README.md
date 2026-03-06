# COZI, SEA and scimap analysis for NEP method comparison

In this repository, we show how to run COZI yourself and we provide code to reproduce the analysis of simulated and biological datasets with scimap, SEA and COZI for the manuscript Schiller et al. (2025) for NEP method comparison here: https://github.com/SchapiroLabor/NEP_comparison. Scimap is a versatile spatial analysis suite and offers a spatial interaction function to infer statistically enriched neighbor preferences (NEP). Scimap outputs scaled normalized interactions as NEP scores and p-values. We forked the scimap repo and adapted the framework to output a z-score and total count normalization (spatial enrichment analysis (SEA)) or a z-score with conditional count normailzation (COZI) here: https://github.com/SchapiroLabor/scimap_COZI. 

# Running COZI

## Installation

We recommend creating a clean conda environment
`conda create -n scimap_env python=3.10 pip -c conda-forge -c defaults`
`conda activate scimap_env`
Then install scimap_COZI directly from GitHub:
`pip install git+https://github.com/SchapiroLabor/scimap_COZI.git`

Installing COZI in a conda environment and importing it in Python each take less than one minute. Running COZI with 300 permutations on a sample of 2,000 cells takes under 30 seconds*.

## Tutorial COZI

The input data for the `sm.tl.spatial_interaction()` function is an adata object. The x, y and cell type columns in the adata.obs can be specified in the function itself.
We created a tutorial notebook with a subset of the simulated data in `/tutorial` to get you started with your own analysis.

# Reproduce results in NEP comparison

## Dependencies

For running scimap, we created a conda environment with dependencies specified in 
`/envs/env_scimap.yml`

For running COZI or SEA, we created a conda environment with dependencies specified in 
`/envs/env_cozi_sea.yml`. 

## Data

### In silico tissue (IST) data
Simulated .csv data with x, y, and ct annotation columns were used. The asymmetric and symmetric in silico tissue (IST) datasets can be accessed here https://github.com/SchapiroLabor/NEP_comparison/simulated_data and can be reproduced here: https://github.com/SchapiroLabor/NEP_IST_generation.

### SpaSim simulated data
Simulated .csv data with x, y, and ct annotation columns were used. The SpaSim generated datasets can be accessed here https://github.com/SchapiroLabor/NEP_comparison/simulated_data and can be reproduced here: https://github.com/SchapiroLabor/NEP_SpaSim.

### Myocardial infarction (MI) data

Sequential Immunofluorescence data was accessed via Synapse (project SynID : syn51449054): https://www.synapse.org/Synapse:syn51449054. The dataframe with phenotypes was accessed within the project at:  https://www.synapse.org/Synapse:syn65487454.

### Triple negative breast cancer (TNBC) data
TNBC data can be found at https://www.angelolab.com/mibi-data. We used the processed data from https://github.com/psl-schaefer/report/tree/master/data.

## Scripts

`/notebooks`:
- `/MI_data`: 
    - `/COZI_scimap_MI_data.ipynb`: This script runs COZI on the MI data using a knn (k=5) as neighborhood definition (Figure 6).  
    - `/COZI_scimap_MI_data_Supplementary_fig_10_11.ipynb`: This script runs COZI on the MI data using a various neighborhood definitions and correlates results. It also correlates CCR and cell typ (Supplementary Figure 10 nd 11).  
    - `/SEA_scimap_MI_data.ipynb`: This script runs SEA on the MI data using a knn (k=5) as neighborhood definition (Figure 6).  
    - `/scimap_MI_data.ipynb`: This script runs scimap on the MI data using a knn (k=5) as neighborhood definition (Figure 6).  
    - `/region_ct_abundances_MI_data.ipynb`: This script generates the cell type abundance Figures of the MI dataset (Figure 4cd, Supplementary Figure 7b)
    - `/COZI_scimap_MI_data_Supplementary_fig_12.ipynb`: This script runs COZI on the MI data using a various neighborhood definitions and plots COZI scores of specific interactions (Supplementary Figure 12)
- `/simulated_data`: 
    - `/COZI_scimap_simulated_data_IST.ipynb`: This script runs COZI on the IST simulated data using a Delaunay triangulation as neighborhood definition (Figure 2 and 3). 
    - `/COZI_scimap_simulated_data_IST.ipynb`: This script runs COZI on the SpaSim simulated data using a Delaunay triangulation as neighborhood definition (Figure 4).  
    - `/SEA_scimap_simulated_data.ipynb`: This script runs SEA on the simulated data using a Delaunay triangulation as neighborhood definition (Figure 2 and 3).  
    - `/scimap_simulated_data.ipynb`: This script runs scimap on the simulated data using a Delaunay triangulation as neighborhood definition (Figure 2 and 3). The delaunay neighborhood definition was added to the `spatial_interaction.py`` script in `/spatial_interaction_delaunay.py` and is monkey patched in the script.
- `/TNBC_data`: 
    - `/COZI_scimap_TNBC.ipynb`: This script runs COZI and SEA on the TNBC data using knn (k=5) as neighborhood definition (Figure 5). 


`/scripts`:
- `/spatial_interaction_delaunay.py`: This scripts provides an adapted version of the spatial_interaction.py script in scimap. It includes delaunay graph neighborhood definition and is called from `/scimap_simulated_data.ipynb`.  

`/tutorial`:
- `/COZI_tutorial.ipynb`: This notebook provides a short tutorial on how to run COZI based on the spatial_interaction function of scimap.  
- `/tutorial_data`: This folder contains 9 .csv files of the simulated cohort (see IST data) with a random, weak and strong self-interaction of cell type 0.



*Run on an Apple Silicon M1. Installation works on Windows 11, Ubuntu 22.04, Mac Sonoma 14.2.1. 
