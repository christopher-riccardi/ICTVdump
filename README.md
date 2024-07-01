# ICTVdump
ICTVdump automatically collects DNA sequence and metadata associated to every exemplar virus listed in the ICTV Virus Metadata Resource (VMR). By default the latest VMR is accessed, but it is also possible to download the previous versions by feeding the desired link to the command line option ```-u```.  

## Usage  
ICTVdump is written in python and its dependencies are listed [here](#dependencies-and-installation). The program automatically connects to the VMR, retrieves the GenBank identifiers, downloads them in batch from NCBI and generates one data table with the ICTV-ratified lineage for each virus, as well as their sequence and metadata. The only mandatory argument is the name of a non-existing directory where ICTVdump will operate.   
 ```bash
./ictvdump -i myfolder
 ```
Upon completion (approximately 40 minutes for the latest VMR),  **exemplars.tsv.gz** (the raw data table) will be present in the path specified by ```-i```. See the [Important notice](#important-notice) section to download this file directly without running the pipeline.  

## Dependencies and installation  
The recommended way to install the dependencies is through conda/mamba on Linux kernel:  
```conda create -n ictv -c conda-forge -c bioconda biopython openpyxl numpy pandas -y```  
with the inclusion of [Entrez Direct](https://www.ncbi.nlm.nih.gov/books/NBK179288/) in a separate step:  
```sh -c "$(curl -fsSL https://ftp.ncbi.nlm.nih.gov/entrez/entrezdirect/install-edirect.sh)"```.  

<br>  
