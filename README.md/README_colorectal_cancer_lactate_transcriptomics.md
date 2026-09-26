# Colorectal Cancer Lactate Transcriptomics

## Overview

This project investigates how lactate exposure alters the transcriptomic profile of **SW480 colorectal cancer cells** using publicly available RNA-seq count data from **GSE180948**.

The analysis compares:

- **3 SW480 control samples (NC)**
- **3 SW480 lactate-treated samples (LA)**

The main objective is to identify differentially expressed genes and biological pathways associated with the response of colorectal cancer cells to lactate.

---

## Biological Question

**How does lactate exposure modify gene expression and biological pathways in SW480 colorectal cancer cells?**

---

## Dataset

**Source:** GEO accession GSE180948

The count matrix contains RNA-seq expression data from two colorectal cancer cell lines:

- DLD1
- SW480

For this project, only the **SW480** samples were used in the primary analysis to avoid introducing variation caused by differences between cell lines.

Samples analyzed:

| Sample | Condition |
|---|---|
| SW480_NC_1 | Control |
| SW480_NC_2 | Control |
| SW480_NC_3 | Control |
| SW480_LA_1 | Lactate |
| SW480_LA_2 | Lactate |
| SW480_LA_3 | Lactate |

---

## Workflow

```text
Raw RNA-seq counts
        ↓
Data inspection
        ↓
Selection of SW480 samples
        ↓
Low-expression gene filtering
        ↓
DESeq2 normalization
        ↓
Variance Stabilizing Transformation (VST)
        ↓
Principal Component Analysis (PCA)
        ↓
Differential expression analysis
        ↓
Volcano plot
        ↓
Heatmap
        ↓
GO / KEGG / Reactome enrichment
        ↓
Biological interpretation
```

---

## Tools

The project was performed in Python using:

- pandas
- numpy
- scipy
- matplotlib
- scikit-learn
- PyDESeq2
- gseapy
- Jupyter Notebook

---

## Quality Control and PCA

After filtering low-expression genes, normalized and variance-stabilized expression values were used for PCA.

The first two principal components explained:

- **PC1: 68.7%**
- **PC2: 14.4%**

Together, PC1 and PC2 explained **83.1% of the total variance**.

The three control samples clustered on one side of PC1, while the three lactate-treated samples clustered on the opposite side, indicating a strong transcriptomic effect associated with lactate exposure.

---

## Differential Expression Analysis

Differential expression was performed using **PyDESeq2** with the contrast:

```text
Lactate vs Control
```

Significance thresholds:

```text
Adjusted p-value < 0.05
|log2FoldChange| >= 1
```

Results:

- **533 differentially expressed genes**
- **355 upregulated genes**
- **178 downregulated genes**

Examples of strongly upregulated genes include:

- HSPA6
- CSF3
- NDRG1
- CYP1A1
- MN1
- HK2
- VEGFA
- PTGS2
- IL1B
- SERPINE1

---

## Functional Enrichment Analysis

Functional enrichment was performed using:

- Gene Ontology Biological Process
- KEGG
- Reactome

Among the upregulated genes, **50 pathways were significantly enriched** using an adjusted p-value threshold of 0.05.

Major enriched biological themes included:

- positive regulation of angiogenesis
- vasculature development
- hypoxia response
- cytokine and inflammatory signaling
- cell motility
- growth-factor signaling

No pathway reached the adjusted p-value < 0.05 threshold among the downregulated genes in this analysis.

---

## Biological Interpretation

The results indicate that lactate exposure is associated with a major reprogramming of gene expression in SW480 colorectal cancer cells.

The transcriptomic response is particularly associated with genes and pathways related to:

- angiogenesis
- adaptation to hypoxia
- inflammatory signaling
- cellular stress
- tumor-associated metabolism
- cell migration and motility

Genes such as **VEGFA, HK2, NDRG1, PTGS2, IL1B, CXCL8, SERPINE1 and HILPDA** support these biological themes.

These results suggest that lactate is associated with molecular programs relevant to tumor adaptation and the tumor microenvironment.

This analysis demonstrates association at the transcriptomic level and does not by itself establish a causal effect on phenotypes such as invasion or angiogenesis.

---

## Project Structure

```text
colorectal-cancer-lactate-transcriptomics/
│
├── data/
│   └── GSE180948_All.counts.txt
│
├── notebooks/
│   └── 01_data_exploration.ipynb
│
├── results/
│   ├── deseq2_all_results.csv
│   ├── deseq2_significant_genes.csv
│   ├── upregulated_genes.csv
│   ├── downregulated_genes.csv
│   ├── volcano_plot.png
│   ├── top20_heatmap.png
│   └── top_enriched_pathways.png
│
├── README.md
└── requirements.txt
```

---

## Main Figures

### PCA

The PCA clearly separates control and lactate-treated SW480 samples along PC1.

### Volcano Plot

The volcano plot highlights genes showing both statistically significant and biologically meaningful expression changes.

### Heatmap

The top differentially expressed genes show a clear expression contrast between lactate-treated and control samples.

### Functional Enrichment

Enrichment analysis identifies biological processes associated mainly with angiogenesis, hypoxia response, signaling and cell motility.

---

## Skills Demonstrated

- RNA-seq data handling
- transcriptomic quality control
- gene-expression filtering
- normalization and VST
- PCA
- differential expression analysis
- volcano plot visualization
- heatmap visualization
- GO / KEGG / Reactome enrichment
- biological interpretation of cancer transcriptomics
- reproducible Python workflow

---

## Possible Extensions

Future analyses could include:

1. repeating the same workflow on the DLD1 cell line;
2. comparing shared and cell-line-specific lactate responses;
3. performing ranked-list GSEA instead of only over-representation analysis;
4. integrating additional colorectal cancer transcriptomic datasets;
5. investigating candidate genes associated with metabolic adaptation and tumor progression.

---

## Author

Bioinformatics project developed as part of training in cancer transcriptomics and computational biology.
