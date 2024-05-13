# ICTVdump
Download viral genomes by connecting to the latest ICTV Virus Metadata Resource (VMR)
## Important!  
*We have run this pipeline and stored the "ready-to-use" sequences on [Zenodo](https://zenodo.org/records/11183043).*  
The user interested in quickly accessing the pre-computed data should download the following two files:   
<br>

[Exemplar_sorts.fa.gz](https://zenodo.org/records/11183043/files/exemplar_sorts.fa.gz?download=1) Viral genomes (DNA) grouped by 'sort', filtered according to the paper's criteria [TBD] and with concatenated segmented sequences. FASTA headers are formatted as '>sort\_{sort}\_{number of concatenated segments}\_{genome length}'  
[Exemplar_sorts.tsv.gz](https://zenodo.org/records/11183043/files/exemplar_sorts.tsv.gz?download=1) ICTV taxonomy for the above. The column 'header' links the FASTA headers for easy access.  

<br>

For convenience, we also included the full dataset, which is unfiltered and contains the raw GenBank DNA sequences ([exemplars.tsv.gz](https://zenodo.org/records/11183043/files/exemplars.tsv.gz?download=1)). The precalculated LLRs for taxonomic prediction (see paper) are stored in the compressed folder [LLR.zip](https://zenodo.org/records/11183043/files/LLR.zip?download=1).  

## Manual  
The following repository provides the source code to download and format viral genomes from the ICTV, from scratch. As stated in https://ictv.global/vmr, the ICTV *chooses an exemplar virus for each species and the VMR provides a list of these exemplars (...) and includes the GenBank accession number for the genomic sequence of the isolate as well as the virus name, isolate designation, suggested abbreviation, genome composition, and host source*.  
<br>
ICTVdump automatically collects sequences and metadata associated to each exemplar virus in the latest VMR. It is a simple and powerful python framework with only a few requirements that makes over 16,000 records available in less than 2 hours.

Upon installation of the dependencies the program operates taking a non-existing directory as input. Three subcommands will allow the user to download, filter, match protein markers and produce a pre-computed LLR matrix. More information is given in our paper at [TBD].
 ```bash
./ictvdump download -i myfolder
./ictvdump match -i myfolder
./ictvdump precalculate -i myfolder
 ```

<br>  
