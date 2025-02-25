# **Part 5. Phylogeny tree of N.granulosis repeats**

Laboratory journal: [Repeats_in_NG](https://colab.research.google.com/drive/15o07jAOu3WPyQiE7BMQPym3fBMT0K3Wm?usp=sharing)

## **Main Points**

- The study was conducted on the microsporidian *Nosema granulosis*.
- RepeatModeler and RepeatMasker results were used to extract "unknown" repeats.
- The repeats were clustered using CD-HIT, and a phylogenetic tree was built with cluster percentage information overlaid.
- Despite the overall low contribution of these clusters (~1% of the genome), two (the biggest) were selected for further analysis.
- **Cluster 3** occupies 1.08% of the genome: ORF detection using "any" start codons revealed a long ORF, which BLAST analysis identified as a *gypsy*-like retrotransposon. When restricting to ATG as the start codon, a shorter ORF was detected, corresponding to a pro-pol polyprotein.
- The second analyzed cluster (0.83% of the genome) did not yield interesting results in ORF analysis.

---

## **Introduction**

This study focuses on repeat analysis in the genome of the microsporidian *Nosema granulosis*. 
Raw data obtained from RepeatModeler and RepeatMasker were used to extract "unknown" repeats, which were subsequently clustered using CD-HIT. 
A phylogenetic tree was constructed, incorporating information on the percentage contribution of each cluster to the genome. Although the total contribution of clusters of repeats is relatively low (~1% for biggest), two clusters were selected for further investigation. 
Notably, Cluster 3 (1.08% of the genome) exhibited ORFs annotated as a *gypsy*-like retrotransposon (when allowing any start codon) or a pro-pol polyprotein (when using only ATG). The second cluster (0.83% of the genome) did not yield meaningful ORF results.

---

## **Methods**

**Plan**:

- Extract and prepare "Unknown" repeats.
- Filter out short sequences and simple repeats (>30% simple repeats based on TRF output).
  
  ```bash
  seqkit seq -g --min-len 150 ng_unknown_repeats.fa > ng_unknown_150.fa
  trf ng_unknown_150.fa 2 5 7 80 10 50 1000 -l 10 -d -h -m > trf_ng_solo.txt
  ```

- Cluster sequences using CD-HIT.
  
  ```bash
  cd-hit-est -i ng_filtered.fa \
           -o ng_filtered_cdhit \
           -c 0.80 \
           -n 4 \
           -d 0 \
           -M 16000 \
           -T 2
  ```

- Estimate cluster coverage.
- Perform sequence alignment with MAFFT.
  
  ```bash
  mafft --auto ng_plus_outgroup.fa > aligned_ng_outgroup.fasta
  ```

- Build a phylogenetic tree using IQ-TREE (LINE/CR1 as an outgroup).
  
  ```bash
  iqtree -s aligned_ng_outgroup.fasta -m TEST -bb 1000 -nt AUTO -o LINECR1_143,LINECR1_170,LINECR1_2_72
  ```

- Select "interesting" families and perform a BLAST test.

---

## **Results**

### **Phylogenetic Tree**

A phylogenetic tree was constructed for the "unknown" repeat clusters obtained after CD-HIT clustering. 
The tree includes additional information on the percentage contribution of each cluster to the *Nosema granulosis* genome. Two clusters were selected for more detailed analysis.

*Figure 1. Visualization of phylogeny tree*
<img width="960" alt="Снимок экрана 2025-02-17 в 22 41 28" src="https://github.com/user-attachments/assets/c6a6dbd0-7979-4cda-a059-f5f226946c95" />


### **Cluster 3 (1.08% of the genome)**

The representative sequence of this cluster, chosen via CD-HIT, was further analyzed for open reading frames (ORFs). When searching with "any" start codon, a relatively long ORF was found, which BLAST identified as a *gypsy*-like retrotransposon. 

Consesus sequence for cluster 3 (the only one sequence in this cluster):
```
>rnd-1_family-16#Unknown ( RepeatScout Family Size = 76, Final Multiple Alignment Size = 76, Localized to 1341 out of 1754 contigs )
CGAATCTCTTATATTACAAAGTTGATCATTAAGAGTTGTGTTTTGAATATCTATTGGGAG
ATTGTCATCTTCAATCCTTTCTTGATCTAAAAATTCGAAATTGCCAATATCCAAGATATC
CACGGGCTCTACAACTTCTATGTTTTCTTCTTCCGCTTCGTCAATTTCACAGATTGAGTC
TTCTATCACCATGCTTAGATGGTCTTCCTGCATTAAATCTCGTATNGGAGGACCAAANAN
CAANNCAAANGGTGTNTTGGATGTCGTAGNATGTCTCATANTATTATATGAATATGTNGC
ATCCTCTCTAACATTAGTCCATTTTCCAGGCGTATTTAAAGACATCAGCATGGAACCAAT
CATCCATTTNATNGTTTGATTTGCTCTTTCCACCTGNCCTTGTATCCACGGACANCTNGC
NCTNCCTCTNACATGTCTNACNTCGAACTCTTCAAGCATANNNNNCATTNGNTCATTGCA
AAATTCTCTTCCATTATCAGTATGCAACAGAAAACTTGGNCCANNAGTCATAAATATGGT
TTTAATAGCNGGAACAACCGCGGATGCNGATTTTTCTTTTAATGGAACGGTCCACATGTA
CTTAGAAAANGAGTCTACCACAACCAACATCCACTTANACCCATCGTTTACATCGCTGTA
ATATCTAAAATCAACTAGATCGGCAATATAACGTTCTCNNGGATGTATAGCAATGATGGG
TCTTATTATAGGCCTNGTAACTAGNGCTCTACGAGATTGACATATCTCACATCCATTTAC
CATATCAGATGTTTCCCTTGTTGTAATACCATATGCCTTTGATTTAAGGAAATGATAGAG
CCTATCTCTTCCAGCGTGTCCATTTTGAACGTGTATAAGAGTAATAAAATCTTTCTTGAA
NTGTTCTTCNTCAAGAGTAAAAAATCTTAAATACACATCAGGACCTCCTTTATATAACAA
CTGACTTTTTACAGTACAGTAGAAGAATTTAGATGCCCTTCTCTTAAATGACTTTAAATC
ATTAGAGGATACTATCCTAGCGGGATAGTTTCACACAACAACCACAGTATGATTTCNTCT
CTCTCCGAATTGGTAAGAATAATTCTCATTGGGCATAAAAAATTTTCAAAGAGAAAAGAA
CAAACCTCTGATGACAGAAATGTTTATATTGATACATAAATAAGCGTTACAAGATTCTTT
ATGTTCAAAACTTGACATACGGATTCTGACCTCTATTAACTGGAACCCCTATGAACTGTG
AC
```
**Any sense codon**

*Figure 2. Visualization of ORF analysis for Cluster 3 (any sense codon) and BLAST results*
<img width="1379" alt="Снимок экрана 2025-02-17 в 22 50 09" src="https://github.com/user-attachments/assets/9f371f5e-0979-46f5-8f41-84cb1f5db313" />
<img width="1247" alt="Снимок экрана 2025-02-17 в 22 52 39" src="https://github.com/user-attachments/assets/1607e959-131d-44b9-af11-2df1a1482a8a" />

**ATG only**

When restricting to ATG start codons, a shorter ORF was identified, showing strong similarity to a pro-pol polyprotein.

*Figure 3. Visualization of ORF analysis for Cluster 3 (ATG only) and BLAST results*
<img width="1373" alt="Снимок экрана 2025-02-17 в 22 59 46" src="https://github.com/user-attachments/assets/99a94a28-eb3c-4005-b907-04195f466ae6" />
<img width="1242" alt="Снимок экрана 2025-02-17 в 22 59 28" src="https://github.com/user-attachments/assets/d5b21002-2d72-4154-a722-2ca9d2152a33" />

*Table 1. BLAST results for longest ORF (ATG only)*
| Accession | Description                                                                 | Scientific Name                                  | Max Score | Total Score | Query Cover | E value | Per. Ident | Acc. Len |
|-----------|------------------------------------------------------------------------------|-------------------------------------------------|-----------|-------------|-------------|---------|------------|----------|
| P23074.3  | RecName: Full=Pro-Pol polyprotein; AltName: Full=Pr125Pol; Contains: RecName: Full=Protease/Reverse transcriptase/ribonuclease H; AltName: Full=p87Pro-RT-RNaseH; Contains: RecName: Full=Protease/Reverse transcriptase; AltName: Full=p65Pro-RT; Contains: RecName: Full=Ribonuclease H; Short=RNase H; Contains: RecName: Full=Integrase; Short=IN; AltName: Full=p42In [Macaque simian foamy virus] | Macaque simian foamy virus                      | 70.1      | 70.1        | 77%         | 2e-12   | 26.54%     | 1149     |
| O93209.1  | RecName: Full=Pro-Pol polyprotein; AltName: Full=Pr125Pol; Contains: RecName: Full=Protease/Reverse transcriptase/ribonuclease H; AltName: Full=p87Pro-RT-RNaseH; Contains: RecName: Full=Protease/Reverse transcriptase; AltName: Full=p65Pro-RT; Contains: RecName: Full=Ribonuclease H; Short=RNase H; Contains: RecName: Full=Integrase; Short=IN; AltName: Full=p42In [Feline foamy virus] | Feline foamy virus                              | 66.2      | 66.2        | 83%         | 4e-11   | 23.96%     | 1156     |
| P27401.2  | RecName: Full=Pro-Pol polyprotein; AltName: Full=Pr125Pol; Contains: RecName: Full=Protease/Reverse transcriptase/ribonuclease H; AltName: Full=p87Pro-RT-RNaseH; Contains: RecName: Full=Protease/Reverse transcriptase; AltName: Full=p65Pro-RT; Contains: RecName: Full=Ribonuclease H; Short=RNase H; Contains: RecName: Full=Integrase; Short=IN; AltName: Full=p42In [Simian foamy virus (TYPE 3 / STRAIN LK3)] | Simian foamy virus (TYPE 3 / STRAIN LK3)        | 65.1      | 65.1        | 77%         | 1e-10   | 25.00%     | 1143     |
| Q87040.1  | RecName: Full=Pro-Pol polyprotein; AltName: Full=Pr125Pol; Contains: RecName: Full=Protease/Reverse transcriptase/ribonuclease H; AltName: Full=p87Pro-RT-RNaseH; Contains: RecName: Full=Protease/Reverse transcriptase; AltName: Full=p65Pro-RT; Contains: RecName: Full=Ribonuclease H; Short=RNase H; Contains: RecName: Full=Integrase; Short=IN; AltName: Full=p42In [Pan troglodytes foamy virus] | Pan troglodytes foamy virus                     | 58.5      | 58.5        | 70%         | 1e-08   | 24.35%     | 1146     |
| P14350.2  | RecName: Full=Pro-Pol polyprotein; AltName: Full=Pr125Pol; Contains: RecName: Full=Protease/Reverse transcriptase/ribonuclease H; AltName: Full=p87Pro-RT-RNaseH; Contains: RecName: Full=Protease/Reverse transcriptase; AltName: Full=p65Pro-RT; Contains: RecName: Full=Ribonuclease H; Short=RNase H; Contains: RecName: Full=Integrase; Short=IN; AltName: Full=p42In [Human spumaretrovirus] | Human spumaretrovirus                           | 56.2      | 56.2        | 70%         | 9e-08   | 24.87%     | 1143     |


### **Second Cluster (0.83% of the genome)**

The ORF analysis for the second cluster did not yield interesting results. The detected ORFs were short and did not allow for a clear functional hypothesis.

Consesus sequence for cluster 2 (the only one sequence in this cluster as well):
```
>rnd-1_family-28#Unknown ( RepeatScout Family Size = 56, Final Multiple Alignment Size = 56, Localized to 1341 out of 1754 contigs )
CCTTTCCATGNACATATTACCTCGTTTTCCTCTTTTCTGATAGTTTTTCATTTGATGAGC
AAAAGAAACAAGATTTAAGTTGTTTNTCTCTCATTTTTTCNACTATCTCTTTCAATTCTT
TCTTACTCAACTTTTGAAAATTCATTTTTAGGGGTATTTTTTTTAAAAAAAATATTTATA
CTGAAAACGGGGGCAAGTCCTCCGAATGCTCCTTATATTCTTACATTTATCAAGATTATA
TTTTGAATCTTGTATAAATTTTTCTTTAGTCTTAAAAATATCATGGATCGTCAATAAAGG
TGTATTATGCGCAATACGTAGCTACTCGAGGGTTTTGTTTATCTTTTTTATCTACTTTTA
GACCAATAGGCAACCTCTGTATAATTGTTTTTTTTTAAGCTGCCGACATTTTTGGGTATG
AATAATAAAAAATATTTCCGATATCGAGAAACATGAATTNCGTTATTTTTAAGTAACAAA
CATATCATAAATCCCGAAAGAGCAAATAANTTGACGAATTTTTCCGTTATNGTGTATTTC
GGTATTAAGAGGGATAACTGTATATGTTCCCATGAATCATTATTTTACCACACGAATTTC
AATTAATTATGTATAAGAAATAATCACAGCGTCTGTAAAACAGCAATCTTAAATTATGAA
CCTGATACCAAAACATTGGTCGAAAGGATGTTGCTTTCNTATTAAAAACTTTTAAGTAAT
TTATAAGGTGGCTCATTACATATCTAAAAAAAGATAAAATTTATTAAATGGCACACAGTC
AAAAAGGTTCGCAATCCTTGGTCTACGATAAGATTANAAAAAAATTCTATCATCGAAGTC
AAAATTCTCCCTTGATACGCNCAAATCCGTAGCGTAGGAGAAGCTAAGGATGTATGATTN
GATAGCAGCTGAAGTAAGNATGATGTACAAGTGTATAGTAAAAATTATACCATACGTTAT
GACATGGGATTTTGTGTGGCAAAATTTCACAAAAAACATTTTAGTTTACTTAATTTGTTA
ACGAGNACCAAAATTTGCACCCAAATCAGTCCTTAAGAAAGCTTTCAAAAGTATTTTTTT
CATATCAGGAAGGAGACACTGGTTTTAGAGAAACAGACGAAATAGCGAGGAGGTACAATA
ATGTTTAAGACCCTACTACTCGGATGCTCCAATTTTTACTTTTTAGACATAGCCTATCAT
GGAGCTTTAATAAACTTAAATAAAAGATAAATTTAAAATGAGATGAACTTTAACTTAGGT
TATTTGNGTTATATATCTTACCATTGTGTTAAAACGTATTCAAGCATT
```
*Figure 4. Visualization of ORF analysis for Cluster 2 (ATG and alternative codons)*
<img width="1379" alt="Снимок экрана 2025-02-17 в 22 55 22" src="https://github.com/user-attachments/assets/03d2cdfb-827f-4153-8d5e-1bc21e5ed2d0" />

---

## **Conclusion**

Repeat analysis in the *Nosema granulosis* genome using RepeatModeler, RepeatMasker, and CD-HIT enabled the construction of a phylogenetic tree with cluster percentage contributions. 
Although the cluster repeat content was low (~1%), the selected clusters provide potential insights for further study. Cluster 3 (1.08% of the genome) is particularly notable, as different ORF detection strategies revealed elements similar to *gypsy* retrotransposons or pro-pol polyproteins. 
The second cluster (0.83% of the genome) did not show significant results, requiring further investigation to clarify its role in the *Nosema granulosis* genome.
