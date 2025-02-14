# A continually expanding collection of scRNA-seq tools

Tools in each section are being resorted newest on top (previously, alphabetically). Check [other bioinformatics resources](https://github.com/mdozmorov/Bioinformatics_notes) and [collections of links to various resources](https://github.com/mdozmorov/MDmisc_notes). Issues with suggestions and pull requests are welcome!

- `[R_packages_for_scRNA-seq.pdf](R_packages_for_scRNA-seq.pdf)` - Bioconductor software packages for single-cell analysis. From [Amezquita et al., “Orchestrating Single-Cell Analysis with Bioconductor.”](https://www.biorxiv.org/content/10.1101/590562v1)

# Table of content

* [Preprocessing pipelines](#preprocessing-pipelines)
  * [scATAC-seq](#scatac-seq)
* [Quality control](#quality-control)
* [Normalization](#normalization)
* [Batch effect, merging](#batch-effect--merging)
* [Imputation](#imputation)
* [Dimensionality reduction](#dimensionality-reduction)
* [Clustering and visualization](#clustering-and-visualization)
  * [Spatial inference](#spatial-inference)
  * [Time, trajectory inference](#time-trajectory-inference)
  * [Networks](#networks)
* [Differential expression](#differential-expression)
* [Annotation](#annotation)
* [Simulation](#simulation)
  * [Power](#power)
* [scATAC-seq](#scatac-seq)
* [10X Genomics](#10x-genomics)
  * [QC](#10x-qc)
* [Data](#data)
  * [Human](#human)
  * [Mouse](#mouse)
  * [Brain single-cell data](#Brain-single-cell-data)
* [Links and other resources](#links)
  * [Papers](#papers)

## Preprocessing pipelines

- `PyMINEr` - Python-based scRNA-seq processing pipeline. Cell type identification, detection of cell type-enriched genes, pathway analysis, co-expression networks and graph theory approaches to interpreting gene expression. Notes on methods: modified K++ clustering, automatic detection of the number of cell types, co-expression and PPI networks. Input: .txt or .hdf5 files. Detailed analysis of several pancreatic datasets. https://www.sciencescott.com/pyminer
    - Tyler, Scott R., Pavana G. Rotti, Xingshen Sun, Yaling Yi, Weiliang Xie, Michael C. Winter, Miles J. Flamme-Wiese, et al. “PyMINEr Finds Gene and Autocrine-Paracrine Networks from Human Islet ScRNA-Seq.” Cell Reports 26, no. 7 (February 2019): 1951-1964.e8. https://doi.org/10.1016/j.celrep.2019.01.063.

- `zUMIs` - scRNA-seq processing pipeline that handles barcodes and summarizes  UMIs using exonic or exonic + intronic mapped reads (improves clustering, DE detection). Adaptive downsampling of oversequenced libraries. STAR aligner, Rsubread::featureCounts counting UMIs in exons and introns. https://github.com/sdparekh/zUMIs
    - Parekh, Swati, Christoph Ziegenhain, Beate Vieth, Wolfgang Enard, and Ines Hellmann. “ZUMIs - A Fast and Flexible Pipeline to Process RNA Sequencing Data with UMIs.” GigaScience 7, no. 6 (01 2018). https://doi.org/10.1093/gigascience/giy059.

- `bigSCale` - scalable analytical framework to analyze large scRNA-seq datasets, UMIs or counts. Pre-clustering, convolution into iCells, final clustering, differential expression, biomarkers.Correlation metric for scRNA-seq data based on converting expression to Z-scores of differential expression. Robust to dropouts. Matlab implementation https://github.com/iaconogi/bigSCale, and data, 1847 human neuronal progenitor cells, https://www.ncbi.nlm.nih.gov/geo/query/acc.cgi?acc=GSE102934
    - Iacono, Giovanni, Elisabetta Mereu, Amy Guillaumet-Adkins, Roser Corominas, Ivon Cuscó, Gustavo Rodríguez-Esteban, Marta Gut, Luis Alberto Pérez-Jurado, Ivo Gut, and Holger Heyn. “BigSCale: An Analytical Framework for Big-Scale Single-Cell Data.” Genome Research 28, no. 6 (June 2018): 878–90. https://doi.org/10.1101/gr.230771.117.

- `MAESTRO` - Model-based AnalysEs of Single-cell Transcriptome and RegulOme - a comprehensive single-cell RNA-seq and ATAC-seq analysis suit built using snakemake. https://github.com/liulab-dfci/MAESTRO

- `Scanpy` - Python-based pipeline for preprocessing, visualization, clustering, pseudotime and trajectory inference, differential expression and network simulation. https://github.com/theislab/scanpy
    - Wolf, F. Alexander, Philipp Angerer, and Fabian J. Theis. “SCANPY: Large-Scale Single-Cell Gene Expression Data Analysis.” Genome Biology 19, no. 1 (06 2018): 15. https://doi.org/10.1186/s13059-017-1382-0.

- `SEQC` - Single-Cell Sequencing Quality Control and Processing Software, a general purpose method to build a count matrix from single cell sequencing reads, able to process data from inDrop, drop-seq, 10X, and Mars-Seq2 technologies. https://github.com/ambrosejcarr/seqc
    - Azizi, Elham, Ambrose J. Carr, George Plitas, Andrew E. Cornish, Catherine Konopacki, Sandhya Prabhakaran, Juozas Nainys, et al. “Single-Cell Map of Diverse Immune Phenotypes in the Breast Tumor Microenvironment.” Cell, June 2018. https://doi.org/10.1016/j.cell.2018.05.060.

- `CALISTA` - clustering, lineage reconstruction, transition gene identification, and cell pseudotime single cell transcriptional analysis. Analyses can be all or separate. Uses a likelihood-based approach based on probabilistic models of stochastic gene transcriptional bursts and random technical dropout events, so all analyses are compatible with each other. Input - a matrix of normalized, batch-removed log(RPKM) or log(TPM) or scaled UMIs. Methods detail statistical methodology. Matlab and R version,  https://github.com/CABSEL/CALISTA
    - Papili Gao, Nan, Thomas Hartmann, Tao Fang, and Rudiyanto Gunawan. “CALISTA: Clustering And Lineage Inference in Single-Cell Transcriptional Analysis.” BioRxiv, January 1, 2018, 257550. https://doi.org/10.1101/257550.

- `scPipe` - A preprocessing pipeline for single cell RNA-seq data that starts from the fastq files and produces a gene count matrix with associated quality control information. It can process fastq data generated by CEL-seq, MARS-seq, Drop-seq, Chromium 10x and SMART-seq protocols. Modular, can swap tools like use different aligners. https://bioconductor.org/packages/release/bioc/html/scPipe.html
    - Tian et al. "scPipe: A flexible R/Bioconductor preprocessing pipeline for single-cell RNA-sequencing data" https://doi.org/10.1371/journal.pcbi.1006361 PLOS Computational Biology, 2018. https://doi.org/10.1371/journal.pcbi.1006361

- `Granatum` - web-based scRNA-seq analysis. list of modules, including plate merging and batch-effect removal, outlier-sample removal, gene-expression normalization, imputation, gene filtering, cell clustering, differential gene expression analysis, pathway/ontology enrichment analysis, protein network interaction visualization, and pseudo-time cell series reconstruction. http://garmiregroup.org/granatum/app, http://ilab.hawaii.edu:8111/
    - Zhu, Xun, Thomas K. Wolfgruber, Austin Tasato, Cédric Arisdakessian, David G. Garmire, and Lana X. Garmire. “Granatum: A Graphical Single-Cell RNA-Seq Analysis Pipeline for Genomics Scientists.” Genome Medicine 9, no. 1 (December 2017). https://doi.org/10.1186/s13073-017-0492-3.

- `singleCellTK` - R/Shiny package for an interactive scRNA-Seq analysis. Input, raw counts in SingleCellExperiment. Analysis: filtering raw results, clustering, batch correction, differential expression, pathway enrichment, and scRNA-Seq study design. https://compbiomed.github.io/sctk_docs/articles/v01-Introduction_to_singleCellTK.html

- STAR alignment parameters: `–outFilterType BySJout, –outFilterMultimapNmax 100, –limitOutSJcollapsed 2000000 –alignSJDBoverhangMin 8, –outFilterMismatchNoverLmax 0.04, –alignIntronMin 20, –alignIntronMax 1000000, –readFilesIn fastqrecords, –outSAMprimaryFlag AllBestScore, –outSAMtype BAM Unsorted`. From Azizi et al., “Single-Cell Map of Diverse Immune Phenotypes in the Breast Tumor Microenvironment.”

### scATAC-seq

- `SnapATAC` - Single Nucleus Analysis Package for ATAC-seq, Python and R. https://github.com/r3fang/SnapATAC

## Quality control

- `celloline` - A pipeline to remove low quality single cell files. Figure 2 - 20 biological and technical features used for filtering. High mitochondrial genes = broken cells. https://github.com/Teichlab/celloline
    - Ilicic, Tomislav, Jong Kyoung Kim, Aleksandra A. Kolodziejczyk, Frederik Otzen Bagger, Davis James McCarthy, John C. Marioni, and Sarah A. Teichmann. “Classification of Low Quality Cells from Single-Cell RNA-Seq Data.” Genome Biology 17 (February 17, 2016): 29. https://doi.org/10.1186/s13059-016-0888-1.

- `scater` - A collection of tools for doing various analyses of single-cell RNA-seq gene expression data, with a focus on quality control. https://bioconductor.org/packages/release/bioc/html/scater.html
    - McCarthy et al. "Scater: pre-processing, quality control, normalisation and visualisation of single-cell RNA-seq data in R." Bioinformatics, 2017. https://doi.org/10.1093/bioinformatics/btw777

- `DropletUtils` - Provides a number of utility functions for handling single-cell (RNA-seq) data from droplet technologies such as 10X Genomics. This includes data loading, identification of cells from empty droplets, removal of barcode-swapped pseudo-cells, and downsampling of the count matrix. https://bioconductor.org/packages/release/bioc/html/DropletUtils.html

- `scrublet` - Detect doublets in single-cell RNA-seq data, https://github.com/AllonKleinLab/scrublet
    - Wolock, Samuel L, Romain Lopez, and Allon M Klein. “Scrublet: Computational Identification of Cell Doublets in Single-Cell Transcriptomic Data.” Preprint. Bioinformatics, July 9, 2018. https://doi.org/10.1101/357368.


## Normalization

- `SCnorm` - normalization for single-cell data. Quantile regression to estimate the dependence of transcript expression on sequencing depth for every gene. Genes with similar dependence are then grouped, and a second quantile regression is used to estimate scale factors within each group. Within-group adjustment for sequencing depth is then performed using the estimated scale factors to provide normalized estimates of expression. Good statistical methods description. https://www.biostat.wisc.edu/~kendzior/SCNORM/
    - Bacher, Rhonda, Li-Fang Chu, Ning Leng, Audrey P Gasch, James A Thomson, Ron M Stewart, Michael Newton, and Christina Kendziorski. “SCnorm: Robust Normalization of Single-Cell RNA-Seq Data.” Nature Methods 14, no. 6 (April 17, 2017): 584–86. https://doi.org/10.1038/nmeth.4263.


## Batch effect, merging

- `BERMUDA` - Batch Effect ReMoval Using Deep Autoencoders, for scRNA-seq data. Requires batches to share at least one common cell type. Five step framework: 1) preprocessing, 2) clustering of cells in each batch individually, 3) identifying similar cell clusters across different batches, 4) removing batch effect by training an autoencoder, 5) further analysis of batch-corrected data. Tested on simulated (splatter) and experimental (10X genomics) data.https://github.com/txWang/BERMUDA
    - Wang, Tongxin, Travis S. Johnson, Wei Shao, Zixiao Lu, Bryan R. Helm, Jie Zhang, and Kun Huang. “BERMUDA: A Novel Deep Transfer Learning Method for Single-Cell RNA Sequencing Batch Correction Reveals Hidden High-Resolution Cellular Subtypes.” Genome Biology 20, no. 1 (December 2019). https://doi.org/10.1186/s13059-019-1764-6.

- `conos` - joint analysis of scRNA-seq datasets through inter-sample mapping (mutual nearest-neighbor mapping) and constructing a joint graph. Analysis scripts: http://pklab.med.harvard.edu/peterk/conos/, R package:  https://github.com/hms-dbmi/conos
    - Barkas, Nikolas, Viktor Petukhov, Daria Nikolaeva, Yaroslav Lozinsky, Samuel Demharter, Konstantin Khodosevich, and Peter V. Kharchenko. “Joint Analysis of Heterogeneous Single-Cell RNA-Seq Dataset Collections.” Nature Methods, July 15, 2019. https://doi.org/10.1038/s41592-019-0466-z.

- `LIGER` - R package for integrating and analyzing multiple single-cell datasets, across conditions, technologies (scRNA-seq and methylation), or species (human and mouse). Integrative nonnegative matrix factorization (W and H matrices), dataset-specific and shared patterns (metagenes, matrix H). Graphs of factor loadings onto these patterns (shared factor neighborhood graph), then comparing patterns. Alignment and agreement metrics to assess performance, LIGER outperforms Seurat on agreement. Analysis of published blood cells, brain. Human/mouse brain data at https://www.ncbi.nlm.nih.gov/geo/query/acc.cgi?acc=GSE126836.   https://github.com/MacoskoLab/liger
    - Welch, Joshua D., Velina Kozareva, Ashley Ferreira, Charles Vanderburg, Carly Martin, and Evan Z. Macosko. “Single-Cell Multi-Omic Integration Compares and Contrasts Features of Brain Cell Identity.” Cell 177, no. 7 (June 13, 2019): 1873-1887.e17. https://doi.org/10.1016/j.cell.2019.05.006.

- `scMerge` - R package for batch effect removal and normalizing of multipe scRNA-seq datasets. fastRUVIII batch removal method. Tested on 14 datasets, compared with scran, MNN, ComBat, Seurat, ZINB-WaVE using Silhouette, ARI - better separation of clusters, pseudotime reconstruction. https://github.com/SydneyBioX/scMerge/
    - Lin, Yingxin, Shila Ghazanfar, Kevin Wang, Johann A. Gagnon-Bartsch, Kitty K. Lo, Xianbin Su, Ze-Guang Han, et al. “ScMerge: Integration of Multiple Single-Cell Transcriptomics Datasets Leveraging Stable Expression and Pseudo-Replication,” September 12, 2018. https://doi.org/10.1101/393280.

- `MNN` - mutual nearest neighbors method for single-cell batch correction. Assumptions: MNN exist between batches, batch is orthogonal to the biology. Cosine normalization, Euclidean distance, a pair-specific barch-correction vector as a vector difference between the expression profiles of the paired cells using selected genes of interest and hypervariable genes. Supplementary note 5 - algorithm. mnnCorrect function in the scran package https://bioconductor.org/packages/release/bioc/html/scran.html. Code for paper https://github.com/MarioniLab/MNN2017/
    - Haghverdi, Laleh, Aaron T L Lun, Michael D Morgan, and John C Marioni. “Batch Effects in Single-Cell RNA-Sequencing Data Are Corrected by Matching Mutual Nearest Neighbors.” Nature Biotechnology, April 2, 2018. https://doi.org/10.1038/nbt.4091.

- `scLVM` - a modelling framework for single-cell RNA-seq data that can be used to dissect the observed heterogeneity into different sources and remove the variation explained by latent variables. Can correct for the cell cycle effect. Applied to naive T cells differentiating into TH2 cells. https://github.com/PMBio/scLVM
    - Buettner, Florian, Kedar N Natarajan, F Paolo Casale, Valentina Proserpio, Antonio Scialdone, Fabian J Theis, Sarah A Teichmann, John C Marioni, and Oliver Stegle. “Computational Analysis of Cell-to-Cell Heterogeneity in Single-Cell RNA-Sequencing Data Reveals Hidden Subpopulations of Cells.” Nature Biotechnology 33, no. 2 (March 2015): 155–60. https://doi.org/10.1038/nbt.3102.
    - Buettner, Florian, Naruemon Pratanwanich, Davis J. McCarthy, John C. Marioni, and Oliver Stegle. “F-ScLVM: Scalable and Versatile Factor Analysis for Single-Cell RNA-Seq.” Genome Biology 18, no. 1 (December 2017). https://doi.org/10.1186/s13059-017-1334-8. - f-scLVM - factorial single-cell latent variable model guided by pathway annotations to infer interpretable factors behind heterogeneity. PCA components are annotated by correlated genes and their enrichment in pathways. Docomposition of the original gene expression matrix to a sum of annotated, unannotated, and confounding components. Applied to their own naive T to TH2 cells, mESCs, reanalyzed 3005 neuronal cells. Simulated data. https://github.com/bioFAM/slalom

## Imputation

- `DCA` - A deep count autoencoder network to denoise scRNA-seq data. Zero-inflated negative binomial model. Current approaches - scimpute, MAGIC, SAVER. Benchmarking by increased correlation between bulk and scRNA-seq data, between protein and RNA levels, between key regulatory genes, better DE concordance in bulk and scRNA-seq, improved clustering, https://github.com/theislab/dca
    - Eraslan, Gökcen, Lukas M. Simon, Maria Mircea, Nikola S. Mueller, and Fabian J. Theis. “Single Cell RNA-Seq Denoising Using a Deep Count Autoencoder,” April 13, 2018. https://doi.org/10.1101/300681. 

- `ENHANCE`, an algorithm that denoises single-cell RNA-Seq data by first performing nearest-neighbor aggregation and then inferring expression levels from principal components. Variance-stabilizing normalization of the data before PCA. Implements its own simulation procedure for simulating sampling noise. Outperforms MAGIC, SAVER, ALRA. Python: https://github.com/yanailab/enhance, and R implementation: https://github.com/yanailab/enhance-R
    - Wagner, Florian, Dalia Barkley, and Itai Yanai. “ENHANCE: Accurate Denoising of Single-Cell RNA-Seq Data.” Preprint. Bioinformatics, June 3, 2019. https://doi.org/10.1101/655365.

- `kNN-smoothing` of scRNA-seq data, aggregates information from similar cells, improves signal-to-noise ratio. Based on observation that gene expression in technical replicates are Poisson distributed. Freeman-Tukey transform to minimize variability of low expressed genes. Tested using real and simulated data. Improves clustering, PCA, Selection of k is critical, discussed.https://github.com/yanailab/knn-smoothing
    - Wagner, Florian, Yun Yan, and Itai Yanai. “K-Nearest Neighbor Smoothing for High-Throughput Single-Cell RNA-Seq Data.” BioRxiv, April 9, 2018. https://doi.org/10.1101/217737.

- `LATE` (Learning with AuToEncoder) to imputescRNA-seq data. `TRANSLATE` (TRANSfer learning with LATE) uses reference (sc)RNA-seq dataset to learn initial parameter estimates. TensorFlow implementation for GPU and CPU. ReLu as an activation function. Various optimization techniques. Comparison with MAGIC, scVI, DCA, SAVER. Links to data. https://github.com/audreyqyfu/LATE 
    - Badsha, Md. Bahadur, Rui Li, Boxiang Liu, Yang I. Li, Min Xian, Nicholas E. Banovich, and Audrey Qiuyan Fu. “Imputation of Single-Cell Gene Expression with an Autoencoder Neural Network.” BioRxiv, January 1, 2018, 504977. https://doi.org/10.1101/504977.

- `MAGIC` - Markov Affinity-based Graph Imputation of Cells. Only ~5-15% of scRNA-seq data is non-zero, the rest are drop-outs. Use the diffusion operator to discover the manifold structure and impute gene expression. Detailed methods description. In real (bone marrow and retinal bipolar cells) and synthetic datasets, Imputed scRNA-seq data clustered better, enhances gene interactions, restores expression of known surface markers, trajectories. scRNA-seq data is preprocessed by library size normalization and PCA (to retain 70% of variability). Comparison with SVD-based low-rank data approximation (LDA) and Nuclear-Norm-based Matrix Completion (NNMC). https://github.com/KrishnaswamyLab/MAGIC, https://cran.r-project.org/web/packages/Rmagic/index.html
    - Dijk, David van, Juozas Nainys, Roshan Sharma, Pooja Kathail, Ambrose J Carr, Kevin R Moon, Linas Mazutis, Guy Wolf, Smita Krishnaswamy, and Dana Pe’er. “MAGIC: A Diffusion-Based Imputation Method Reveals Gene-Gene Interactions in Single-Cell RNA-Sequencing Data,” February 25, 2017. https://doi.org/10.1101/111591.

- `scimpute` - imputation of scRNA-seq data. Methodology: 1) Determine K subpopulations using PCA, remove outliers; 2) Mixture model of gene i in subpopulation k as gamma and normal distributions, estimate dropout probability d; 3) Impute dropout values by splitting the subpopulation into A (dropout larger than threshold t) and B (smaller). Information from B is used to impute A. Better than MAGIC, SAVER. https://github.com/Vivianstats/scImpute
    - Li, Wei Vivian, and Jingyi Jessica Li. “An Accurate and Robust Imputation Method ScImpute for Single-Cell RNA-Seq Data.” Nature Communications 9, no. 1 (08 2018): 997. https://doi.org/10.1038/s41467-018-03405-7.

- `scHinter` - imputation for small-size scRNA-seq datasets. Three modules: voting-based ensemble distance for learning cell-cell similarity, a SMOTE-based random interpolation module for imputing dropout events, and a hierarchical model for multi-layer random interpolation.  https://github.com/BMILAB/scHinter, [RNA-seq blog](https://www.rna-seqblog.com/schinter-imputing-dropout-events-for-single-cell-rna-seq-data-with-limited-sample-size/)
    - Ye, Pengchao, Wenbin Ye, Congting Ye, Shuchao Li, Lishan Ye, Guoli Ji, and Xiaohui Wu. “ScHinter: Imputing Dropout Events for Single-Cell RNA-Seq Data with Limited Sample Size.” Edited by Inanc Birol. Bioinformatics, August 8, 2019. https://doi.org/10.1093/bioinformatics/btz627.

- `scRMD` - dropout imputation in scRNA-seq via robust matrix decomposition into true expression matrix (further decomposed into a matrix of means and gene's random deviation from its mean) minus dropout matrix plus error matrix. A function to estimate the matrix of means and dropouts. Comparison with MAGIC, scImpute. https://github.com/ChongC1990/scRMD
    - Chen, Chong, Changjing Wu, Linjie Wu, Yishu Wang, Minghua Deng, and Ruibin Xi. “ScRMD: Imputation for Single Cell RNA-Seq Data via Robust Matrix Decomposition,” November 4, 2018. https://doi.org/10.1101/459404.


## Dimensionality reduction

- `CIDR` - Clustering through Imputation and Dimensionality Reduction. Impute dropouts. Explicitly deconvolve Euclidean distance into distance driven by complete, partially complete, and dropout pairs. Principal Coordinate Analysis. https://github.com/VCCRI/CIDR
    - Lin, Peijie, Michael Troup, and Joshua W. K. Ho. “CIDR: Ultrafast and Accurate Clustering through Imputation for Single-Cell RNA-Seq Data.” Genome Biology 18, no. 1 (December 2017). https://doi.org/10.1186/s13059-017-1188-0.

- `RobustAutoencoder` - Autoencoder and robust PCA for gene expression representation, robust to outliers. Main idea - split the input data X into two parts, L (reconstructed data) and S (outliers and noise). Grouped "l2,1" norm - an l2 regularizer within a group and then an l1 regularizer between groups. Iterative procedure to obtain L and S. TensorFlow implementation. https://github.com/zc8340311/RobustAutoencoder
    - Zhou, Chong, and Randy C. Paffenroth. “Anomaly Detection with Robust Deep Autoencoders.” In Proceedings of the 23rd ACM SIGKDD International Conference on Knowledge Discovery and Data Mining  - KDD ’17, 665–74. Halifax, NS, Canada: ACM Press, 2017. https://doi.org/10.1145/3097983.3098052. 

- SAUCIE - deep neural network with regularization on layers to improve interpretability. Denoising, batch removal, imputation, visualization of low-dimensional representation. Extensive comparison on simulated and real data. https://github.com/KrishnaswamyLab/SAUCIE
    - Amodio, Matthew, David van Dijk, Krishnan Srinivasan, William S Chen, Hussein Mohsen, Kevin R Moon, Allison Campbell, et al. “Exploring Single-Cell Data with Deep Multitasking Neural Networks,” August 27, 2018. https://doi.org/10.1101/237065.

- `ZIFA` - Zero-inflated dimensionality reduction algorithm for single-cell data. Single-cell dimensionality reduction. Model dropout rate as double exponential, give less weights to these counts. EM algorithm that incorporates imputation step for the expected gene expression level of drop-outs. https://github.com/epierson9/ZIFA
    - Pierson, Emma, and Christopher Yau. “ZIFA: Dimensionality Reduction for Zero-Inflated Single-Cell Gene Expression Analysis.” Genome Biology 16 (November 2, 2015): 241. https://doi.org/10.1186/s13059-015-0805-z.

- `ZINB-WAVE` - Zero-inflated negative binomial model for normalization, batch removal, and dimensionality reduction. Extends the RUV model with more careful definition of "unwanted" variation as it may be biological. Good statistical derivations in Methods. Refs to real and simulated scRNA-seq datasets. https://bioconductor.org/packages/release/bioc/html/zinbwave.html
    - Risso, Davide, Fanny Perraudeau, Svetlana Gribkova, Sandrine Dudoit, and Jean-Philippe Vert. “ZINB-WaVE: A General and Flexible Method for Signal Extraction from Single-Cell RNA-Seq Data.” BioRxiv, January 1, 2017. https://doi.org/10.1101/125112.

- `UMAP` (Uniform Manifold Approximation and Projection) - dimensionality reduction using machine learning. Detailed statistical framework. Compared with t-SNE, better preserves global structure. http://github.com/lmcinnes/umap. R implementation: https://github.com/jlmelville/uwot
    - McInnes, Leland, and John Healy. “UMAP: Uniform Manifold Approximation and Projection for Dimension Reduction.” ArXiv:1802.03426 [Cs, Stat], February 9, 2018. http://arxiv.org/abs/1802.03426.

- `VASC` - deep variational autoencoder for scRNA-seq data for dimensionality reduction and visualization. Tested on twenty datasets vs PCA, tSNE, ZIFA, and SIMLR. Four metrics to assess clustering performance: NMI (normalized mutual information score), ARI (adjusted rand index), HOM (homogeneity) and COM (completeness). No filtering, only log transformation. Keras implementation. Datasets https://hemberg-lab.github.io/scRNA.seq.datasets/, and the code https://github.com/wang-research/VASC
    - Wang, Dongfang, and Jin Gu. “VASC: Dimension Reduction and Visualization of Single Cell RNA Sequencing Data by Deep Variational Autoencoder,” October 6, 2017. https://doi.org/10.1101/199315.


## Clustering and visualization

- `BAMM-SC` - scRNA-seq clustering. A Bayesian hierarchical Dirichlet multinomial mixture model, accounts for batch effect, operates on raw counts. Outperforms K-means, TSCAN, Seurat corrected for batch using MNN or CCA in simulated and experimental settings. https://github.com/CHPGenetics/BAMMSC
    - Sun, Zhe, Li Chen, Hongyi Xin, Yale Jiang, Qianhui Huang, Anthony R. Cillo, Tracy Tabib, et al. “A Bayesian Mixture Model for Clustering Droplet-Based Single-Cell Transcriptomic Data from Population Studies.” Nature Communications 10, no. 1 (December 2019): 1649. https://doi.org/10.1038/s41467-019-09639-3.

- `Bisquit` - a Bayesian clustering and normalization method. https://github.com/sandhya212/BISCUIT_SingleCell_IMM_ICML_2016
    - Azizi, Elham, Ambrose J. Carr, George Plitas, Andrew E. Cornish, Catherine Konopacki, Sandhya Prabhakaran, Juozas Nainys, et al. “Single-Cell Map of Diverse Immune Phenotypes in the Breast Tumor Microenvironment.” Cell, June 2018. https://doi.org/10.1016/j.cell.2018.05.060.

- `celda` - CEllular Latent Dirichlet Allocation. Simultaneous clustering of cells into subpopulations and genes into transcriptional states. https://github.com/compbiomed/celda. Tutorials will be at https://github.com/compbiomed/celda_tutorials. No preprint yet.

- `cellxgene` - An interactive explorer for single-cell transcriptomics data. https://chanzuckerberg.github.io/cellxgene/, https://github.com/chanzuckerberg/cellxgene

- `Cerebro` - interactive scRNA-seq visualization from a Seurat object (v2 or 3), dimensionality reduction, clustering, identification and visualization of marker genes, enriched pathways (EnrichR), signatures (MSigDb),  expression of individual genes. cerebroPrepare R package saves the Seurat object (https://github.com/romanhaa/cerebroPrepare), to be visualized with cerebroApp Shiny app (https://github.com/romanhaa/cerebroApp). Standalone and Docker versions are available. Main repo:https://github.com/romanhaa/Cerebro
    - Hillje, Roman, Pier Giuseppe Pelicci, and Lucilla Luzi. “Cerebro: Interactive Visualization of ScRNA-Seq Data.” Preprint. Bioinformatics, May 8, 2019. https://doi.org/10.1101/631705.

- `CIDR` - Clustering through Imputation and Dimensionality Reduction. Impute dropouts. Explicitly deconvolve Euclidean distance into distance driven by complete, partially complete, and dropout pairs. Principal Coordinate Analysis. https://github.com/VCCRI/CIDR
    - Lin, Peijie, Michael Troup, and Joshua W. K. Ho. “CIDR: Ultrafast and Accurate Clustering through Imputation for Single-Cell RNA-Seq Data.” Genome Biology 18, no. 1 (December 2017). https://doi.org/10.1186/s13059-017-1188-0.

- `clusterExperiment` R package for scRNA-seq data visualization. Resampling-based Sequential Ensemble Clustering (RSEC) method. clusterMany - makeConsensus - makeDendrogram - mergeClusters pipeline. Biomarker detection by differential expression analysis between clusters. Visualization as heatmaps, https://bioconductor.org/packages/release/bioc/html/clusterExperiment.html
    - Risso, Davide, Liam Purvis, Russell B. Fletcher, Diya Das, John Ngai, Sandrine Dudoit, and Elizabeth Purdom. “ClusterExperiment and RSEC: A Bioconductor Package and Framework for Clustering of Single-Cell and Other Large Gene Expression Datasets.” Edited by Aaron E. Darling. PLOS Computational Biology 14, no. 9 (September 4, 2018): e1006378. https://doi.org/10.1371/journal.pcbi.1006378.

- Conos - clustering of scRNA-seq samples by joint graph construction. Seurat or pagoda2 for data preprocessing, selection of hypervariable genes, initial clustering (KNN, or dimensionality reduction), then joint clustering. R package, https://github.com/hms-dbmi/conos
    - Barkas, Nikolas, Viktor Petukhov, Daria Nikolaeva, Yaroslav Lozinsky, Samuel Demharter, Konstantin Khodosevich, and Peter V Kharchenko. “Wiring Together Large Single-Cell RNA-Seq Sample Collections.” BioRxiv, January 1, 2018. https://doi.org/10.1101/460246.

- `destiny` - R package for diffusion maps-based visualization of single-cell data. https://bioconductor.org/packages/release/bioc/html/destiny.html
    - Haghverdi, Laleh, Florian Buettner, and Fabian J. Theis. “Diffusion Maps for High-Dimensional Single-Cell Analysis of Differentiation Data.” Bioinformatics 31, no. 18 (September 15, 2015): 2989–98. https://doi.org/10.1093/bioinformatics/btv325. - Introduction of other methods, Table 1 compares them. Methods details. Performance is similar to PCA and tSNE. 

- `FIt-SNE` - accelerated version of t-SNE clustering for visualizing thousands/milions of cells. https://github.com/KlugerLab/FIt-SNE. `t-SNE-Heatmaps` - discretized t-SNE clustering representation as a heatmap. https://github.com/KlugerLab/t-SNE-Heatmaps. Detailed methods, and further stats at https://gauss.math.yale.edu/~gcl22/blog/numerics/low-rank/t-sne/2018/01/11/low-rank-kernels.html
    - Linderman, George C., Manas Rachh, Jeremy G. Hoskins, Stefan Steinerberger, and Yuval Kluger. “Fast Interpolation-Based t-SNE for Improved Visualization of Single-Cell RNA-Seq Data.” Nature Methods, February 11, 2019. https://doi.org/10.1038/s41592-018-0308-4.

- `iSEE` - Shiny app for interactive visualization of SummarizedExperiment scRNA-seq objects. https://github.com/csoneson/iSEE, https://www.rna-seqblog.com/isee-an-interactive-shiny-based-graphical-user-interface-for-exploring-data-stored-in-summarizedexperiment-objects/, https://github.com/kevinrue/iSEEWorkshop2019
    - Rue-Albrecht, Kevin, Federico Marini, Charlotte Soneson, and Aaron T.L. Lun. “ISEE: Interactive SummarizedExperiment Explorer.” F1000Research 7 (June 14, 2018): 741. https://doi.org/10.12688/f1000research.14966.1.

- `MetaCell` - partitioning scRNA-seq data into metacells - disjoint and homogeneous/compact groups of cells exhibiting only sampling variance. Most variable genes to cell-to-cell similarity matrix (PCC on  to Knn similarity graph that is partitioned by bootstrapping to obtain subgraphs. Tested on several 10X datasets, https://support.10xgenomics.com/single-cell-gene-expression/datasets. https://bitbucket.org/tanaylab/metacell/src/default/
    - Baran, Yael, Arnau Sebe-Pedros, Yaniv Lubling, Amir Giladi, Elad Chomsky, Zohar Meir, Michael Hoichman, Aviezer Lifshitz, and Amos Tanay. “MetaCell: Analysis of Single Cell RNA-Seq Data Using k-NN Graph Partitions.” BioRxiv, January 1, 2018, 437665. https://doi.org/10.1101/437665.

- `PHATE` (Potential of Heat-diffusion for Affinity-based Transition Embedding) - low-dimensional embedding, denoising, and visualization, applicable to scRNA-seq, microbiome, SNP, Hi-C (as affinity matrices) and other data. Preserves biological structures and branching better than PCA, tSNE, diffusion maps. Robust to noise and subsampling. Detailed methods description and graphical representation of the algorithm. https://github.com/KrishnaswamyLab/PHATE
    - Moon, Kevin R., David van Dijk, Zheng Wang, Scott Gigante, Daniel Burkhardt, William Chen, Antonia van den Elzen, et al. “Visualizing Transitions and Structure for Biological Data Exploration,” June 28, 2018. https://doi.org/10.1101/120378.

- `PhenoGraph` - discovers subpopulations in scRNA-seq data. High-dimensional space is modeled as a nearest-neighbor graph, then the Louvain community detection algorithm. No assumptions about the size, number, or form of subpopulations. https://github.com/jacoblevine/PhenoGraph
    - Levine, Jacob H., Erin F. Simonds, Sean C. Bendall, Kara L. Davis, El-ad D. Amir, Michelle D. Tadmor, Oren Litvin, et al. “Data-Driven Phenotypic Dissection of AML Reveals Progenitor-like Cells That Correlate with Prognosis.” Cell 162, no. 1 (July 2015): 184–97. https://doi.org/10.1016/j.cell.2015.05.047.

- `SC3` - single-cell clustering. Multiple clustering iterations, consensus matrix, then hierarhical clustering. Benchmarking against other methods. https://bioconductor.org/packages/release/bioc/html/SC3.html
    - Kiselev, Vladimir Yu, Kristina Kirschner, Michael T Schaub, Tallulah Andrews, Andrew Yiu, Tamir Chandra, Kedar N Natarajan, et al. “SC3: Consensus Clustering of Single-Cell RNA-Seq Data.” Nature Methods 14, no. 5 (March 27, 2017): 483–86. https://doi.org/10.1038/nmeth.4236.

- `scVAE` - Variational auroencoder frameworks for modelling raw RNA-seq counts, denoising the data to improve biologically plausible grouping in scRNA-seq data. Improvement in Rand index. https://github.com/chgroenbech/scVAE
    - Grønbech, Christopher Heje, Maximillian Fornitz Vording, Pascal N Timshel, Casper Kaae Sønderby, Tune Hannes Pers, and Ole Winther. “ScVAE: Variational Auto-Encoders for Single-Cell Gene Expression Data,” May 16, 2018. https://doi.org/10.1101/318295. 

- `SIMLR` - scRNA-seq dimensionality reduction, clustering, and visualization based on multiple kernel-learned distance metric. Comparison with PCA, t-SNE, ZIFA. Seven datasets. R and Matlab implementation. https://github.com/BatzoglouLabSU/SIMLR
    - Wang, Bo, Junjie Zhu, Emma Pierson, Daniele Ramazzotti, and Serafim Batzoglou. “Visualization and Analysis of Single-Cell RNA-Seq Data by Kernel-Based Similarity Learning.” Nature Methods 14, no. 4 (April 2017): 414–16. https://doi.org/10.1038/nmeth.4207.

- `SPRING` - a pipeline for data filtering, normalization and visualization using force-directed layout of k-nearest-neighbor graph. Web-based (10,000 cells max) https://kleintools.hms.harvard.edu/tools/spring.html) and GitHub https://github.com/AllonKleinLab/SPRING_dev 
    - Weinreb, Caleb, Samuel Wolock, and Allon M. Klein. “SPRING: A Kinetic Interface for Visualizing High Dimensional Single-Cell Expression Data.” Bioinformatics (Oxford, England) 34, no. 7 (April 1, 2018): 1246–48. https://doi.org/10.1093/bioinformatics/btx792.

- `SNN-Cliq` - shared nearest neighbor clustering of scRNA-seq data, represented as a graph. Similarity between two data points based on the ranking of their shared neighborhood. Automatically determine the number of clusters, accomodates different densities and shapes. Compared with K-means and DBSCAN using Purity, Adjusted Rand Indes, F1-score. Matlab, Python, R implementation. http://bioinfo.uncc.edu/SNNCliq/
    - Xu, Chen, and Zhengchang Su. “Identification of Cell Types from Single-Cell Transcriptomes Using a Novel Clustering Method.” Bioinformatics (Oxford, England) 31, no. 12 (June 15, 2015): 1974–80. https://doi.org/10.1093/bioinformatics/btv088.

- `TooManyCells` - divisive hierarchical spectral clustering of scRNA-seq data. Uses truncated singular vector decomposition to bipartition the cells. Newman-Girvain modularity Q to assess whether bipartition is significant or should be stopped. BirchBeer visualization. Outperforms Phenograph, Seurat, Cellranger, Monocle, the latter is second in performance. Excels for rare populations. Normalization marginally affects performance. https://github.com/GregorySchwartz/tooManyCellsR and  https://github.com/faryabiLab/birch-beer
    - Schwartz, Gregory W, Jelena Petrovic, Maria Fasolino, Yeqiao Zhou, Stanley Cai, Lanwei Xu, Warren S Pear, Golnaz Vahedi, and Robert B Faryabi. “TooManyCells Identifies and Visualizes Relationships of Single-Cell Clades.” BioRxiv, January 13, 2019. https://doi.org/10.1101/519660.

- `viSNE` - the Barnes-Hut implementation of the t-SNE algorithm, improved and tailored for the analysis of single-cell data. Details of tSNE https://www.denovosoftware.com/site/manual/visne.htm, and the `Rtsne` R package https://cran.r-project.org/web/packages/Rtsne/index.html
    - Amir, El-ad David, Kara L Davis, Michelle D Tadmor, Erin F Simonds, Jacob H Levine, Sean C Bendall, Daniel K Shenfeld, Smita Krishnaswamy, Garry P Nolan, and Dana Pe’er. “ViSNE Enables Visualization of High Dimensional Single-Cell Data and Reveals Phenotypic Heterogeneity of Leukemia.” Nature Biotechnology 31, no. 6 (June 2013): 545–52. https://doi.org/10.1038/nbt.2594.

- `UCSC Single Cell Browser` - Python pipeline and Javascript scatter plot library for single-cell datasets. Pre-process an expression matrix by filtering, PCA, nearest-neighbors, clustering, t-SNE and UMAP and formats them for cbBuild. Stand-alone app on GitHub, https://github.com/maximilianh/cellBrowser, Demo that includes several landmark datasets, https://cells.ucsc.edu/


### Spatial inference

- https://github.com/hms-dbmi/brainmapr - R package to infer spatial location of neuronal subpopulations within the developing mouse brain by integrating single-cell RNA-seq data with in situ RNA patterns from the Allen Developing Mouse Brain Atlas http://hms-dbmi.github.io/brainmapr/

- `Seurat` - single-cell RNA-seq for spatial cellular localization, using in situ RNA patterns as a reference. Impute landmark genes, relate them to the reference map. http://satijalab.org/seurat/. Tutorial, https://satijalab.org/seurat/pbmc3k_tutorial.html, and Dave Tang notes https://davetang.org/muse/2017/08/01/getting-started-seurat/
    - Satija, Rahul, Jeffrey A. Farrell, David Gennert, Alexander F. Schier, and Aviv Regev. “Spatial Reconstruction of Single-Cell Gene Expression Data.” Nature Biotechnology 33, no. 5 (May 2015): 495–502. https://doi.org/10.1038/nbt.3192.


### Time, trajectory inference

- A collection of 57 trajectory inference methods, https://github.com/dynverse/dynmethods#list-of-included-methods
    - Saelens, Wouter, Robrecht Cannoodt, Helena Todorov, and Yvan Saeys. “A Comparison of Single-Cell Trajectory Inference Methods: Towards More Accurate and Robust Tools,” March 5, 2018. https://doi.org/10.1101/276907. - Review of trajectory 29 inference methods for single-cell RNA-seq (out of 57 methods collected). Slingshot, TSCAN and Monocle DDRTree perform best overall. https://github.com/dynverse/dynverse

- Single-cell RNA-seq pseudotime estimation algorithms, by Anthony Gitter. References and descriptions of many algorithms. https://github.com/agitter/single-cell-pseudotime

- `cellTree` - hierarchical tree inference and visualization. Latent Dirichlet Allocation (LDA). Cells are analogous to text documents, discretized gene expression levels replace word frequencies. The LDA model represents topic distribution for each cell, analogous to low-dimensional embedding of the data where similarity is measured with chi-square distance. Fast and precise. http://bioconductor.org/packages/release/bioc/html/cellTree.html
    - duVerle, David A., Sohiya Yotsukura, Seitaro Nomura, Hiroyuki Aburatani, and Koji Tsuda. “CellTree: An R/Bioconductor Package to Infer the Hierarchical Structure of Cell Populations from Single-Cell RNA-Seq Data.” BMC Bioinformatics 17, no. 1 (December 2016). https://doi.org/10.1186/s12859-016-1175-6.

- `Monocle` - Temporal ordering of single cell gene expression profiles. Independent Component Analysis to reduce dimensionality, Minimum Spanning Tree on the reduced representation and the longest path through it. https://cole-trapnell-lab.github.io/monocle-release/
    - Trapnell, Cole, Davide Cacchiarelli, Jonna Grimsby, Prapti Pokharel, Shuqiang Li, Michael Morse, Niall J. Lennon, Kenneth J. Livak, Tarjei S. Mikkelsen, and John L. Rinn. “The Dynamics and Regulators of Cell Fate Decisions Are Revealed by Pseudotemporal Ordering of Single Cells.” Nature Biotechnology 32, no. 4 (April 2014): 381–86. https://doi.org/10.1038/nbt.2859.

- `Monocle 2` - Reversed graph embedding (DDRTree), finding low-dimensional mapping of differential genes while learning the graph in this reduced space. Allows for the selection of root. Compared with Monocle 1, Wishbone, Diffusion Pseudotime, SLICER. Code, https://github.com/cole-trapnell-lab/monocle-release, analysis, https://github.com/cole-trapnell-lab/monocle2-rge-paper
    - Qiu, Xiaojie, Qi Mao, Ying Tang, Li Wang, Raghav Chawla, Hannah A Pliner, and Cole Trapnell. “Reversed Graph Embedding Resolves Complex Single-Cell Trajectories.” Nature Methods 14, no. 10 (August 21, 2017): 979–82. https://doi.org/10.1038/nmeth.4402.

- `SCUBA` - single-cell clustering using bifurcation analysis. Cells may differentiate in a monolineage manner or may differentiate into multiple cell lineages, which is the bifurcation event - two new lineages. Methods. Matlab code https://github.com/gcyuan/SCUBA
    - Marco, Eugenio, Robert L. Karp, Guoji Guo, Paul Robson, Adam H. Hart, Lorenzo Trippa, and Guo-Cheng Yuan. “Bifurcation Analysis of Single-Cell Gene Expression Data Reveals Epigenetic Landscape.” Proceedings of the National Academy of Sciences of the United States of America 111, no. 52 (December 30, 2014): E5643-5650. https://doi.org/10.1073/pnas.1408993111.

-`Slingshot` - Inferring multiple developmental lineages from single-cell gene expression. Clustering by gene expression, then inferring cell lineage as an ordered set of clusters -minimum spanning tree through the clusters using Mahalanobis distance. Initial state and terminal state specification. Principal curves to draw a path through the gene expression space of each lineage. https://github.com/kstreet13/slingshot
    - Street, Kelly, Davide Risso, Russell B Fletcher, Diya Das, John Ngai, Nir Yosef, Elizabeth Purdom, and Sandrine Dudoit. “Slingshot: Cell Lineage and Pseudotime Inference for Single-Cell Transcriptomics.” BioRxiv, January 1, 2017. https://doi.org/10.1186/s12864-018-4772-0.

- `TSCAN` - pseudo-time reconstruction for scRNA-seq. Clustering first, then minimum spanning tree over cluster centers. Cells are projected to the tree (PCA) to determine their pseudo-time and order. Code https://github.com/zji90/tscan and R package that includes GUI http://www.bioconductor.org/packages/release/bioc/html/TSCAN.html
    - Ji, Zhicheng, and Hongkai Ji. “TSCAN: Pseudo-Time Reconstruction and Evaluation in Single-Cell RNA-Seq Analysis.” Nucleic Acids Research 44, no. 13 (27 2016): e117. https://doi.org/10.1093/nar/gkw430.

- `Wishbone` - ordering scRNA-seq along bifurcating developmental trajectories. nearest-heighbor graphs to capture developmental distances using shortest paths. Solves short-circuits by low-dimensional projection using diffusion maps. Waypoints as guides for building the trajectory. Detailed and comprehensive Methods description. Supersedes Wanderlust. Comparison with SCUBA, Monocle. https://github.com/ManuSetty/wishbone
    - Setty, Manu, Michelle D. Tadmor, Shlomit Reich-Zeliger, Omer Angel, Tomer Meir Salame, Pooja Kathail, Kristy Choi, Sean Bendall, Nir Friedman, and Dana Pe’er. “Wishbone Identifies Bifurcating Developmental Trajectories from Single-Cell Data.” Nature Biotechnology 34, no. 6 (2016): 637–45. https://doi.org/10.1038/nbt.3569.



### Networks

- `GraphDDP` - combines user-guided clustering and transition of differentiation processes between clusters. Shortcomings of PCA, MDS, t-SNE. Tested on several datasets to improve interpretability of clustering, compared with other methods (Monocle2, SPRING, TSCAN). Detailed methods. https://github.com/fabriziocosta/GraphEmbed
    - Costa, Fabrizio, Dominic Grün, and Rolf Backofen. “GraphDDP: A Graph-Embedding Approach to Detect Differentiation Pathways in Single-Cell-Data Using Prior Class Knowledge.” Nature Communications 9, no. 1 (December 2018). https://doi.org/10.1038/s41467-018-05988-7. 

- `PAGA` - graph-like representation of scRNA-seq data. The kNN graph is partitioned using Louvain community detection algorithm, discarding spurious edged (denoising). Much faster than UMAP. Part of Scanpy pipeline.https://github.com/theislab/paga
    - Wolf, F. Alexander, Fiona K. Hamey, Mireya Plass, Jordi Solana, Joakim S. Dahlin, Berthold Göttgens, Nikolaus Rajewsky, Lukas Simon, and Fabian J. Theis. “PAGA: Graph Abstraction Reconciles Clustering with Trajectory Inference through a Topology Preserving Map of Single Cells.” Genome Biology 20, no. 1 (March 19, 2019): 59. https://doi.org/10.1186/s13059-019-1663-x.

- `SCENIC` - single-cell network reconstruction and cell-state identification. Three modules: 1) GENIE3 - connect co-expressed genes and TFs using random forest regression; 2) RcisTarget - Refine them using cis-motif enrichment; 3) AUCell - assign activity scores for each network in each cell type. The R implementation of GENIE3 does not scale well with larger datasets; use arboreto instead, which is a much faster Python implementation. https://gbiomed.kuleuven.be/english/research/50000622/lcb/tools/scenic, https://github.com/aertslab/SCENIC, https://github.com/aertslab/GENIE3, https://github.com/aertslab/AUCell, https://github.com/tmoerman/arboreto, https://github.com/aertslab/pySCENIC
    - Aibar, Sara, Carmen Bravo González-Blas, Thomas Moerman, Vân Anh Huynh-Thu, Hana Imrichova, Gert Hulselmans, Florian Rambow, et al. “SCENIC: Single-Cell Regulatory Network Inference and Clustering.” Nature Methods 14, no. 11 (November 2017): 1083–86. https://doi.org/10.1038/nmeth.4463.
    - Davie et al. "A Single-Cell Transcriptome Atlas of the Aging Drosophila Brain" Cell, 2018 https://doi.org/10.1016/j.cell.2018.05.057

- `SCIRA` - infer tissue-specific regulatory networks using large-scale bulk RNA-seq, estimate regulatory activity. SEPIRA uses a greedy partial correlation framework to infer a regulatory network from GTeX data, TF-specific regulons used as target profiles in a linear regression model framework. Compared against SCENIC. Works even for small cell populations. Tested on three scRNA-seq datasets. A part of SEPIRA R package, http://bioconductor.org/packages/release/bioc/html/SEPIRA.html
    - Wang, Ning, and Andrew E Teschendorff. “Leveraging High-Powered RNA-Seq Datasets to Improve Inference of Regulatory Activity in Single-Cell RNA-Seq Data.” BioRxiv, February 22, 2019. https://doi.org/10.1101/553040.

- `SINCERA` - identification of major cell types, the corresponding gene signatures and transcription factor networks. Pre-filtering (expression filter, cell specificity filter) improves inter-sample correlation and decrease inter-sample distance. Normalization: per-sample z-score, then trimmed mean across cells. Clustering (centered Pearson for distance, average linkage), and other metrics, permutation to assess clustering significance. Functional enrichment, cell type enrichment analysis, identification of cell signatures. TF networks and their parameters (disruptive fragmentation centrality, disruptive connection centrality, disruptive distance centrality). Example analysis of mouse lung cells at E16.5, Fluidigm, 9 clusters, comparison with SNN-Cliq, scLVM, SINGuLAR Analysis Toolset. Web-site: https://research.cchmc.org/pbge/sincera.html; GitHub: https://github.com/xu-lab/SINCERA; [Data](https://lungmap.net/breath-entity-page/?entityType=none&entityId=&entityLabel=&experimentTypes[]=LMXT0000000016) 
    - Guo, Minzhe, Hui Wang, S. Steven Potter, Jeffrey A. Whitsett, and Yan Xu. “SINCERA: A Pipeline for Single-Cell RNA-Seq Profiling Analysis.” PLoS Computational Biology 11, no. 11 (November 2015): e1004575. https://doi.org/10.1371/journal.pcbi.1004575.


## Differential expression

- Soneson, Charlotte, and Mark D Robinson. “Bias, Robustness and Scalability in Single-Cell Differential Expression Analysis.” Nature Methods, February 26, 2018. https://doi.org/10.1038/nmeth.4612. - Differential analysis of scRNA-seq data, 36 methods. Prefiltering of low expressed genes is important. edgeRQLFDetRate performs best. The conquer database, scRNA-seq datasets as RDS objects - http://imlspenticton.uzh.ch:3838/conquer/


- `MAST` - scRNA-seq DEG analysis. CDR - the fraction of genes that are detectably expressed in each cell - added to the hurdle model that explicitly parameterizes distributions of expressed and non-expressed genes. Generalized linear model, log2(TPM+1), Gaussian. Regression coeffs are estimated using Bayesian approach. Variance shrinkage, gamma distribution. https://github.com/RGLab/MAST
    - Finak, Greg, Andrew McDavid, Masanao Yajima, Jingyuan Deng, Vivian Gersuk, Alex K. Shalek, Chloe K. Slichter, et al. “MAST: A Flexible Statistical Framework for Assessing Transcriptional Changes and Characterizing Heterogeneity in Single-Cell RNA Sequencing Data.” Genome Biology 16 (December 10, 2015): 278. https://doi.org/10.1186/s13059-015-0844-5.

-  `SCDE`. Stochasticity of gene expression, high drop-out rate. A mixture model of two processes - detected expression and drop-out failure modeled as low-magnitude Poisson. Drop-out rate depends on the expected expression and can be approximated by logistic regression. https://hms-dbmi.github.io/scde/index.html
    - Kharchenko, Peter V., Lev Silberstein, and David T. Scadden. “Bayesian Approach to Single-Cell Differential Expression Analysis.” Nature Methods 11, no. 7 (July 2014): 740–42. https://doi.org/10.1038/nmeth.2967.

- `scDD` R package to identify differentially expressed genes in single cell RNA-seq data. Accounts for unobserved data. Four types of differential expression (DE, DP, DM, DB, see paper). https://github.com/kdkorthauer/scDD
    - Korthauer, Keegan D., Li-Fang Chu, Michael A. Newton, Yuan Li, James Thomson, Ron Stewart, and Christina Kendziorski. “A Statistical Approach for Identifying Differential Distributions in Single-Cell RNA-Seq Experiments.” Genome Biology 17, no. 1 (December 2016). https://doi.org/10.1186/s13059-016-1077-y.


## Annotation

- `CellAssign` - R package for scRNA-seq cell type inference. Probabilistic graphical model to assign cell type probabilities to single cells using known marker genes (binarized matrix), including "unassigned" categorization. Insensitive to batch- or sample-specific effects. Outperforms Seurat, SC3, PhenoGraph, densityCut, dynamicTreeCut, scmap-cluster, correlation-based methods, SCINA. Applied to delineate the composition of the tumor microenvironment. Built using TensorFlow. https://github.com/irrationone/cellassign
    - Zhang, Allen W., Ciara O’Flanagan, Elizabeth A. Chavez, Jamie L. P. Lim, Nicholas Ceglia, Andrew McPherson, Matt Wiens, et al. “Probabilistic Cell-Type Assignment of Single-Cell RNA-Seq for Tumor Microenvironment Profiling.” Nature Methods, September 9, 2019. https://doi.org/10.1038/s41592-019-0529-1.

- `matchSCore2` - classifying cell types based on reference data. https://github.com/elimereu/matchSCore2
    - Mereu, Elisabetta, Atefeh Lafzi, Catia Moutinho, Christoph Ziegenhain, Davis J. MacCarthy, Adrian Alvarez, Eduard Batlle, et al. “Benchmarking Single-Cell RNA Sequencing Protocols for Cell Atlas Projects.” Preprint. Genomics, May 13, 2019. https://doi.org/10.1101/630087.

- `Single-Cell Signature Explorer` - gene signature (\~17,000 from MSigDb, KEGG, Reactome) scoring (sum of UMIs in in a gene signature over the total UMIs in a cell) for single cells, and visualization on top of a t-SNE plot. Optional Noise Reduction (Freeman-Tuckey transform to stabilize technical noise). Four consecutive tools (Go language, R/Shiny). Comparison with Seurat's Cell CycleScore module and AUCell from SCENIC. Very fast.https://sites.google.com/site/fredsoftwares/products/single-cell-signature-explorer
    - Pont, Frédéric, Marie Tosolini, and Jean Jacques Fournié. “Single-Cell Signature Explorer for Comprehensive Visualization of Single Cell Signatures across ScRNA-Seq Data Sets.” Preprint. Bioinformatics, April 29, 2019. https://doi.org/10.1101/621805.

- `VISION` - functional annotation of scRNA-seq data using gene signatures (Geary's C statistics), unsupervised and supervised. Operates downstream of dimensionality reduction, clustering. A continuation of FastProject. https://github.com/YosefLab/VISION
    - DeTomaso, David, Matthew Jones, Meena Subramaniam, Tal Ashuach, Chun J Ye, and Nir Yosef. “Functional Interpretation of Single-Cell Similarity Maps,” August 29, 2018. https://doi.org/10.1101/403055.

- `SingleR` - single-cell recognition of cell types by correlating (Spearman) scRNA-seq expression against reference databases. Post-Seurat analysis. Web tool, http://comphealth.ucsf.edu/SingleR/, that takes SingleR objects, instructions are on GitHub, https://github.com/dviraran/SingleR/. Example analysis: http://comphealth.ucsf.edu/sample-apps/SingleR/SingleR.MCA.html
    - Aran, Dvir, Agnieszka P. Looney, Leqian Liu, Valerie Fong, Austin Hsu, Paul J. Wolters, Adam Abate, Atul J. Butte, and Mallar Bhattacharya. “Reference-Based Annotation of Single-Cell Transcriptomes Identifies a Profibrotic Macrophage Niche after Tissue Injury.” BioRxiv, January 1, 2018, 284604. https://doi.org/10.1101/284604.


## Simulation

- `scDesign` - scRNA-seq data simulator and statistical framework to access experimental design for differential gene expression analysis. Gamma-Normal mixture model better fits scRNA-seq data, accounts for dropout events (Methods describe step-wise statistical derivations). Single- or double-batch sequencing scenarios. Comparable or superior performance to simulation methods `splat`, `powsimR`, `scDD`, Lun et al. method. DE tested using t-test. Applications include DE methods evaluation, dimensionality reduction testing. https://github.com/Vivianstats/scDesign
    - Li, Wei Vivian, and Jingyi Jessica Li. “A Statistical Simulator ScDesign for Rational ScRNA-Seq Experimental Design.” Bioinformatics 35, no. 14 (July 15, 2019): i41–50. https://doi.org/10.1093/bioinformatics/btz321.

- `Splatter` - scRNA-seq simulator and pre-defined differential expression. 6 methods, description of each. Issues with scRNA-seq data - dropouts, zero inflation, proportion of zeros, batch effect. Negative binomial for simulation. No simulation is perfect. https://github.com/Oshlack/splatter
    - Zappia, Luke, Belinda Phipson, and Alicia Oshlack. “Splatter: Simulation Of Single-Cell RNA Sequencing Data,” July 24, 2017. https://doi.org/10.1186/s13059-017-1305-0.
    
### Power

- `powsimR` - an R package for simulating scRNA-seq datasets and assess performance of differential analysis methods. Supports Poisson, Negative Binomial, and zero inflated NB, or estimates parameters from user-provided data. Simulates differential expression with pre-defined fold changes, estimates power, TPR, FDR, sample size, and for the user-provided dataset. https://github.com/bvieth/powsimR
    - Vieth, Beate, Christoph Ziegenhain, Swati Parekh, Wolfgang Enard, and Ines Hellmann. “PowsimR: Power Analysis for Bulk and Single Cell RNA-Seq Experiments.” Edited by Ivo Hofacker. Bioinformatics 33, no. 21 (November 1, 2017): 3486–88. https://doi.org/10.1093/bioinformatics/btx435.

## scATAC-seq

- Signac is an extension of Seurat for the analysis, interpretation, and exploration of single-cell chromatin datasets. https://satijalab.org/signac/



## 10X Genomics

- List of tools and resources related to the 10x Genomics GEMCode/Chromium system, https://github.com/johandahlberg/awesome-10x-genomics

- Zheng, Grace X. Y., Jessica M. Terry, Phillip Belgrader, Paul Ryvkin, Zachary W. Bent, Ryan Wilson, Solongo B. Ziraldo, et al. “Massively Parallel Digital Transcriptional Profiling of Single Cells.” Nature Communications 8 (January 16, 2017): 14049. https://doi.org/10.1038/ncomms14049. - 10X technology. Details of each wet-lab step, sequencing, and basic computational analysis. Calling SNPs from scRNA-seq data. Reduce dimensionality with PCA (50 PCs), K-means to assign cluster labels, visualizing with tSNE. Code for the paper: https://github.com/10XGenomics/single-cell-3prime-paper. scRNA-Seq dataset of 3000 peripheral blood mononuclear cells (PBMCs) from the 10X Genomics platform. https://support.10xgenomics.com/single-cell-gene-expression/datasets

- Cell Ranger, Loupe Cell Browser software download, https://support.10xgenomics.com/single-cell-gene-expression/software/downloads/latest

- Cell Ranger R kit, https://support.10xgenomics.com/single-cell-gene-expression/software/pipelines/latest/rkit

- Cellranger AWS Pipeline. https://github.com/ismms-himc/cellranger-aws-pipeline

- An R script for importing the fragments file from the CellRanger output and making a SummarizedExperiment, by Caleb Lareau. https://github.com/caleblareau/scATAC_10X_raw_to_kmers/blob/master/example_kmers.R

### 10X QC

- `bxcheck` - Toolset for QC and processing 10x genomics data. https://github.com/pd3/bxcheck

- What is sequencing saturation?. https://kb.10xgenomics.com/hc/en-us/articles/115005062366-What-is-sequencing-saturation-

## Data

- Single-cell portal, Broad Institute.  https://portals.broadinstitute.org/single_cell

- Conquer DB of scRNA-seq datasets as R MultiAssayExperiment objects: http://imlspenticton.uzh.ch:3838/conquer/

- Multiple datasets, from the 10X Genomics website, https://support.10xgenomics.com/single-cell-gene-expression/datasets

- SingleCellExperiment data, human and mouse, brain, embryo development, embryo stem cells, hematopoietic stem cells, pancreas, retina, other tissues. https://hemberg-lab.github.io/scRNA.seq.datasets/, and GitHub https://github.com/hemberg-lab/scRNA.seq.datasets

- CellBench: single cell RNA-seq benchmarking, R SingleCellExperiment object. https://github.com/LuyiTian/CellBench_data

- Multiple datasets (Human Cell Atlas, STARmap mouse visual cortex spatial transcriptomics. Tabula Muris, 10X Genomics datasets, others in STAR methods, analyzed in Seurat v3 paper. https://www.cell.com/cell/fulltext/S0092-8674(19)30559-8

- `scRNAseq` - three small scRNA-seq datasets, to play with in R. http://bioconductor.org/packages/release/data/experiment/html/scRNAseq.html

- UCSC cell browser. http://cells.ucsc.edu/

### Human

- Human Cell Atlas Preview Datasets, https://preview.data.humancellatlas.org/. Massive amount of data. An R package to access this data is being developed, https://github.com/federicomarini/HCAData

- Single Cell Immune Profiling Datasets. ~150,000 CD8+ T cells from 4 human donors across a highly multiplexed panel of 44 distinct, specific peptide–MHC (pMHC) multimers. https://support.10xgenomics.com/single-cell-vdj/datasets

- Paul, Franziska, Ya’ara Arkin, Amir Giladi, Diego Adhemar Jaitin, Ephraim Kenigsberg, Hadas Keren-Shaul, Deborah Winter, et al. “Transcriptional Heterogeneity and Lineage Commitment in Myeloid Progenitors.” Cell 163, no. 7 (December 17, 2015): 1663–77. https://doi.org/10.1016/j.cell.2015.11.013. - 3′ MARS (massively parallel RNA single-cell)-Seq protocol with shallow sequencing (1,453 genes/cell) to examine heterogeneity across bone marrow resident myeloid progenitors, 2,686 cells. Batch-corrected UMI count matrix: 19 clusters. http://compgenomics.weizmann.ac.il/tanay/?page_id=649. Seurat (PMID: 29608179) clusters (Supplementary Data 2,https://www.nature.com/articles/nbt.4096#supplementary-information). GEO: https://www.ncbi.nlm.nih.gov/geo/query/acc.cgi?acc=GSE72857
    - `Amit_2015/Supplementary_dataset_1.txt` - Cell metadata for IFNB response analysis. [Source](https://media.nature.com/original/nature-assets/nbt/journal/v36/n5/extref/nbt.4096-S3.txt)
    - `Amit_2015/Supplementary_dataset_2.txt` - Cell metadata for murine hematopoiesis analysis. [Source](https://media.nature.com/original/nature-assets/nbt/journal/v36/n5/extref/nbt.4096-S4.txt)
    - `Amit_2015` - Cell metadata for cross-species pancreatic islet analysis. [Source](https://media.nature.com/original/nature-assets/nbt/journal/v36/n5/extref/nbt.4096-S5.txt)
    - `Amit_2015/generate_clustering.tar.gz` - all the data and scripts required for reproducing the MARS-seq results. 913Gb. [Source](http://www.wisdom.weizmann.ac.il/~arkiny/Paul2015/generate_clustering.tar.gz)

- Yan, Liying, Mingyu Yang, Hongshan Guo, Lu Yang, Jun Wu, Rong Li, Ping Liu, et al. “Single-Cell RNA-Seq Profiling of Human Preimplantation Embryos and Embryonic Stem Cells.” Nature Structural & Molecular Biology 20, no. 9 (September 2013): 1131–39. https://doi.org/10.1038/nsmb.2660. - scRNA-seq of human embryos and embryonic stem cells. 124 cells at different stages of development. Clustering, PCA. Expression of novel genes and de novo assembly of other transcripts, including lncRNAs. https://www.ncbi.nlm.nih.gov/geo/query/acc.cgi?acc=GSE36552

#### Cancer

- Azizi, Elham, Ambrose J. Carr, George Plitas, Andrew E. Cornish, Catherine Konopacki, Sandhya Prabhakaran, Juozas Nainys, et al. “Single-Cell Map of Diverse Immune Phenotypes in the Breast Tumor Microenvironment.” Cell, June 2018. https://doi.org/10.1016/j.cell.2018.05.060. - scRNA-seq of immune cells in BRCA - continuous activation of T cells, no macrophage polarization. inDrop and 10X platforms. 47,016 CD45+ cells from 8 primary breast carcinomas. 83 clusters, tested by cross-validation. Data: https://www.ncbi.nlm.nih.gov/geo/query/acc.cgi?acc=GSE114727, https://www.ncbi.nlm.nih.gov/geo/query/acc.cgi?acc=GSE114725, https://www.ncbi.nlm.nih.gov/geo/query/acc.cgi?acc=GSE114724 

### Mouse

- `DropViz` - Exploring the Mouse Brain through Single Cell Expression Profiles. Drop-seq to analyze 690,000 individual cells from nine different regions of the adult mouse brain. http://dropviz.org/

- `STARmap` - in situ gene expression datasets of the mouse visual cortex (890 cells, 1,020 genes). https://www.starmapresources.com/data/

- Mouse Cell Atlas - http://bis.zju.edu.cn/MCA/

- Tablua Muris - Mouse scRNA-seq of 100,605 cells from 20 organs and tissues. Web-site http://tabula-muris.ds.czbiohub.org/, and GitHub with gene matrix download and other scripts to reproduce all figures in the paper, https://github.com/czbiohub/tabula-muris. Raw data are at https://www.ncbi.nlm.nih.gov/geo/query/acc.cgi?acc=GSE109774. Processed: https://figshare.com/articles/Single-cell_RNA-seq_data_from_Smart-seq2_sequencing_of_FACS_sorted_cells_v2_/5829687/1
    - Quake, Stephen R., Tony Wyss-Coray, and Spyros Darmanis. “Single-Cell Transcriptomic Characterization of 20 Organs and Tissues from Individual Mice Creates a Tabula Muris,” March 29, 2018. https://doi.org/10.1101/237446. 

- The 1 million neuron data set from E18 mice, from the 10X Genomics website (https://support.10xgenomics.com/single-cell-gene-expression/datasets). R packages for its analyses: 
    - `TENxGenomics` - https://github.com/mtmorgan/TENxGenomics
    - `TENxBrainAnalysis` - https://github.com/Bioconductor/TENxBrainAnalysis

- Single-cell ATAC-seq, approx. 100,000 single cells from 13 adult mouse tissues. Two sequence platforms, good concordance. Filtered data assigned into 85 clusters. Genes associated with the corresponding ATAC sites (Cicero for identification). Differential accessibility. Motif enrichment (Basset CNN). GWAS results enrichment. All data and metadata are available for download as text or rds format at http://atlas.gs.washington.edu/mouse-atac/
    - Cusanovich, Darren A., Andrew J. Hill, Delasa Aghamirzaie, Riza M. Daza, Hannah A. Pliner, Joel B. Berletch, Galina N. Filippova, et al. “A Single-Cell Atlas of In Vivo Mammalian Chromatin Accessibility.” Cell 174, no. 5 (August 2018): 1309-1324.e18. https://doi.org/10.1016/j.cell.2018.06.052. 

- scRNA-seq of aging. >50,000 cells from kidney, lung, and spleen in young (7 months) and aged (22-23 months) mice. Transcriptional variation using difference from the median. Cell-cell heterogeneity using the Euclidean distance from centroids. Aging trajectories derived from NMF embedding. Cell type identification by neural network trained on Tabula Muris. ln(CPM + 1) UMIs used for all analyses. Visualization, downloadable data, code, pre-trained network.  https://mca.research.calicolabs.com/
    - Kimmel, Jacob C, Lolita Penland, Nimrod D Rubinstein, David G Hendrickson, David R Kelley, and Adam Z Rosenthal. “A Murine Aging Cell Atlas Reveals Cell Identity and Tissue-Specific Trajectories of Aging.” BioRxiv, January 1, 2019, 657726. https://doi.org/10.1101/657726.

- scRNA-seq (10X Genomics) of murine cerebellum. 39245 cells (after filtering) from 12 time points, 48 distinct clusters. Cell Seek for online exploration, https://cellseek.stjude.org/cerebellum/ and https://gawadlab.github.io/CellSeek/. Approx. 83,000 cells (BAM files per time point) are available at https://www.ebi.ac.uk/ena/data/view/PRJEB23051. No annotations.
    - Carter, Robert A., Laure Bihannic, Celeste Rosencrance, Jennifer L. Hadley, Yiai Tong, Timothy N. Phoenix, Sivaraman Natarajan, John Easton, Paul A. Northcott, and Charles Gawad. “A Single-Cell Transcriptional Atlas of the Developing Murine Cerebellum.” Current Biology, September 2018. https://doi.org/10.1016/j.cub.2018.07.062. 

- Sci-CAR, single-cell RNA- and ATAC-seq. Two experiments: 1) Lung adenocarcinoma A549 cells, dexametasone treatment over 3 timepoints. 2) Mixture of HEK293T (human) and NIH3T3 (mouse) cells. Differential gene expression, accessibility analysis, clustering. Linking distal open chromatin to genes, 44% map to nearest, 21 to the second nearest. Gene expression counts and ATAC-seq peaks, https://www.ncbi.nlm.nih.gov/geo/query/acc.cgi?acc=GSE117089
    - Cao, Junyue, Darren A. Cusanovich, Vijay Ramani, Delasa Aghamirzaie, Hannah A. Pliner, Andrew J. Hill, Riza M. Daza, et al. “Joint Profiling of Chromatin Accessibility and Gene Expression in Thousands of Single Cells.” Science 361, no. 6409 (September 28, 2018): 1380–85. https://doi.org/10.1126/science.aau0730. 

- Mouse spinal cord development scRNA-seq. Temporal (embryonic day 9.5-13.5) and spatial (cervical and thoracic regions of the neural tube) profiling. 10X genomics protocol, Cell Ranger processing, filtering, combinatorial testing for differential expression, pseudotime reconstruction using Monocle2. UMI matrix (21465 cells), https://www.ebi.ac.uk/arrayexpress/experiments/E-MTAB-7320/, code, https://github.com/juliendelile/MouseSpinalCordAtlas,  Table S1 - binarized matrix of gene markers for each neuronal subtype, http://www.biologists.com/DEV_Movies/DEV173807/TableS1.csv
    - Delile, Julien, Teresa Rayon, Manuela Melchionda, Amelia Edwards, James Briscoe, and Andreas Sagner. “Single Cell Transcriptomics Reveals Spatial and Temporal Dynamics of Gene Expression in the Developing Mouse Spinal Cord.” Development, March 7, 2019, dev.173807. https://doi.org/10.1242/dev.173807. 

- Mouse pancreas scRNA-seq, \~12,000 cells. https://www.ncbi.nlm.nih.gov/geo/query/acc.cgi?acc=GSE84133. Deconvolution of bulk RNA-seq data using cell signatures derived from clusters of scRNA-seq cells, https://github.com/shenorrLab/bseqsc
    - Baron, Maayan, Adrian Veres, Samuel L. Wolock, Aubrey L. Faust, Renaud Gaujoux, Amedeo Vetere, Jennifer Hyoje Ryu, et al. “A Single-Cell Transcriptomic Map of the Human and Mouse Pancreas Reveals Inter- and Intra-Cell Population Structure.” Cell Systems 3, no. 4 (26 2016): 346-360.e4. https://doi.org/10.1016/j.cels.2016.08.011.

- The full-length SMART-Seq2 protocol with deep sequencing (6,558 genes/cell) to profile 765 multipotent mouse hematopoietic progenitors. https://www.ncbi.nlm.nih.gov/geo/query/acc.cgi?acc=GSE81682
    - Nestorowa, S., F. K. Hamey, B. Pijuan Sala, E. Diamanti, M. Shepherd, E. Laurenti, N. K. Wilson, D. G. Kent, and B. Gottgens. “A Single-Cell Resolution Map of Mouse Hematopoietic Stem and Progenitor Cell Differentiation.” Blood 128, no. 8 (August 25, 2016): e20–31. https://doi.org/10.1182/blood-2016-05-716480.

- Buettner, Florian, Kedar N Natarajan, F Paolo Casale, Valentina Proserpio, Antonio Scialdone, Fabian J Theis, Sarah A Teichmann, John C Marioni, and Oliver Stegle. “Computational Analysis of Cell-to-Cell Heterogeneity in Single-Cell RNA-Sequencing Data Reveals Hidden Subpopulations of Cells.” Nature Biotechnology 33, no. 2 (March 2015): 155–60. https://doi.org/10.1038/nbt.3102.
    - `data/scLVM/nbt.3102-S7.xlsx` - Uncorrected and cell-cycle corrected expression values (81 cells x 7073 genes) for T-cell data. Includes cluster assignment to naive T cells vs. TH2 cells (GATA3 high marker). [Source](https://media.nature.com/original/nature-assets/nbt/journal/v33/n2/extref/nbt.3102-S7.xlsx)
    - `data/scLVM/nbt.3102-S8.xlsx` - Corrected and uncorrected expression values for the newly generated mouse ESC data. 182 samples x 9571 genes. [Source](https://media.nature.com/original/nature-assets/nbt/journal/v33/n2/extref/nbt.3102-S8.xlsx)

- Zeisel, A., Munoz-Manchado, A.B., Codeluppi, S., Lonnerberg, P., La Manno, G., Jureus, A., Marques, S., Munguba, H., He, L., Betsholtz, C., et al. (2015). Brain structure. Cell types in the mouse cortex and hippocampus revealed by single-cell RNA- seq. Science 347, 1138–1142. - 3,005 single cells from the hippocampus and cerebral cortex of mice. https://www.ncbi.nlm.nih.gov/geo/query/acc.cgi?acc=GSE60361, http://linnarssonlab.org/cortex/, and more on this site.
    - `data/Brain/Zeisel_2015_TableS1.xlsx` - Table S1 - gene signatures for Ependymal, Oligodendrocyte, Microglia, CA1 Pyramidal, Interneuron, Endothelial, S1 Pyramidal, Astrocyte, Mural cells. [Source](http://science.sciencemag.org/highwire/filestream/628248/field_highwire_adjunct_files/1/aaa1934_TableS1.xlsx)
    - `data/Brain/expression_mRNA_17-Aug-2014.txt` - 19,972 genes x 3005 cells. Additional rows with class annotations to interneurons, pyramidal SS, pyramidal CA1, oligodendrocytes, microglia, endothelial-mural, astrocytes_ependymal, further subdivided into 47 subclasses. [Source](https://storage.googleapis.com/linnarsson-lab-www-blobs/blobs/cortex/expression_mRNA_17-Aug-2014.txt)



### Brain single-cell data

- Brain immune atlas scRNA-seq resource. Border-associated macrophages from discrete mouse brain compartments, tissue-specific transcriptional signatures. http://www.brainimmuneatlas.org/index.php, https://github.com/saeyslab/brainimmuneatlas/
    - Van Hove, Hannah, Liesbet Martens, Isabelle Scheyltjens, Karen De Vlaminck, Ana Rita Pombo Antunes, Sofie De Prijck, Niels Vandamme, et al. “A Single-Cell Atlas of Mouse Brain Macrophages Reveals Unique Transcriptional Identities Shaped by Ontogeny and Tissue Environment.” Nature Neuroscience, May 6, 2019. https://doi.org/10.1038/s41593-019-0393-4.

- Darmanis, S., Sloan, S.A., Zhang, Y., Enge, M., Caneda, C., Shuer, L.M., Hayden Gephart, M.G., Barres, B.A., and Quake, S.R. (2015). A survey of human brain transcriptome diversity at the single cell level. Proc. Natl. Acad. Sci. USA 112, 7285–7290. - Single cell brain transcriptomics, human. Fluidigm C1 platform. Healthy cortex cells (466 cells) containing: Astrocytes, oligodendrocytes, oligodendrocyte precursor cells (OPCs), neurons, microglia, and vascular cells. Single cells clustered into 10 clusters, their top 20 gene signatures are in Supplementary Table S3. Raw data athttps://www.ncbi.nlm.nih.gov/geo/query/acc.cgi?acc=GSE67835
    - `data/Brain/TableS3.txt` - top 20 cell type-specific genes
    - `data/Brain/TableS3_matrix.txt` - genes vs. cell types with 0/1 indicator variables.

- Nowakowski, Tomasz J., Aparna Bhaduri, Alex A. Pollen, Beatriz Alvarado, Mohammed A. Mostajo-Radji, Elizabeth Di Lullo, Maximilian Haeussler, et al. “Spatiotemporal Gene Expression Trajectories Reveal Developmental Hierarchies of the Human Cortex.” Science 358, no. 6368 (December 8, 2017): 1318–23. https://doi.org/10.1126/science.aap8809. - single-cell RNA-seq of neuronal cell types. Dimensionality reduction, clustering, WGCNA, defining cell type-specific signatures, comparison with other signatures (Zeng, Miller). 
    - `data/Brain/Nowakowski_2017_Tables_S1-S11.xlsx` - Table S5 has brain region-specific gene signatures. [Source](http://science.sciencemag.org/highwire/filestream/703290/field_highwire_adjunct_files/1/aap8809_Nowakowski_SM-Tables-S1-S11.xlsx) 

- Luo, Chongyuan, Christopher L. Keown, Laurie Kurihara, Jingtian Zhou, Yupeng He, Junhao Li, Rosa Castanon, et al. “Single-Cell Methylomes Identify Neuronal Subtypes and Regulatory Elements in Mammalian Cortex.” Science (New York, N.Y.) 357, no. 6351 (11 2017): 600–604. https://doi.org/10.1126/science.aan3351. - single-cell methylation of human and mouse neuronal cells. Marker genes with cell type-specific methylation profiles - Table S3, http://science.sciencemag.org/content/suppl/2017/08/09/357.6351.600.DC1

- Major Depressive Disorder Working Group of the Psychiatric Genomics Consortium et al., “Genetic Identification of Brain Cell Types Underlying Schizophrenia,” Nature Genetics 50, no. 6 (June 2018): 825–33, https://doi.org/10.1038/s41588-018-0129-5. - Cell-type specificity of schizophrenia SNPs judged by enrichment in expressed genes. scRNA-seq custom data collection. Difference between schizophrenia and neurological disorders.
    - `data/Brain_cell_type_gene_expression.xlsx` - Supplementary Table 4 - Specificity values for Karolinska scRNA-seq superset. Specificity represents the proportion of the total expression of a gene found in one cell type as compared to that in all cell types (i.e., the mean expression in one cell type divided by the mean expression in all cell types). Gene X cell type matrix. Level 1 (core cell types) and level 2 (extended collection of cell types) data. [Source](https://static-content.springer.com/esm/art%3A10.1038%2Fs41588-018-0129-5/MediaObjects/41588_2018_129_MOESM3_ESM.xlsx)

- Nowakowski, Tomasz J., Aparna Bhaduri, Alex A. Pollen, Beatriz Alvarado, Mohammed A. Mostajo-Radji, Elizabeth Di Lullo, Maximilian Haeussler, et al. “Spatiotemporal Gene Expression Trajectories Reveal Developmental Hierarchies of the Human Cortex.” Science 358, no. 6368 (December 8, 2017): 1318–23. https://doi.org/10.1126/science.aap8809. - single-cell RNA-seq of human neuronal cell types. Dimensionality reduction, clustering, WGCNA, defining cell type-specific signatures, comparison with other signatures (Zeng, Miller). Supplementary material at http://science.sciencemag.org/content/suppl/2017/12/06/358.6368.1318.DC1 Table 5 has gene signatures.https://www.wired.com/story/neuroscientists-just-launched-an-atlas-of-the-developing-human-brain/. Controlled access data on dbGAP, https://www.ncbi.nlm.nih.gov/projects/gap/cgi-bin/study.cgi?study_id=phs000989.v3.p1, summarized matrix with annotations is available on https://cells.ucsc.edu/?ds=cortex-dev


## Links

- Introduction to single-cell RNA-seq technologies, presentation by Lior Pachter. Key figures, references, statistics. Slides, https://figshare.com/articles/Introduction_to_single-cell_RNA-seq_technologies/7704659/1, and notes, https://liorpachter.wordpress.com/2019/02/19/introduction-to-single-cell-rna-seq-technologies/

- http://hemberg-lab.github.io/scRNA.seq.course/ - Analysis of single cell RNA-seq data, step-by-step R tutorial, description of packages, data. Analysis using read counts or UMIs. SingleCellExperiment, Seurat. Video lectures https://www.youtube.com/watch?list=PLEyKDyF1qdOYAhwU71qlrOXYsYHtyIu8n&v=56n77bpjiKo

- https://osca.bioconductor.org/ - Amezquita, Robert A., Vincent J. Carey, Lindsay N. Carpp, Ludwig Geistlinger, Aaron TL Lun, Federico Marini, Kevin Rue-Albrecht, et al. “Orchestrating Single-Cell Analysis with Bioconductor.” BioRxiv, March 27, 2019. https://doi.org/10.1101/590562. - scRNA-seq analysis overview within Bioconductor ecosystem. SingleCellexperiment, scran and scater examples. Table S1 - summary of packages for data input, infrastructure, QC, integration, dimensionality reduction, clustering, pseudotime, differential expression, functional enrichment, simulation, benchmarking data, and data packages. Types of feature selection. https://github.com/Bioconductor/OrchestratingSingleCellAnalysis, https://github.com/Bioconductor/OSCABase

- A step-by-step workflow for low-level analysis of single-cell RNA-seq data with Bioconductor, by Aaron Lun et al. https://bioconductor.org/packages/release/workflows/html/simpleSingleCell.html

- A Google Doc with a structured collection of methods, software, and many other scRNA-seq information, https://docs.google.com/spreadsheets/d/1IPe2ozb1Mny8sLvJaSE57RJr3oruiBoSudAVhSH-O8M/edit#gid=11468010 

- https://en.wikipedia.org/wiki/List_of_RNA-Seq_bioinformatics_tools#Single_cell_RNA-Seq

- https://github.com/crazyhottommy/RNA-seq-analysis#single-cell-rna-seq

- https://www.scrna-tools.org/ - Zappia, Luke, Belinda Phipson, and Alicia Oshlack. “Exploring the Single-Cell RNA-Seq Analysis Landscape with the ScRNA-Tools Database.” BioRxiv, January 1, 2018. https://doi.org/10.1101/206573.

- https://github.com/seandavi/awesome-single-cell

- https://github.com/johandahlberg/awesome-10x-genomics

- https://davetang.org/muse/category/single-cell-2/

- Figure depicting the breadth of multimodal scRNA-seq technologies, https://github.com/arnavm/multimodal-scRNA-seq

- How many cells do we need to sample so that we see at least n cells of each type? https://satijalab.org/howmanycells

- `Loompy` - file format for large omics datasets. http://loompy.org/. Includes scRNA-seq datasets in `.loom` format, http://loom.linnarssonlab.org/. Example R script to read the data in, [loom.R](tools/loom.R)


### Papers

- Vieth, Beate, Swati Parekh, Christoph Ziegenhain, Wolfgang Enard, and Ines Hellmann. “A Systematic Evaluation of Single Cell RNA-Seq Analysis Pipelines.” BioRxiv, March 19, 2019. https://doi.org/10.1101/583013. scRNA-seq pipeline benchmarking, beta regression to explain the variance in pipeline performance. Best settings: Genome mapping using STAR + GENCODE annotation, imputation using scone or SAVER is optional, scran or SCnorm for normalization, any differential expression method, e.g., edgeR and limma-trend, works OK. Filtering has no effect on performance. The most significant effect on performance is from normalization and library preparation choices. Pipelines tested with `powsimR` package https://github.com/bvieth/powsimR, data at https://github.com/bvieth/scRNA-seq-pipelines

- Luecken, Malte D., and Fabian J. Theis. “Current Best Practices in Single-Cell RNA-Seq Analysis: A Tutorial.” Molecular Systems Biology 15, no. 6 (June 19, 2019): e8746. https://doi.org/10.15252/msb.20188746. - All steps in scRNA-seq analysis, QC (count depth, number of genes, % mitochondrial), normalization (global, downsampling, nonlinear), data correction (batch, denoising, imputation), feature selection, dimensionality reduction (PCA, diffusion maps, tSNE, UMAP), visualization, clustering (k-means, graph/community detection), annotation, trajectory inference (PAGA, Monocle), differential analysis (DESeq2, EdgeR, MAST), gene regulatory networks. Description of the bigger picture at each step, latest tools, their brief description, references. R-based Scater as the full pipeline for QC and preprocessing, Seurat for downstream analysis, scanpy Python pipeline. Links and refs for tutorials. https://github.com/theislab/single-cell-tutorial

- Stuart, Tim, Andrew Butler, Paul Hoffman, Christoph Hafemeister, Efthymia Papalexi, William M Mauck, Marlon Stoeckius, Peter Smibert, and Rahul Satija. “Comprehensive Integration of Single Cell Data.” Preprint. Genomics, November 2, 2018. https://doi.org/10.1101/460147. https://www.cell.com/cell/fulltext/S0092-8674(19)30559-8
    - Seurat v.3 paper. Integration of multiple scRNA-seq and other single-cell omics (spatial transcriptomics, scATAC-seq, immunophenotyping), including batch correction. Anchors as reference to harmonize multiple datasets. Canonical Correlation Analysis (CCA) coupled with Mutual Nearest Neighborhoors (MNN) to identify shared subpopulations across datasets. CCA to reduce dimensionality, search for MNN in the low-dimensional representation. Shared Nearest Neighbor (SNN) graphs to assess similarity between two cells. Outperforms scmap. Extensive validation on multiple datasets (Human Cell Atlas, STARmap mouse visual cortex spatial transcriptomics. Tabula Muris, 10X Genomics datasets, others in STAR methods). Data normalization, variable feature selection within- and between datasets, anchor identification using CCA (methods), their scoring, batch correction, label transfer, imputation. Methods correspond to details of each Seurat function. Preprocessing of real single-cell data.https://satijalab.org/seurat/

- Cao, Junyue, Jonathan S. Packer, Vijay Ramani, Darren A. Cusanovich, Chau Huynh, Riza Daza, Xiaojie Qiu, et al. “Comprehensive Single-Cell Transcriptional Profiling of a Multicellular Organism.” Science 357, no. 6352 (August 18, 2017): 661–67. https://doi.org/10.1126/science.aam8940. - sciRNA-seq - single-cell combinatorial indexing RNA-seq technology and sequencing of C. elegans, ~49,000 cells, 27 cell types. Data and R code to download it at http://atlas.gs.washington.edu/hub/
