# 🤝 Contributing to BioScriptR

Thank you for wanting to contribute to BioScriptR! Every script, fix, or suggestion makes this resource better for thousands of bioinformaticians worldwide.

---

## 📌 Ground Rules

- All scripts must be written in **R**
- Code must be **tested and working**
- Every script must follow the **standard template** (see below)
- Be respectful and constructive in all interactions
- No script is too simple — beginner scripts are just as valuable as advanced ones

---

## 📋 The Standard Script Template

Every `.Rmd` file you contribute must follow this structure exactly:

````markdown
---
title: "Your Script Title"
category: "e.g. RNA-seq"
subcategory: "e.g. Differential Expression"
packages: "e.g. DESeq2, dplyr, ggplot2"
r_version: "4.4.0"
package_versions: "DESeq2 1.42.0, dplyr 1.1.4"
author: "Your Name or GitHub username"
date: "YYYY-MM-DD"
difficulty: "Beginner"
---

## Overview
What this script does in 2-3 clear sentences. No jargon — write as if 
explaining to a smart person who is new to this specific method.

## Use Case
The specific biological question this script answers.
Example: "Use this when you have raw count data and a metadata file and 
want to identify genes that are significantly different between two conditions."

## Input
Describe the data this script needs:
- Format (e.g. CSV count matrix, rows = genes, columns = samples)
- Required columns (e.g. metadata must have 'sample' and 'condition' columns)
- Where to get example data (e.g. GEO accession, built-in dataset)

## Required Packages
```r
# Install if needed:
# BiocManager::install("DESeq2")
# install.packages("dplyr")

library(DESeq2)
library(dplyr)
```

## Code
```r
# ----------------------------------------------------------
# Step 1: Load your data
# ----------------------------------------------------------
# count_matrix: genes as rows, samples as columns
counts <- read.csv("counts.csv", row.names = 1)

# metadata: must have 'sample' and 'condition' columns
metadata <- read.csv("metadata.csv")

# ----------------------------------------------------------
# Step 2: Create DESeq2 object
# ----------------------------------------------------------
dds <- DESeqDataSetFromMatrix(
  countData = counts,
  colData   = metadata,
  design    = ~ condition   # change 'condition' to your variable
)

# ----------------------------------------------------------
# Step 3: Run differential expression
# ----------------------------------------------------------
dds <- DESeq(dds)
res <- results(dds, alpha = 0.05)

# ----------------------------------------------------------
# Step 4: View results
# ----------------------------------------------------------
summary(res)
head(res[order(res$padj), ])
```

## Output
Describe what the user gets:
- A DESeqResults table with log2FoldChange, padj, etc.
- Genes sorted by adjusted p-value

## Common Errors & Fixes

**Error:** `"object 'condition' not found"`  
**Fix:** Make sure your metadata column name matches exactly what you put in `design = ~ condition`

**Error:** `"size factor estimates"`  
**Fix:** You may have too few counts. Try `estimateSizeFactors(dds)` manually first.

## References
- Love MI et al. (2014) Moderated estimation of fold change. *Genome Biology*. https://doi.org/10.1186/s13059-014-0550-8
- DESeq2 vignette: https://bioconductor.org/packages/release/bioc/vignettes/DESeq2/inst/doc/DESeq2.html
````

---

## 🗂️ Which Folder Does My Script Go In?

| Your Script Is About | Folder |
|----------------------|--------|
| DESeq2, edgeR, limma, differential expression | `01_RNA-seq/` |
| Seurat, SingleCellExperiment, scRNA-seq | `02_Single-Cell/` |
| VCF files, SNPs, variant annotation | `03_Variant-Analysis/` |
| ChIP-seq, ATAC-seq, methylation | `04_Epigenomics/` |
| 16S rRNA, shotgun metagenomics | `05_Metagenomics/` |
| Mass spectrometry, protein abundance | `06_Proteomics/` |
| ggplot2, heatmaps, volcano plots | `07_Visualization/` |
| Classification, clustering, PCA | `08_Machine-Learning/` |
| FastQC, normalization, outliers | `09_QC-and-Preprocessing/` |
| Survival, mixed models, power | `10_Statistical-Methods/` |
| dplyr, tidyr, data reshaping | `11_Data-Wrangling/` |
| GO, KEGG, GSEA, pathway analysis | `12_Pathway-and-Enrichment/` |
| Ensembl, BioMart, GEO queries | `13_Genomic-Databases/` |
| renv, reproducibility, workflows | `14_Reproducibility/` |

---

## 🔤 File Naming Convention

Use lowercase with underscores. Be specific:

```
✅ deseq2_basic_two_group.Rmd
✅ volcano_plot_ggplot2_labeled.Rmd
✅ seurat_clustering_workflow.Rmd

❌ script1.Rmd
❌ myanalysis.Rmd
❌ DESeq.Rmd
```

---

## 📤 How to Submit Your Script (Step by Step)

**Step 1 — Fork the repository**
Go to https://github.com/josh45-source/BioScriptR and click **"Fork"**

**Step 2 — Clone your fork**
```bash
git clone https://github.com/YOUR_USERNAME/BioScriptR.git
cd BioScriptR
```

**Step 3 — Create a new branch**
```bash
git checkout -b add-my-script-name
```

**Step 4 — Add your script**
Place your `.Rmd` file in the correct folder following the template above.

**Step 5 — Commit and push**
```bash
git add .
git commit -m "Add: brief description of what your script does"
git push origin add-my-script-name
```

**Step 6 — Open a Pull Request**
Go to your fork on GitHub → click **"Compare & pull request"** → describe what your script does → submit.

---

## ✅ Pull Request Checklist

Before submitting, make sure:

- [ ] Script follows the standard template
- [ ] File is in the correct folder
- [ ] File name uses lowercase underscores
- [ ] Code is tested and runs without errors
- [ ] R and package versions are noted in the YAML header
- [ ] Comments explain every major step
- [ ] At least one reference is included

---

## 💡 Ideas for Contributions

Not sure what to add? Here are always-needed scripts:

- Any DESeq2, edgeR, or limma workflow variant
- Single-gene expression plots
- GSEA from scratch
- Batch effect correction (ComBat, limma removeBatchEffect)
- Multi-omics integration
- Survival analysis with clinical data
- Any Seurat workflow step
- Publication-quality figure scripts

---

Thank you for being part of BioScriptR. Every line of code you share moves science forward. 🌱
