# **Part 3. Phylogeny tree of repeats**

## **Introduction**

Microsporidia are intracellular parasites characterized by compact genomes and significant variation in genome size. One of the hypotheses proposed to explain this diversity is the possibility of horizontal transfer of repeats from the host to the parasite. In this study, we examine the hypothesis that parasites—specifically, microsporidia—may acquire repeats from their hosts, potentially contributing to changes in their genome sizes. To test this hypothesis, the genomes of two microsporidia parasitizing the same host, as well as that of the host itself, were analyzed. The organisms under investigation were *Dictocoela muelleri* and *Nosema granulosis* as representatives of the parasites, and *Gammarus roeselli* as the host.
 
## **Methods**

**Plan**:

- Extracting and preparing "Unknown" repeats
- Filtering of short sequences and simple repeats (SSR)
- Clusterization (CD-HIT)
- Alignment (MAFFT)
- Building a tree (IQ-TREE)
- Cluster coverage estimation
- Selection of "interesting" families and a BLAST test on a small subset

## **Results**

*Figure 1. Visualization of alignment*
<img width="1366" alt="Снимок экрана 2025-02-16 в 17 33 37" src="https://github.com/user-attachments/assets/699a456a-edd2-4deb-8bba-b1c246df3205" />

LINE/CR1 was taken as an outgroup.

*Figure 2. Visualization of phylogeny tree*
<img width="759" alt="Снимок экрана 2025-02-17 в 11 21 43" src="https://github.com/user-attachments/assets/7380d27e-d520-4c5e-9570-7fcbd7dffc8e" />

*Figure 3. Visualization of phylogeny tree (circle variant)*
<img width="829" alt="Снимок экрана 2025-02-17 в 11 22 05" src="https://github.com/user-attachments/assets/e8c96d26-1eec-4316-a06e-e2de07df0652" />

But i took the consensus for the cluster 92 (~15% of the genome), so it'd be better to check what is also in the cluster.
```
>rnd-1_family-3#Unknown ( RepeatScout Family Size = 1464, Final Multiple Alignment Size = 100, Localized to 9327 out of 11027 contigs )
ATATATATTACATGTTGACAACATCCATAGCTGCCAACCCGGAGAGTTGTCTCCTACCGT
GGTCTGTGACCTTTGGTTCTTGGTGTTCCAATAATACGTCACTTCCTAAGCTACCCAGAA
GCCCAGCTGTATACGCGATTTTCGTTTTATCAATGACTCAGCAGGATACAGGTAATTAGT
GGCTTTTCATGAATTTTTATTTTTCACTACTTTTTGCCGAGATGCGTCGCCGCACTCATC
CCCACACCTAGGAGAGTCCCTTCTGCTTCATTGTCATATTAGACCAAGTCTTAATCAGCT
ATACCACACTGGAACAACTGTATATTATACTATAATTATATAGTTNTGACCGCTTAATGT
CATTCCCTCATTATTTATTAAAGAGTGACGTCAGCGGGATTCGAACCACGATACTTAAAT
TTTACATTCAAGAGTGTTAACCACTGAGCTATCTGGCCCCTTAAATATTGTTTAAATCTA
TAATACTCTATAATAAATGTGTATAAGCTTGAAAGAAATGGGTCTATAACTTTGGAAAAA
TAGGTTTATAACTATGAAAAGCCCGTATAAAAGACGACTTGGTCTAATTGAAAATAGAAC
AGAATAGCTCTTTGAGAGTGGACATAAGACGGCGACACATTAAGCAAAACATAGTGAA
```

*Figure 4. ORFs that was found in rnd-1_family-3#Unknown*
<img width="1328" alt="Снимок экрана 2025-02-16 в 19 08 46" src="https://github.com/user-attachments/assets/7ab5b2d2-676f-4d09-8abc-e7db294b9fa7" />
