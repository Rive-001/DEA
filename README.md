# Database of eCLIP assays

[eCLIP](https://www.illumina.com/science/sequencing-method-explorer/kits-and-arrays/eclip.html) is a sequencing technique developed by Illumina, which sequences mRNA strands that are bound by RNA-binding proteins. It involves in-vivo cross-linking of RNA and protein. The protein is then immunoprecipitated and the attached mRNA is sequenced. This sequencing data is available as fastq files on [ENCODE](https://www.encodeproject.org/eclip/). This project aims to create a pipeline for extracting the mRNA sequences from these fastq files. The project comes with an API that aims to enable end-users to extract sequences from their own eCLIP experiments and compare it against the database of eCLIP experiments on ENCODE. The presentation slides for our project can be found [here](https://drive.google.com/file/d/1KjDJwkKWtvKg8dCRg9QQIzq4aPHW0L15/view?usp=sharing).

## Technology Stack

* **Language**: Shell scripting
* **Computing Platform**: HPC using SLURM workload manager

## Pipeline

The pipeline takes the fastq files from [ENCODE](https://www.encodeproject.org/eclip/) and the human hg38 reference genome from the [Ensembl genome browser](https://useast.ensembl.org/index.html). It uses [FastQC](https://www.bioinformatics.babraham.ac.uk/projects/fastqc/) to check the quality of the fastq files. Then it uses [Cutadapt](https://cutadapt.readthedocs.io/en/stable/) to remove adapters from the reads. It then aligns the trimmed reads against the reference genome using [STAR](https://github.com/alexdobin/STAR) aligner. The bam files from the aligner are indexed using [Samtools](http://www.htslib.org/) before being fed to [PureCLIP](https://github.com/skrakau/PureCLIP) for peak-calling. [Bedtools](https://bedtools.readthedocs.io/en/latest/) is used to extract raw sequences from this output. The output is stored in a BLAST database, which allows us to [BLAST](https://blast.ncbi.nlm.nih.gov/Blast.cgi) a sequence against this database of sequences.

A detailed user manual for this API can be found [here](https://docs.google.com/document/d/1oN8uVp0X6dJDNgbZuuwEoN9pRx6a43hob3GOVItfcQU/edit?usp=sharing)

<div align="center"><img src="https://github.com/Rive-001/DEA/blob/master/DEA_pipeline.png" width="600" height="400"></div>
<div align="center"><b>DEA pipeline</b></div>

## Summary

We developed a pipeline that could extract mRNA sequences bound by RBP from the reads data available at ENCODE. The API for this pipeline could be used by end-users to extract sequences from their experiments and compare it against the sequences available within ENCODE.

## Team

* [Rishi Verma](https://github.com/Rive-001)
*  Neel Mittal
*  Yuying Biyan
*  Zhiyun Gong
