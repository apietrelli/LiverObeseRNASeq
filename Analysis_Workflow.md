# RNASeq Analysis worflow for LiverObese project

## Project description

The aim of the project is to collect the most wide transcriptome expression data for Liver samples.

All the samples are **obese** patients mainly **female** patient.

The information about other clinical/genetic information are stored in a XLS file created by Marica.

### RNASeq Sequencing

RNA was extracted from (type of cells).


| Feature     | Value     |
| :------------- | :------------- |
| Service       | Novogene       |
|Sequencing type|RNASeq Unstranded|
|Depth of coverage | > 20M reads (pairs)|
|Samples|150|


There were some **RNA extraction issue** for several samples and the quality for the sequencing did not satisfy the standard sequencing protocol.

We decided to **go over it and do the sequencing** even for the under quality samples.

Probably we will see some problems in the sequencing yield and quality during the analysis step. Some samples would be discarded.

## Analysis workflow

-- Description; workflow

### Formatting the data

### Get Sample ID list

```shell
ls *.gz | sed 's/_/\t/' | cut -f1 | sort | uniq > SampleSequencing.id
```

## Metrics

### RNASeq Metrics with picard tools

Script: ```RNAseq_metrics.pbs```

Check the results

```shell
cd /gpfs/work/uMI17_MedVaP/LiverObeseRNASeq/Analisi/RNAseq_metrics_picard
cat <(grep PF R100.HQ.RNAmetrics) <(grep "PF" -A 1 *RNAmetrics | sed '/PF_BA/d;/--/d') | column -t | less -S
```

## Differential expression

### Selecting only Protein Coding genes
```R
g=readGFF("Data/Homo_sapiens.GRCh37.75.gtf")
primary_genes = g %>%
    filter(type=="gene") %>%
    filter(source == "protein_coding") %>%
    filter(seqid %in% c(seq(1:22),"X","Y")) %>%
    select("gene_id")
saveRDS(primary_genes, "../Data/Homo_sapiens.GRCh37.75.PrimaryProteinCodingGenes.rds")
```

# PCSK7

Follow the protocol from this article:

[https://www.ncbi.nlm.nih.gov/pmc/articles/PMC4631051/](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC4631051/)

See protocol 7:

```
Alternate Protocol 7: Mapping RNA-seq reads, generating output in transcriptomic coordinates and using RSEM to quantify expression of transcripts and genes
```
