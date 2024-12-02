_your zenodo badge here_

# Pollack-etal_2024_pnas

**Funding rules that promote equity in climate adaptation outcomes**

Adam Pollack<sup>1\*</sup>, Sara Santamaria-Aguilar<sup>2,3</sup>, Pravin Maduwantha<sup>2,3</sup>, Casey Helgeson<sup>4,5</sup>, Thomas Wahl<sup>2,3</sup>, Klaus Keller<sup>1</sup>

<sup>1 </sup> Thayer School of Engineering, Dartmouth College; Hanover, 03755, USA.

<sup>2 </sup> Department of Civil, Environmental and Construction Engineering, University of Central Florida; Orlando, 32816, USA.

<sup>3 </sup> National Center for Integrated Coastal Research, University of Central Florida; Orlando, 32816, USA.

<sup>4 </sup> Earth and Environmental Systems Institute, Penn State University; State College, 16801, USA.

<sup>5 </sup> Department of Philosophy, Penn State University; State College, 16801, USA.

\* corresponding author:  adam.b.pollack@dartmouth.edu

## Abstract
Many climate policies adopt improving equity as a key objective. A key challenge is that policies often conceive of equity in terms of individuals but introduce strategies that focus on spatially coarse administrative areas. For example, the Justice40 Initiative in the United States requires 518 diverse federal programs to prioritize funds for “disadvantaged” census tracts. This strategy is largely untested and contrasts with the federal government’s definition of equity as the “consistent and systematic fair, just and impartial treatment of all individuals [^1].” How well does the Justice40 approach improve equity in climate adaptation outcomes across individuals? We analyze this question using a case study of a municipality that faces repetitive flooding and struggles to effectively manage these risks due to limited resources and public investment. We find that the way the Federal Emergency Management Agency implements the Justice40 Initiative can be an obstacle to promoting equity in household flood-risk outcomes. For example, in this case study, ensuring the majority of benefits accrue in “Justice40 Communities” does not reduce risk for the most burdened households, does not reduce risk-burden inequality, and produces net costs. In contrast, we design simple funding based on household risk burden that cost-effectively target the most burdened households, reduce risk-burden inequality, and accrue large net benefits. Our findings suggest that “disadvantaged community” indicators defined at coarse spatial scales face the risk of poorly capturing many climate risks and can be ineffective for meeting equity promises about climate-related investments.  

## Journal reference
Will update upon publication.

