<p align="center">
  <img src="logo.svg" alt="TaxaGO Logo" width="500"/>
</p>

---

# TaxaGO Manuscript: Chordata Case Study

<p align="left">
  <a href="https://www.gnu.org/licenses/gpl-3.0"><img src="https://img.shields.io/badge/License-GPLv3-blue.svg" alt="License: GPL v3"></a>
  <a href="https://www.rust-lang.org"><img src="https://img.shields.io/badge/Rust-1.87+-orange.svg" alt="Rust Version"></a>
  <img src="https://img.shields.io/badge/Version-v1.0.0-green.svg" alt="TaxaGO Version">
</p>

This repository provides the data and Python scripts (Jupyter Notebooks) used to perform the Chordata case study detailed in the TaxaGO manuscript. The analysis focuses on proteins with identified taxonomic quasi-primes (QPs), as described in:

Bochalis, E., Patsakis, M., Chantzi, N., Mouratidis, I., Chartoumpekis, D., & Georgakopoulos-Soares, I. (2025). *Unraveling diversity by isolating peptide sequences specific to distinct taxonomic groups*. bioRxiv, 2025.02.05.636664. doi: [10.1101/2025.02.05.636664](https://doi.org/10.1101/2025.02.05.636664)

Specifically, this case study utilizes QP data from the Chordata Phylum where the ε-score is greater than 90.00%.


## Overview

The repository includes two main scripts:

1.  **`generate_study_pop.ipynb`**: This notebook preprocesses the initial Chordata quasi-prime data. It filters this dataset based on Taxon IDs that are also present in the lineage file (sourced from `taxago_assets`), creating a refined "study population" CSV file.
2.  **`analyze_results.ipynb`**: This notebook performs an analysis of Gene Ontology Enrichment Analysis (GOEA) results derived from the Chordata study. It identifies the top 10 statistically significant GO terms for Biological Process, Molecular Function, and Cellular Component namespaces and visualizes their log(Odds Ratio) using a Circos plot.


## Prerequisites

* Python 3
* Jupyter Notebook or JupyterLab
* Python libraries for the analysis:
    * pandas
    * numpy
    * pathlib
    * matplotlib
    * textwrap
    * pycirclize
* TaxaGO


## Scripts in Detail

### 1. `generate_study_pop.ipynb`

* **Purpose:** Filters the Chordata quasi-prime dataset to create a "study population" file. The filtering ensures that only Taxon IDs present in both the QP dataset and a `taxago_assets` lineage file are retained.
* **Inputs:**
    * `original_chordata_qp_data.csv`: CSV file containing the original QP data for Chordata. Columns should represent Taxon IDs.
    * `$CARGO_HOME/taxago_assets/lineage.txt`: Tab-separated lineage file.
* **Output:**
    * `chordata_study_pop.csv`: CSV file with the filtered QP data. 625 common Taxon IDs were included.
* **Key Libraries Used:** `pandas`, `pathlib`
* **How to Run:**
    1.  Place `original_chordata_qp_data.csv` in the same directory as the notebook.
    2.  Verify the `lineage.txt` file is at `$CARGO_HOME/taxago_assets/lineage.txt`.
    3.  Execute all cells within the `generate_study_pop.ipynb` notebook.

### 2. `analyze_results.ipynb`

* **Purpose:** Analyzes Chordata Gene Ontology Enrichment Analysis (GOEA) results. It extracts the top 10 significant terms for each GO namespace (Biological Process, Molecular Function, Cellular Component), based on statistical significance and log(Odds Ratio), and visualizes these using a Circos plot.
* **Inputs:**
    * `results/combined_taxonomy_results/Chordata_GOEA_results.txt`: Tab-separated file with GOEA results.
* **Outputs:**
    * `top_results.tsv`: Tab-separated file listing the top 10 GO terms for each namespace.
    * `top_results.svg`: SVG image of the Circos plot showing log(Odds Ratio) for the top terms.
* **Key Libraries Used:** `pandas`, `numpy`, `matplotlib`, `textwrap`, `pycirclize`
* **How to Run:**
    1.  Ensure `Chordata_GOEA_results.txt` is in the `results/combined_taxonomy_results/` subdirectory.
    2.  Execute all cells within the `analyze_results.ipynb` notebook.


## How to reproduce
1. **Install TaxaGO:** Details for this installation can be found in the main [TaxaGO repository](https://github.com/Georgakopoulos-Soares-lab/TaxaGO)
2. **Clone this repository:**
    ```bash
    git clone https://github.com/Georgakopoulos-Soares-lab/TaxaGO_case_study
    ```

3. **Install external Python dependencies:**
    ```bash
    pip install pandas numpy pathlib matplotlib textwrap pycirclize
    ```
4.  **Prepare Study Population:** Run `generate_study_pop.ipynb` to generate `chordata_study_pop.csv`. While this specific output isn't a direct input for `analyze_results.ipynb`, it represents a crucial data preparation step in the overall research workflow that leads to the GOEA results.
5. **Run TaxaGO with the phylogenetic meta-analysis enabled:**
    ```bash
    taxago -s chordata_study_pop.csv -d results -p classic -c benjamini-hochberg -g phylum
    ```
5.  **Analyze GOEA Results:** Once GOEA has been performed (using the study population or related data), place the results file at `results/combined_taxonomy_results/Chordata_GOEA_results.txt`.
6.  **Visualize and Extract:** Run `analyze_results.ipynb` to extract the top GO terms into `top_results.tsv` and generate the `top_results.svg` Circos plot.


## Contact
For any questions or support, please contact:
* izg5139@psu.edu
* left.bochalis@gmail.com
* antonpapg@gmail.com