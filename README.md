
# Gene Regulatory Network Inference using GENIE3 (RNA-seq)

## Overview

This repository contains an **end-to-end R pipeline for inferring gene regulatory networks (GRNs)** from bulk RNA-seq data using **GENIE3**, a random forest–based machine learning method.
The analysis focuses on identifying **transcription factor (TF)–target gene relationships**, **master regulators**, and **condition-specific network rewiring**.

The workflow starts from **raw count data downloaded from GEO** and proceeds through normalization, network inference, biological interpretation, and validation against known TF–target interactions.

---

## What this analysis does

* Infers **directed TF → target gene regulatory interactions**
* Identifies **master regulatory transcription factors**
* Compares regulatory networks between **experimental conditions**
* Performs **functional enrichment** of TF target genes
* Analyzes **network topology and centrality**
* Validates predictions using **DoRothEA curated regulons**

---

## Data

* **Input:** Bulk RNA-seq count matrix (GEO: `GSE261875`)
* **Organism:** Human
* **Conditions:** Wild-type vs AKO (condition-specific network comparison)

---

## Workflow Summary

1. **Data acquisition**

   * Download RNA-seq count data from GEO
   * Extract and clean sample metadata

2. **Preprocessing**

   * Filter low-count and low-variance genes
   * Normalize counts using **DESeq2 (VST)**

3. **Transcription factor definition**

   * Curated human TF list from **DoRothEA**
   * Restrict TFs to genes present in the expression matrix

4. **Network inference**

   * Run **GENIE3** to infer TF → target interactions
   * Rank interactions by importance score

5. **Master regulator analysis**

   * Identify TFs with strongest regulatory influence
   * Extract high-confidence TF–target relationships

6. **Functional interpretation**

   * GO Biological Process enrichment of TF targets
   * Identification of regulatory hierarchies and cascades

7. **Condition-specific analysis**

   * Separate GRNs for WT and AKO
   * Identify shared, lost, and gained regulatory interactions

8. **Network analysis & visualization**

   * Graph-based analysis using **igraph**
   * Centrality metrics (degree, betweenness, closeness)
   * Visualization of top regulatory interactions

9. **Validation**

   * Compare predictions with **DoRothEA A/B/C confidence regulons**
   * Assess overlap and precision of top GENIE3 predictions

---

## Key Outputs

* `results/genie3_all_links.tsv` – All inferred TF–target interactions
* `results/tf_regulatory_statistics.tsv` – Master regulator statistics
* `results/validated_tf_target_predictions.tsv` – Validated interactions
* `results/tf_comparison_wt_vs_ako.tsv` – Condition-specific TF activity
* `plots/` – Network visualizations and enrichment plots

---

## Interpretation Notes

* Low validation precision (≈1–5%) is **expected** for GRN inference
* Many predictions may be **novel or context-specific**
* GENIE3 predicts **regulatory influence**, not direct binding
* Experimental validation (e.g. ChIP-seq, perturbation assays) is required

---

## Dependencies

Key R packages:

* `GENIE3`
* `DESeq2`
* `dorothea`
* `igraph`
* `clusterProfiler`
* `org.Hs.eg.db`
* `ggplot2`, `dplyr`, `pheatmap`

All required packages are installed automatically in the script.

---

## How to run

```r
# Open R
source("Script.R")
```

## Use cases

* Discover **master regulators** in RNA-seq datasets
* Study **regulatory network rewiring** in perturbation experiments
* Generate hypotheses for **TF-target validation**
* Complement differential expression and pathway analysis

