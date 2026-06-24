🧬 Single‑Cell RNA‑seq Analysis of Invasive Ductal Carcinoma
Author: Sherry Ali
Project Type: Bioinformatics Portfolio — scRNA‑seq Workflow (Seurat + SingleR)
Dataset: Paired 10x Genomics datasets (750‑cell low‑throughput and 7,500‑cell high‑throughput) from the same patient

📌 Overview
This project performs a complete single‑cell RNA‑seq (scRNA‑seq) analysis on two paired 10x Genomics datasets derived from the same Invasive Ductal Carcinoma (IDC) patient. The datasets differ only in throughput:

Low‑throughput (LT): ~750 recovered cells

High‑throughput (HT): ~7,500 recovered cells

The goal of this project was to compare how sequencing depth and cell recovery affect data quality, clustering resolution, and biological interpretability.
By running the entire workflow on both datasets — QC, normalization, PCA, UMAP, clustering, marker detection, and cell type annotation — this analysis highlights the practical differences between low‑ and high‑throughput scRNA‑seq experiments.

As expected, the high‑throughput dataset produced more robust clusters, clearer marker gene patterns, and more reliable cell type annotations, while the low‑throughput dataset showed reduced resolution and noisier QC metrics.

- Low‑ vs High‑Throughput Comparison (Same Patient)
![Throughput Comparison Diagram](assets/throughput_comparison.png)

This visual summarizes the differences between the two datasets and how throughput impacts downstream analysis.

🔬 Methods
1. Data Loading
Two 10x Genomics .h5 matrices were loaded using Read10X_h5() and converted into Seurat objects.

2. Quality Control
QC metrics computed:

nFeature_RNA

nCount_RNA

percent.mt

Cells were filtered using thresholds such as:

nFeature_RNA > 200

percent.mt < 20%

3. Normalization & Feature Selection
Log normalization

Identification of top 2,000 variable genes

Scaling across all genes

4. Dimensionality Reduction
PCA

Elbow plot to determine significant PCs

UMAP embedding using PCs 1–6

5. Clustering
Graph‑based clustering (FindNeighbors, FindClusters) at resolution 1.0.

6. Differential Expression
Marker genes identified using:
r
FindMarkers()
FindAllMarkers(only.pos = TRUE)

7. Cell Type Annotation
Automated annotation performed using:

SingleR

HumanPrimaryCellAtlasData reference

8. Gene Expression Visualization
Violin plots generated for cancer‑relevant genes such as:

CEACAM5, DUSP6, PARP1/2/4, AGR2, AIM2, HMMR, KIT, MKI67, MUC1, NES, NGFR

Growth factor receptors: EGFR, PDGFR, VEGFR2

MAPK pathway genes: ERK1, ERK2

- Key Results
Throughput Comparison: Low vs High
Because both datasets originated from the same patient, differences in results reflect technical throughput, not biological variation.

Low‑throughput (750 cells):
Fewer detectable clusters

Higher noise in QC metrics

Weaker marker gene separation

Less confident cell type annotation

High‑throughput (7,500 cells):
15 well‑defined clusters

Stronger separation in UMAP space

More reliable differential expression

Clearer tumor vs microenvironment distinctions

Higher confidence in SingleR annotations

- Biological Interpretation
The high‑throughput dataset revealed richer tumor heterogeneity, including proliferative subpopulations (MKI67+), epithelial tumor clusters, and immune infiltrates.
The low‑throughput dataset captured the same broad cell types but with reduced clarity and fewer detectable rare populations.

This comparison reinforces a key principle in single‑cell genomics:
Higher throughput improves cluster resolution, marker detection, and biological interpretability — even when samples come from the same patient.

 Reproducibility
To reproduce this analysis:

Install required R packages:

r
install.packages(c("Seurat", "dplyr", "patchwork"))
BiocManager::install(c("SingleCellExperiment", "SingleR", "celldex"))
Download the 10x .h5 matrices.

Run the R Markdown script:
r
rmarkdown::render("final_project_BMS690.Rmd")

Skills Demonstrated
scRNA‑seq preprocessing and QC

Dimensionality reduction (PCA, UMAP)

Graph‑based clustering

Differential expression analysis

Automated cell type annotation

Cancer genomics interpretation

Data visualization in R

Reproducible workflow design

Future Improvements
Integrate DoubletFinder for doublet detection

Perform trajectory inference (Monocle3 or Slingshot)

Add copy number variation (CNV) inference (inferCNV)


📫 Contact
If you’d like to discuss this project or collaborate on computational biology research, feel free to reach out.