## Overview of this repository
This repository includes the code and instructions for reproducing the main analysis in the paper *Funding rules that promote equity in climate adaptation outcomes.* Collaborators conducted an extreme value analysis and ran an inundation model on the results of that analysis to produce the flood hazard maps for the main analysis. The outputs of the inundation model runs are cited in the next section as a minted repository. The code and instructions to reproduce both analyses can be found [here](https://github.com/CoRE-Lab-UCF/Pollack_et_al_2024/tree/main). 

## Data references

### Input data
 Several datasets were downloaded from minted data repositories. 

| Dataset | DOI |
|---------|-----|
| Flood Hazard Maps for case study | https://doi.org/10.5281/zenodo.14260630 |
| HAZUS & NACCS depth-damage functions | https://zenodo.org/doi/10.5281/zenodo.10027235 |

Note: the HAZUS & NACCS depth-damage functions are included when you clone this repository. 

Some datasets were not available from minted repositories. Most of this data is downloaded in the notebook `risk_estimates.ipynb`. However, there is one dataset we could not download in this notebook: the [FY 2023 ACS 5-Year 2011-2015 Low- and Moderate-Income Summary Data](https://www.hudexchange.info/programs/acs-low-mod-summary-data/). The download link is https://www.hudexchange.info/sites/onecpd/assets/File/ACS_2015_lowmod_blockgroup_all.xlsx. This dataset is included when you clone the repository. 

We also use the [OpenFEMA Dataset: Hazard Mitigation Assistance Projects - v3](https://www.fema.gov/openfema-data-page/hazard-mitigation-assistance-projects-v3) data to characterize historic elevation project costs. We downloaded from the API endpoint for FIPS 34007, the county code for Gloucester City, NJ. Because the data set depreciates over time, we make the data we downloaded available when you clone this repository. We also did this for other OpenFEMA datasets used in this analysis, which are read in the `supplementary.ipynb` notebook.  

We use the the [Census Bureau of Labor Statistics construction price indices for single family houses under construction](https://www.census.gov/construction/cpi/current.html) to inflation-adjust the historic project costs. This data is available in the `resources/` directory. We use those price indices, and the [Bureau of Labor Statistics non-seasonally adjusted index for wages and salaries for privacy industry workers in construction](https://fred.stlouisfed.org/series/CIU2022300000000I) to inflation-adjust elevation cost estimates (i.e. those used in the decision analysis, not those in the OpenFEMA dataset). This data is also available in the `resources/` directory. 

### Contributing model software
| Model | Repository Link | Version
| ----- | --------------- | ------|
| Random Discounting | https://github.com/vsrikrish/random-discount | n/a |
| Uncertain Structure and Fragility Ensemble (UNSAFE) framework for property-level flood risk estimation | https://github.com/abpoll/unsafe | 0.1|

We forked this repository, which can be found [here](https://github.com/abpoll/random-discount), and ran the code to generate 10,000 stochoastic realizations of discount rate chains for 100 years into the future. This  dataset is included when you clone the present repository (also the forked random-discount repository). 

### Output data
Will upload a minted data release with all data in the data/ directory. 

## Reproduce our experiment
You can follow the instructions below to reproduce all results reported in the manuscript and supplementary materials. For this experiment, reproduction does not imply bit-wise reproducibility because there are stochastic processes. You should obtain similar quantitative results and figures. 

If you would like to check for internal bit-wise correctness, you can do so by assessing the output data we link to above. In addition to figures and outputs, we also include all downloaded, raw, and interim data. You can test whether the interim data, which includes realizations of the simulations we used for the published study, is consistent with the processed final data. Note that if you want to inspect the interim and output data from the Zenodo link provided earlier, you should not run code that produces interim data or results. 

These reproduction instructions assume you are familiar with [Mamba](https://mamba.readthedocs.io/en/latest/) or [Conda](https://conda.io/projects/conda/en/latest/user-guide/getting-started.html) and running [Jupyter notebooks](https://jupyter.org/).

To reproduce:

1. Clone this repository into a local directory.
2. Get your environment ready. We recommend using `mamba`. 

    a) Run `mamba env create -f env/env.yml` or replace `mamba` with `conda`.

    b) Once this is complete, run `mamba activate gc_elev`. 

    c) Create an ipykernel for the environment. If you are new to Jupyter Notebooks and/or conda, please see: https://ipython.readthedocs.io/en/stable/install/kernel_install.html#kernels-for-different-environments. We ran `python -m ipykernel install --user --name gc_elev`.

    d) Run `pip install git+https://github.com/abpoll/unsafe@v0.1` to use the modules in UNSAFE. 

3. Set up the [Input data](#input-data).

    a) Run `mkdir data/raw/external/haz/` then download the flood hazard maps (will update with the link when it's ready), which are available as a .zip directory, and unzip them. Move the unzipped files and directories into `data/raw/external/haz/`.

4. Make sure you activate the correct `conda` or `mamba` environment and run all cells in the following notebooks in the `workflow` directory in the following order: 

| Script Name | Description | Stochastic?|
| --- | --- | -- |
| `risk_estimates.ipynb` | Download and unzip data, prepare and generate ensemble of risk estimates | Yes |
| `optimal_elev.ipynb` | Use ensembles to find optimal heightening for each structure | Yes |
| `allocate_funds.ipynb` | Apply funding rules | No |
| `results.ipynb` | Generate figures and summary statistics | No |
| `supplementary.ipynb` | Generate supplementary material, mostly figures | No |


This experiment was designed and run on an Ubuntu 22.04.4 LTS (GNU/Linux 5.15.0-102-generic x86_64) machine with mamba version 1.4.2.

This experiment was successfully reproduced on the same machine by Alexis Hudes on September 11, 2024. An earlier version of this experiment was successfully reproduced on a macOS Sonoma 14.2.1 with mamba version 1.5.8 by Prabhat Hegde on May 20, 2024.

Please contact Adam Pollack at adam.b.pollack@dartmouth.edu if you have any issues following these instructions.

[^1]: https://www.federalregister.gov/documents/2021/01/25/2021-01753/advancing-racial-equity-and-support-for-underserved-communities-through-the-federal-government