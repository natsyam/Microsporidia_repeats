# **Part 3. Phylogeny tree of repeats**

[laboratory journal](https://colab.research.google.com/drive/11DVFrSG88UEFJSD8tNy8TVvt0u01eTQl?usp=sharing)

## **Introduction**

In the current part of the study, we expanded the approach by examining the phylogenetic relationships among repeats. To do this, a phylogenetic tree was constructed based on the repeats common to the parasitic microsporidia (Dictocoela muelleri and Nosema granulosis) and their host (Gammarus roeselli). Data on the percentage of the genome occupied by each of these repeats was also incorporated into the tree, allowing us to assess their contribution to the overall genome structure.
 
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

A phylogenetic tree for parasite repeats similar to the host repeats was obtained. On the left is the version where branch lengths are ignored, and on the right is the variant with accurately represented branch lengths.

*Figure 1. Visualization of phylogeny tree*
<img width="1139" alt="Снимок экрана 2025-02-17 в 10 58 58" src="https://github.com/user-attachments/assets/9b238b33-1afb-4ed5-a6ad-f713e4e5a300" />

The visualization of the tree alignment does not appear particularly optimal, which is most likely due to the use of different types of repeats in a single analysis.

*Figure 2. Visualization of alignment*
<img width="1367" alt="Снимок экрана 2025-02-16 в 00 57 09" src="https://github.com/user-attachments/assets/3427f13d-d05f-4bb6-873e-25d62c3af9b1" />

Additionally, the tree was supplemented with data on the percentage of the genome occupied by each repeat.

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

## **Conclusion**

The resulting phylogenetic tree turned out to be unrooted, as it was unclear what to use as an outgroup given that entirely different groups of repeats were used to build the tree. Interestingly, not all LINE/CR1 repeats clustered together, which might indicate potential misclassification. However, a distinct clade can be observed that corresponds to the one obtained using CD-hit, where repeats from all three organisms are present, although their overall contribution is rather insignificant.


