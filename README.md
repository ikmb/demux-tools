# demux-tools

Tools for the Demux Pipeline

How to build:

This will not build from the current repository. To build the container, you will need to manually obtain the 10X Genomics tools from:

10X Genomics Longranger [here](https://support.10xgenomics.com/genome-exome/software/downloads/latest)

10X Genomics Cellranger [here](https://support.10xgenomics.com/single-cell-gene-expression/software/downloads/latest)

10X Genomics Cellranager ATAC [here](https://support.10xgenomics.com/single-cell-atac/software/downloads/latest)

10X Genomics Supernova [here](https://support.10xgenomics.com/de-novo-assembly/software/downloads/latest)

10X Genomics Spaceranger [here](https://support.10xgenomics.com/spatial-gene-expression/software/downloads/latest)

Why is this necessary? Well, 10XGenomics download links are not persistent and need to be updated directly before buidling the container :(


To build the container, copy the files `Singularity` and `environment.yml` to a machine on which you have sudo rights and where Singularity is installed. 

Next, create a subfolder called "10x" and copy the tar archives of the 10X Genomics tools there. 

Finally, if the versions of the 10X tools were updated, modify the file `Singularity` to adjust the version names throughout. 

You should now be able to build the container like so:

```
singularity build ikmb-demux-1.0.simg Singularity
```


