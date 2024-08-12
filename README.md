Certainly! Here is the updated README content formatted for use in a GitHub repository:

```markdown
# Drug Repurposing Data Integration and Analysis

## Overview

This repository contains R scripts designed for processing and integrating datasets related to drug repurposing. The scripts facilitate the analysis of drug predictions, clean and merge data from various sources, and generate insights into potential drug candidates. The focus areas include drug predictions, blood-brain barrier (BBB) permeability assessments, and Mechanism of Action (MOA) enrichment analysis.

## Prerequisites

Before running the scripts, ensure that you have the following R packages installed. These packages are required for the scripts to execute correctly:

- **readr**: For reading rectangular data files (like CSVs).
- **dplyr**: For data manipulation.
- **ggplot2**: For data visualization.
- **ggrepel**: For creating easily readable plots with non-overlapping labels.
- **tidyr**: For tidying data.
- **readxl**: For reading Excel files.
- **tools**: For file extension and manipulation utilities.
- **metap**: For meta-analysis of p-values.
- **pathprint**: For pathway enrichment analysis.
- **GeneNet**: For inferring gene regulatory networks.

You can install all these packages in R by running:

```r
install.packages(c("readr", "dplyr", "ggplot2", "ggrepel", "tidyr", "readxl", "tools", "metap", "pathprint", "GeneNet"))
```

## Pipeline

The pipeline is structured into three main stages:

### 1. Pathways to Drugs

- **Objective**: Integrate various data sources to identify potential drug candidates based on disease pathway signatures.
- **Process**:
  - Load pathway signatures and perform differential analysis.
  - Match these signatures with existing drug data.
  - Prioritize drugs that might influence the identified pathways.

### 2. Drugs to MOA

- **Objective**: Analyze the Mechanism of Action (MOA) of the prioritized drug candidates.
- **Process**:
  - Merge drug prediction data with metadata.
  - Perform MOA enrichment analysis to identify common mechanisms among the top candidates.
  - Generate plots to visualize the MOA enrichment.

### 3. Drug Name Matching

- **Objective**: Ensure consistency and accuracy in drug names across various datasets.
- **Process**:
  - Standardize drug names and check for inconsistencies.
  - Match drug names against known databases or lists to ensure accuracy.

## Inputs

The pipeline requires several input files, which must adhere to specific formats:

1. **Disease Pathway Signature**:
   - Format: Excel file (.xlsx) with differential pathway activity.
   - Columns: Must include `pathway`, `logFC`, and `adj.P.Val`.

2. **Geneset (GS) File**:
   - Format: RDS file containing the geneset information.
   - Example: `cds_meta_sig.RDS`.

3. **PDxN File**:
   - Format: RDS file, usually generated during the pipeline process.
   - Example: `combined_1_2_3_4_5_6p.adj<1.RDS`.

### Example Input Files

- **Pathway Input**: `../Signature_processing_and_drug_prioritisation/input/glioblastoma/egfr/egfryes.vs.egfrno.xlsx`
- **Geneset Input**: `../System_generation/data/cds_meta_sig.RDS`
- **Generated PDxN**: `../Signature_processing_and_drug_prioritisation/output/glioblastoma/egfr/glioblastoma_egfr_2024-07-10_10_up_29_down_16_qval_0.05_cluster_no_w_cor_scores.csv`

You can find sample files in the `example_files` directory, which demonstrate the required format for each input.

## Outputs

The pipeline generates several key outputs:

1. **Prioritized Drug List**:
   - Format: CSV file containing a ranked list of drug candidates based on the pathway analysis.
   - Example: `glioblastoma_egfr_2024-07-10_10_up_29_down_16_qval_0.05_cluster_no_w_cor_scores.csv`

2. **MOA Enrichment Plots**:
   - Format: PDF and PNG files showing the results of the MOA enrichment analysis.
   - These plots highlight the most common mechanisms among the prioritized drug candidates.

## Instructions for Running the Pipeline

### 1. Update File Names and Paths

Before running the scripts, you need to configure the paths and file names within the scripts. Here's an example configuration:

```r
project_outer_dir <- "glioblastoma"
project_inner_folder <- "egfr"
pathwayFileLocation <- file.path("..", "input", project_outer_dir, project_inner_folder, "")

up_regulated_file_name <- "up_egfryes.vs.egfrno.xlsx"
down_regulated_file_name <- "down_egfryes.vs.egfrno.xlsx"
pathwayDataFilenames <- c("egfryes.vs.egfrno.xlsx")
```

### 2. Set the Project Directories

Ensure that the `project_outer_dir` and `project_inner_folder` variables in both scripts match your folder structure. This will ensure that files are correctly located and processed.

### 3. Execute the Scripts

#### **Pathways to Drugs**

Run the `pathways_to_drugs.R` script to process the pathway data and generate prioritized drug lists.

```bash
Rscript pathways_to_drugs.R "glioblastoma" "egfr" "egfryes.vs.egfrno.xlsx" "cds_meta_sig.RDS" "combined_1_2_3_4_5_6p.adj<1.RDS" 1
```

#### **Drugs to MOA**

Run the `drugs_to_moa.R` script to analyze MOA enrichment and generate visualizations.

```bash
Rscript drugs_to_moa.R "AgingPathwaysforDrugMatchingJune17" "june17"
```

### Example Output

- After running `pathways_to_drugs.R`, you might find the output at: `../Signature_processing_and_drug_prioritisation/output/glioblastoma/egfr/`
- MOA enrichment plots and CSV files will be generated after running `drugs_to_moa.R`.

```

You can paste this content into a `README.md` file in your GitHub repository. This will provide clear instructions and context for users of your repository.
