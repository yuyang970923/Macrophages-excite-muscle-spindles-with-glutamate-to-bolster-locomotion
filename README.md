The following scripts were use for data analysis of bulk RNA seq datasets and single cell/nucleus RNA seq datasets analysis in the manuscript.

#For bulk RNA sequencing data analysis (both from laser capture microdissection and FACS-sorted macrophages).

Laser-capture micro-dissected muscle tissues or macrophages sorted from muscles, hearts and lungs were processed for RNA extraction.
SNMP RNA seq datasets (Fastq) were extracted from a published dataset GSE144708 and were processed with the same pipeline as the FACS-sorted macrophages from muscles, heart and lung.
Sequences were demultiplexed and adapters trimmed with `bcl2fastq-v2.20 (Illumina).
Read quality controls were carried out using FastQC-v0.11.9, trimming reads less than Phred33 quality score 20 and removing remaining adapters with Trim-Galore (v0.6.6).
RNA-seq analysis was run using the COMBINE lab’s Salmon-DESeq2 pipeline.
Salmon-v1.6.0 was used in mapping-based mode to quantify read sets.
Reads were mapped to the M25 GENCODE reference mouse genome. 
Salmon’s output files were imported and converted by Tximeta (v1.12.4) for DESeq2.
Differential expression analysis was performed using DESeq2 (v1.34.0) in R (v4.1.2).
Normalised counts were generated using the median of ratios method in DESeq2.

#For single cell/nucleus RNA sequencing data analysis of sorted muscle macrophages/DRG neuronal nuclei.

The library of MSMP or DRG was sequenced by Illumina NovaSeq 6000 platform.
Samples were de-multiplexed into FASTQ reads and then aligned to the mouse GRCm39 genome reference.
Sample de-multiplexing, sequence alignment, barcode processing and single cell 3’ unique molecular identifier (UMI) counting were performed by using Cell Ranger Software Suite (v7.1.0).
Seurat objects for each sample were created by converting the count matrix and performing initial quality control.
Cells were filtered based on thresholds for read counts (> 500), gene features (> 250), and mitochondrial content (< 15%).
Genes expressed in less than 10 cells were filtered out. Doublets were removed from the dataset by DoubletFinder package (doublet formation rate was set as 7.5%).
The filtered datasets were normalised by using SCTransform.
The count matrices from different samples were merged into a single Seurat object. 
The analysis then progressed to perform data integration using Seurat (v4) integration function. Anchors were identified for dataset integration, and hierarchical clustering is utilized to perform dimensionality reduction.
Principal component analysis (PCA) and uniform manifold approximation and projection (UMAP) were employed for dimensionality reduction and visualization.
After PCA, 40 principal components were selected for cell clustering.
Clusters were defined based on a chosen resolution, and the resulting cell clusters were visualized through UMAP plots.
Seurat FindAllMarkers function enabled the identification of marker genes associated with specific cell clusters.
Genes that were differentially expressed in each cell cluster between two conditions were identified by using the Seurat FindMarkers function with the MAST test. 
