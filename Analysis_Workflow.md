# RNASeq Analysis worflow for LiverObese project

## Description

The aim of the project is to collect the most wide transcriptome expression data for Liver samples.



## Formatting the data

### Sample ID

```
ls *.gz | sed 's/_/\t/' | cut -f1 | sort | uniq > SampleSequencing.id
```


## Metrics

### RNASeq Metrics with picard tools

Script: ```RNAseq_metrics.pbs```

Check the results

```
cd /gpfs/work/uMI17_MedVaP/LiverObeseRNASeq/Analisi/RNAseq_metrics_picard
cat <(grep PF R100.HQ.RNAmetrics) <(grep "PF" -A 1 *RNAmetrics | sed '/PF_BA/d;/--/d') | column -t | less -S
```
