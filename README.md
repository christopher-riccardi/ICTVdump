# ICTVdump
We envisioned to facilitate the access to any release of the Virus Metadata Resource (VMR). ICTVdump automatically collects taxonomic labels and viral genomic sequences associated to every virus listed in the official taxonomy (ICTV). By default, the latest version of the VMR is accessed, with the possibility of downloading any previous version through the command line option ```-u```.  

![alt text](ictv_workflow.svg)

## Usage  
ICTVdump is written in python and its dependencies are listed [here](#dependencies-and-installation). The program automatically connects to the VMR, retrieves the GenBank identifiers, downloads them in batch from the NCBI and generates an SQL database and one taxonomy table. When the path to an already existing database is provided, ICTVdump skips the download of sequences that are already present, which saves a lot of time for users interested in accessing several releases of the VMR. The taxonomy table lists the ICTV-ratified taxa for every virus for which at least one GenBank accession was found.   
 ```bash
python ictvdump -d <str> -o <str> [-u <url to any version, or default>]
 ```
## Example  
To download the latest version of the VMR, run the following command:
```{bash}
python ictvdump -d gb.db -o VMR_latest -u https://ictv.global/vmr/current?fid=15873#block-teamplus-page-title
```
To download a specific version, such as VMR_MSL39_v1 (the version used in the paper for evaluation), use the command below:
```{bash}
python ictvdump -d gb.db -o VMR_MSL39_v1 -u https://ictv.global/sites/default/files/VMR/VMR_MSL39_v1.xlsx
```

## Dependencies and installation  
The recommended way to install the dependencies is through conda/mamba on Linux kernel:  
```conda create -n ictv -c conda-forge openpyxl numpy pandas -y```  
with the inclusion of [Entrez Direct](https://www.ncbi.nlm.nih.gov/books/NBK179288/) in a separate step:  
```sh -c "$(curl -fsSL https://ftp.ncbi.nlm.nih.gov/entrez/entrezdirect/install-edirect.sh)"```.  

<br>  

## Additional  
For convenience, we provide a [script](script) that allows access to every version of the VMR up until version MSL39_1
