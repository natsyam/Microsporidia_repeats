# **Part 3. Phylogeny tree of repeats**

## **Introduction**

Microsporidia are intracellular parasites characterized by compact genomes and significant variation in genome size. One of the hypotheses proposed to explain this diversity is the possibility of horizontal transfer of repeats from the host to the parasite. In this study, we examine the hypothesis that parasites—specifically, microsporidia—may acquire repeats from their hosts, potentially contributing to changes in their genome sizes. To test this hypothesis, the genomes of two microsporidia parasitizing the same host, as well as that of the host itself, were analyzed. The organisms under investigation were *Dictocoela muelleri* and *Nosema granulosis* as representatives of the parasites, and *Gammarus roeselli* as the host.
 
## **Methods**

1. Determine similar sequences using a blast with a threshold about the same as the repitmasker was on kimuraplot to get all repeats out 
```
blastn -query dm_consensi.fa.classified.renamed -db host_db -perc_identity 55 -out dm_vs_host.tsv -evalue 1e-3 -outfmt "6 qseqid sseqid pident length evalue bitscore"
blastn -query ng_consensi.fa.classified.renamed -db host_db -perc_identity 55 -out ng_vs_host.tsv -evalue 1e-3 -outfmt "6 qseqid sseqid pident length evalue bitscore"
```
2. Merge the sequences for 2 parasites and a host, select unique sequences to avoid repettiton and extract sequences for them to align them afterwards
```
cat dm_vs_host.tsv ng_vs_host.tsv > combined.tsv
extract_fasta.py --tsv combined.tsv --fasta combined_consensi.fa --output output.fasta
```
3. Align sequences with the help of the MAFFT
```
mafft --auto /content/output.fasta > /content/aligned.fasta
```
4. Constract the phylogeny tree with the help of IQtree
```
iqtree -s /content/aligned.fasta -m TEST -bb 1000 -nt AUTO
```

## **Results**

*Figure 1. Visualization of phylogeny tree*
<img width="1139" alt="Снимок экрана 2025-02-17 в 10 58 58" src="https://github.com/user-attachments/assets/9b238b33-1afb-4ed5-a6ad-f713e4e5a300" />

*Figure 2. Visualization of alignment*
<img width="1367" alt="Снимок экрана 2025-02-16 в 00 57 09" src="https://github.com/user-attachments/assets/3427f13d-d05f-4bb6-873e-25d62c3af9b1" />

*Figure 3. Visualization of phylogeny tree with percentage of the genome each repeat occupy*
<img width="1314" alt="Снимок экрана 2025-02-16 в 02 29 55" src="https://github.com/user-attachments/assets/d6c54d38-f340-472d-805c-0a5f9ed16433" />

*Table 1. Cluster 23 from CD-Hit*
| cluster_id | seq_name                                    | fam_size | cons_len | total_bp |
|------------|---------------------------------------------|----------|----------|----------|
| 23         | d_muelleri_rnd-1_family-1045#LINE/CR1     | 20       | 491      | 9820     |
|            | d_muelleri_rnd-1_family-1139#LINE/CR1     | 17       | 588      | 9996     |
|            | n_granulosis_rnd-1_family-104#LINE/CR1    | 27       | 224      | 6048     |
|            | n_granulosis_rnd-1_family-143#LINE/CR1    | 21       | 527      | 11067    |
|            | n_granulosis_rnd-1_family-158#LINE/CR1    | 20       | 86       | 1720     |
|            | n_granulosis_rnd-1_family-160#LINE/CR1    | 20       | 233      | 4660     |
|            | n_granulosis_rnd-1_family-167#LINE/CR1    | 20       | 151      | 3020     |
|            | n_granulosis_rnd-1_family-170#LINE/CR1    | 19       | 281      | 5339     |
|            | n_granulosis_rnd-1_family-186#LINE/CR1    | 18       | 193      | 3474     |
|            | n_granulosis_rnd-2_family-72#LINE/CR1     | 20       | 1039     | 20780    |
|            | **host_rnd-1_family-11#LINE/CR1**              | 403      | 2041     | 822523   |
|            | host_rnd-1_family-14#LINE/CR1              | 380      | 3824     | 1453120  |


