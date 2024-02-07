# Reproduce analyses for Budd & Gunn et al. 2020
<font size="+1">Follow the steps listed below in the <b><i>Analyses</i></b> section to reproduce analyses for Budd & Gunn et al. (2020). Each step below gives a summary of the analysis and directs you to a general code file which then works through the analysis step-by-step. This general file will usually point you to other Rmd code, bash shell scripts, or python scripts. Each analysis is contained within sub-directories of the same name in the main R project directory.</font>

<b>Find the article here</b>: <a href="url">https://onlinelibrary.wiley.com/doi/10.1002/ece3.6305</a>

Citation here: Budd K, Gunn JC, Finch T, Klymus K, Sitati N, Eggert LS. Effects of diet, habitat, and phylogeny on the fecal microbiome of wild African savanna (<i>Loxodonta africana</i>) and forest elephants (<i>L. cyclotis</i>). Ecol Evol. 2020;10:5637–5650.

## Project: Assessing effects of phylogeny, diet, and habitat on gut microbial composition in African elephants 
We characterized the Afican elephant gut microbiome (aka, A.E.G.M.), specifically of African Savanna elephants (<i>Loxodonta africana</i>) and African Forest elephants (<i>Loxodonta cyclotis</i>). We assessed the relationship of gut microbial composition, including analyses of alpha and beta diversity, with host phylogeny (i.e., species) and habitat type (i.e., forest or savanna) for both species. We also assessed the relationship between microbial composition and diet (i.e., crop-raiding vs. non-crop-raiding) within <i>L. africana</i>. 
## General information on repository structure
This is a publicly visible GitHub repository storing code (and a small amount of data, although we have done our best to avoid uploading large amounts of data due to the limited storage in GitHub) for Budd & Gunn et al. (2020). In the home directory of the repository (Elephant_Microbiome), you will find a README.md file (the source script for this information), the R Project file (Elephant_Microbiome.Rproj), a .gitignore file, and [number] different "analysis" directories, each of which corresponds with a specific analysis conducted in our study:

1) 01_bioinformatic_analysis
2) 02_taxon_summary_analysis
3) 03_otu_abundance_analysis
4) 04_
5) 05_
6) 06_
7) 07_

Within each analysis directory, you will find an R markdown script (.Rmd) with the name of the analysis, which contains all of the code needed to run the full analysis. Additionally, you will find one:

1) code

The code directory will store all source code, shell scripts, lists of bash commands, and software packages needed for analysis. 

Once you have downloaded the repository and located the code directory, you should create two additional sub-directories within each analysis (on the same level as the code directory):

2) data
3) figures

The data directory will store all raw data, processed data, and metadata needed for analysis. The figures folder will contain any raw figures generated in ggplot for each analysis. Ideally, the Rmd script should have paths set up so that the code reads all data and scripts and generates figures seamlessly.

## Using the code
To reproduce all analyses in Budd & Gunn et al. (2020), download this repository and place in a desired home directory. This may be done on your local machine, but we recommend downloading to a high-performance computing cluster so that all code will run seamlessly in one environment, as long as Rstudio is installed and the GUI can be called on the cluster.

Once all directories are downloaded, create a new sub-directory within the home directory (same level as the seven analysis directories, .Rproj, README.md, etc.) called "raw_data". This is where you will store the raw genomic data and associated sample metadata (see <i><b>Data</i></b> section below).

## Data
Raw 16S rRNA sequence reads and accompanying metadata are available on NCBI: <a href="url">https://www.ncbi.nlm.nih.gov/bioproject/PRJNA587772/</a>

Metagenomic data files (.fastq.gz) must be downloaded individually from the NBI database. Once downloaded, place all .fastq files into a desired working directory to be accessed during bioinformatic processing in QIIME.

Code for processing raw data files in QIIME are provided in the first analysis folder ("01_bioinformatic_analysis") in this repository.

You will need only the "raw_data" table outputs from QIIME to reproduce analyses 2 through [number].

If you have any questions or issues with data and/or code, please don't hesitate to contact me: jcgunn@uvm.edu

## Analyses

### Analysis 1: Generating Species Native Range Maps
In this analysis, we generated easily readable maps displaying the native distributions of the two species of interest, Smallmouth Bass and Neosho Bass. We generated two types of maps: 1) a full range map, in which the full native range of each species is displayed, and 2) a close-up map of the Central Interior Highlands (CIH), where the paraptry of the species' ranges is shown in detail. In R, we generated only georeferenced outlines of these maps. Shapes representing stream sites and/or populations were superimposed <i>a posteriori</i> on the maps in PowerPoint.

