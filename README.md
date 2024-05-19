# ICTVdump
Download viral genomes by connecting to the latest ICTV Virus Metadata Resource (VMR)
## Important notice  
We've pre-run this pipeline and stored the 'ready-to-use' sequences on [Zenodo](https://zenodo.org/records/11218054). Users who wish to swiftly access the pre-computed data can do so by downloading the following two files:   
<br>
[Exemplar_sorts.fa](https://zenodo.org/records/11218054/files/exemplar_sorts.fa?download=1) Viral genomic DNA sequences grouped by 'sort'. Multipartite genomes are concatenated. FASTA headers are formatted as such: '>sort\_{sort identifier}\_{number of concatenated segments}\_{genome length (bp)}'  
[Exemplar_sorts.tsv](https://zenodo.org/records/11218054/files/exemplar_sorts.tsv?download=1) ICTV taxonomy for the above. The column 'header' links the FASTA headers for easy access.  

<br>

For convenience, we also included the full dataset, i.e., genomic sequences + metadata not grouped by viral sort: ([exemplars.tsv.gz](https://zenodo.org/records/11218054/files/exemplars.tsv.gz?download=1)). The precalculated LLRs for taxonomic prediction (see paper) are stored in the compressed folder [LLR.zip](https://zenodo.org/records/11218054/files/LLR.zip?download=1).  

## Introduction  
This repository offers the source code for downloading exemplar viral genomes from the NCBI, with taxonomy curated by the ICTV. As stated in https://ictv.global/vmr, the ICTV *chooses an exemplar virus for each species and the VMR provides a list of these exemplars (...) and includes the GenBank accession number for the genomic sequence of the isolate as well as the virus name, isolate designation, suggested abbreviation, genome composition, and host source*.  
<br>
ICTVdump automatically collects sequences and metadata associated to each exemplar virus in the latest VMR. It is a simple and powerful python framework with only a few requirements that makes over 16,000 records available in less than 2 hours.

## Usage  
ICTVdump is written in python and its dependencies are listed [here](#dependencies-and-installation). It is composed of three subcommands, 'download', 'match' and 'precalculate'. The first one automatically connects to the VMR, retrieves the GenBank identifiers, downloads them in batch from NCBI and generates three main files: a multi-FASTA with viral sequences organized by viral sort, a taxonomy table linking each viral sort to its latest ICTV-defined taxonomy, and one raw data table with the starting VMR metadata + sequences. The only mandatory argument is the name of a non-existing directory where ICTVdump will operate.   
 ```bash
./ictvdump download -i myfolder
 ```
Upon completion (approximately 90 minutes), three files **exemplar_sorts.fa** (multi-FASTA), **exemplar_sorts.tsv** (taxonomy table) and **exemplars.tsv.gz** (the raw data table) will be present in the path specified by "-i". See the [Important notice](#important-notice) section to download these three files without running the pipeline.  

## Matching markers from geNomad and precalculating the LLRs  
With ICTVdump it is also possible to infer the open reading frames (ORFs) of viral genomes, match the amino acid sequences to geNomad's viral-specific protein markers dataset, and compute the log-likelihood ratio background of each viral taxonomy. See our paper [TBD] for a thorough explanation. When the pipline is executed end to end:  

 ```bash
./ictvdump download -i myfolder
./ictvdump match -i myfolder #same name given to "download" subcommand
./ictvdump precalculate -i myfolder
 ```
two additional files are generated, feature_matrix.pkl and LLR.zip. The former is a logical matrix that indicates the presence (1) or absence (0) of protein markers (columns) in each viral sort (rows). The latter is a compressed folder containing genus-wise precomputed log-likelihood ratio matrices. LLR.zip serves as the basis for virus classification using protein markers.   

<br>  

## Dependencies and installation  
The recommended way to install the dependencies is through conda/mamba on Linux kernel:  
```conda create -n ictv -c conda-forge -c bioconda biopython openpyxl numpy pandas prodigal-gv mmseqs2 -y```  
with the inclusion of [Entrez Direct](https://www.ncbi.nlm.nih.gov/books/NBK179288/) in a separate step:  
```sh -c "$(curl -fsSL https://ftp.ncbi.nlm.nih.gov/entrez/entrezdirect/install-edirect.sh)"```.  

