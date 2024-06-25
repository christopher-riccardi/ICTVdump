# ICTVdump
ICTVdump automatically collects DNA sequence and metadata associated to every exemplar virus listed in the ICTV Virus Metadata Resource (VMR). By default the latest VMR is accessed, but it is also possible to download the previous versions by feeding the desired link to the command line option ```-u```.  

## Usage of the 'download' subcommand  
ICTVdump is written in python and its dependencies are listed [here](#dependencies-and-installation). The 'download' subcommand automatically connects to the VMR, retrieves the GenBank identifiers, downloads them in batch from NCBI and generates three main files: a multi-FASTA with viral sequences organized by viral sort, a taxonomy table linking each viral sort to its latest ICTV-defined taxonomy, and one raw data table with the starting VMR metadata + sequences. The only mandatory argument is the name of a non-existing directory where ICTVdump will operate.   
 ```bash
./ictvdump download -i myfolder
 ```
Upon completion (approximately 90 minutes for the latest VMR), three files **exemplar_sorts.fa** (multi-FASTA), **exemplar_sorts.tsv** (taxonomy table) and **exemplars.tsv.gz** (the raw data table) will be present in the path specified by ```-i```. See the [Important notice](#important-notice) section to download these three files directly without running the pipeline.  

## Dependencies and installation  
The recommended way to install the dependencies is through conda/mamba on Linux kernel:  
```conda create -n ictv -c conda-forge -c bioconda biopython openpyxl numpy pandas prodigal-gv mmseqs2 -y```  
with the inclusion of [Entrez Direct](https://www.ncbi.nlm.nih.gov/books/NBK179288/) in a separate step:  
```sh -c "$(curl -fsSL https://ftp.ncbi.nlm.nih.gov/entrez/entrezdirect/install-edirect.sh)"```.  

<br>  

<br>  

<br>  

## Additional subcommands    
This section is specific to our upcoming paper ([TBD]) and will be thoroughly documented soon. 