#### Run the code: `01_map_analysis/smb_genomics_map_analysis.Rmd`

### Analysis 2: SNP Filtering, Data Processing, and Preliminary Calculations
In this analysis, we performed further quality filtering on the processed and genotyped SNPs generated at Floragenex, Inc. for Smallmouth Bass and Neosho Bass. Specifically, we screened the processed data for SNPs with greater than 15X read depth; fish samples with less than 20% genotype calls across all SNPs ("badsamples"); SNPs with a phred quality score less than 20 ("qual"); and SNPs with greater than 20% missing genotype calls across fish individuals ('missing').

#### Run the code: `02_filtering_processing_analysis/smb_genomics_filtering_processing_analysis.Rmd`

### Analysis 3: Admixture and phylogenomics
In this analysis, we used the popgen.vcf data generated in Analysis 2 (SNP Filtering...) to assess population genomic structure of Spotted Bass, Smallmouth Bass, and Neosho Bass in the CIH. Specifically, we conducted an initial screen of hybridization and gene flow by running maximum likelihood clustering on the full, filtered dataset and identified any individuals of interspecific origin between Spotted Bass and all other Interior Highlands fish (Smallmouth Bass and Neosho Bass) and individuals of interspecific origin between Smallmouth Bass and Neosho Bass. After removing hybrids, we conducted a separate admixture analysis and complementary phylogenomic analysis on the "pure" genomic samples to estimate genomic divergence between species.

#### Run the code: `03_filtering_processing_analysis/smb_genomics_admixture_phylogenomics_analysis.Rmd`

### Analysis 4: Population Inference
In this analysis, we used the finerad.vcf data generated in Analysis 2 (SNP Filtering...) to assess fine-scale coancestry between Smallmouth Bass, and Neosho Bass in the CIH using haplotype inference (excluding Spotted Bass). Specifically, we estimated coancestry in 1) the full dataset, with all pure and admixed individuals, excluding the Spotted Bass X Smallmouth Bass hybrid (BFC10) inferred from population genomic analysis in Analysis 3, 2) the pure dataset, with only pure individuals of Smallmouth Bass and Neosho Bass, and 3) the admixed dataset, with only admixed individuals of Neosho Bass (no admixed Smallmouth Bass were detected).

#### Run the code: `04_population_analysis/smb_genomics_population_analysis.Rmd`

### Analysis 5: Admixture Mapping
In this analysis, we used the popgen.vcf data generated in Analysis 2 (SNP Filtering...) to assess assess the relative timing of admixture events between Smallmouth Bass and Neosho Bass. Specifically, we used moment statistics in MatLab with the software program MIXMAPPER to build a scaffold phylogeny with significantly pure (non-admixed) populations (based on our <i>a posteriori</i>) discovered populations in Analysis 4) and to map significantly admixed populations (also based on our discovered populations in Analysis 4) onto the tree. 

#### Run the code: `05_admixture_mapping_analysis/smb_genomics_admixture_mapping_analysis.Rmd`

## Analysis 6: Directional selection analysis
In this analysis, we used the popgen.vcf data generated in Analysis 2 (SNP Filtering...) to scan for signatures of directional selection on SNP loci with outlier Fst (high outlier Fst: directional selection; low Fst: balancing selection). We used two software programs with different underlying statistical frameworks to detect outliers and then used any outliers commonly detected in both analyses as canditates for being under strong selection. Specifically, we used the software program BAYESCAN (based in Bayesian analysis) and the R package PCAdapt principal component analysis (based in multivariate principal component analysis). We then employed DAPC in R to map patterns of population differentiation at any shared outlier and neutral loci to detect populations that may be under differential selection pressures and to detect signatures of genetic drift,

#### Run the code: `06_outlier_fst_analysis/smb_genomics_outlier_fst_analysis.Rmd`

## Analysis 7: Demographic analysis
In this analysis, we investigated the demographic history of populations found to be admixed between Smallmouth Bass and Neosho Bass based on admixture and phylogenomics (Analysis 3) and admixture mapping analysis (Analysis 5). Specifically, we used the joint site frequency spectrum (JSFS) of admixed populations within the Neosho Bass range (ELK, BAYOU, ILLI, and UPPARK) and the inferred interspecific parent population within the Smallmouth Bass range (SKIA, MISS, and WHITE) to determine the relative timing of admixture events by testing multiple demographic scenarios in a model-testing maximum likelihood framework. We inferred whether admixed populations were the results of relatively recent admixture, old admixture, or a combination of both and gleaned insights about the complexities of potential natural and anthropogenic sources of gene flow.

#### Run the code: `07_demographic_analysis/smb_genomics_demographic_analysis.Rmd`