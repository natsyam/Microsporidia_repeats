# **Part 6. Investigation of D.muelleri repeats**

Laboratory journal: [Single_repeat_in_DM](https://colab.research.google.com/drive/1sFXeP8YB5RnrjCHItEoXzn0n5LPJpg9C?usp=sharing)

## **Main Points**

- **Repeat Identification:** De novo repeat identification was performed using RepeatModeler, and redundant sequences were clustered, domain prediction (minimum 300 nucleotides) and BLAST homology searches were conducted.
- **rnd-1_family-3 Analysis:** A detailed analysis of the rnd-1_family-3 repeat was performed, including homology searches (721 hits found). No TSDs (Target Site Duplications) were detected.
- **Classification of rnd-1_family-3:** TE-Aid classified rnd-1_family-3 as RC/Helitron, but this classification has low statistical reliability and requires further confirmation.
- **Unknown Repeats with ORFs:** Domains such as Integrase_H2C2, HTH_Tnp_Tc5, FLYWCH, and gag-asp_proteas were identified in unknown repeats with ORFs, the number of BLAST hits for these unknown repeats with ORFs was low (less than 10), suggesting a need for further investigation.

## **Introduction**

This study focuses on the analysis of repeats found in the D. muelleri genome. The repeats were identified de novo using RepeatModeler, followed by clustering to eliminate redundancy. Further analysis included domain prediction with a minimum length constraint of 300 nucleotides and a BLAST homology search against the parasite genome to determine the number of repeat copies present.

Based on the obtained data, a final table was compiled containing information from RepeatModeler, including: Name, Order, Superfamily, Family_Size, MSA_Size, Localized_Contigs, Total_Contigs. Additionally, the table included: Length in nucleotides, Number of good BLAST hits, Number of Pfam conserved domains.

For further analysis and manual classification of repeats, the following selection criteria were proposed:
1. Presence of at least one TE-related conserved protein domain.
2. Sequence length within the expected TE family range, approximately between 1 and 10 kb.
3. At least 10 high-quality BLAST hits in the genome.

## **Methods**

1. **Repeat Identification**:
   - Use of RepeatModeler for *de novo* repeat detection.
   - Clustering of repeats to remove redundancy.
```
BuildDatabase -name d_muelleri_rm_db genomes_ms/d_muelleri_up.fna
RepeatModeler -threads 40 -database d_muelleri_rm_db > d_muelleri_rm.log

cd-hit-est -i dm_consensi.fa.classified -o reduced.fa -d 0 -aS 0.8 -c 0.8 -G 0 -g 1 -b 500
```
2. **Sequence Analysis**:
   - Domain prediction with a 300-nucleotide constraint.
   - Homology search using BLAST against the parasite genome.
   - Compilation of a final table with repeat annotations.
```
getorf -sequence reduced.fa -outseq reduced300.orf -minsize 300
pfam_scan.pl -fasta reduced300.orf -dir /content/Pfam_db -outfile reduced300.pfam
```
3. **In-depth Analysis of a Specific Repeat**:
   - Selection of repeat element *rnd-1_family-3#Unknown* for detailed analysis.

| Name                   | rnd-1_family-3 |
|------------------------|---------------|
| Order                 | Unknown       |
| Superfamily           | NA            |
| Length in nucleotides | 658           |
| Family_Size           | 1464          |
| Number of good BLAST hits | 697     |
| MSA_Size              | 100           |
| Localized_Contigs     | 9327          |
| Total_Contigs         | 11027         |
| Number of Pfam conserved domains | 0 |

4. **Homology Search and Repeat Boundary Definition**:
   - Homology search of this repeat in the genome revealed 721 BLAST hits.
   - Sequences were extended by 1000 nucleotides on both sides for more accurate boundary determination.
   - Selection of the 50 longest sequences and 150 random ones for further alignment.
   - Alignment using MAFFT + T-Coffee for gap filtering.
   - No TSD was detected in the alignment analysis.
5. **Consensus Sequence Determination**:
   - Use of *cons* from EMBOSS to generate the consensus sequence.
   - Application of HMMER to analyze variability at each position.
```
cons -sequence /content/rnd1_fam3_tcoffee.aln -outseq rnd1_fam3.cons
hmmbuild hmmout.stk /content/rnd1_fam3_tcoffee.aln
```
6. **Repeat Classification**:
   - TE-Aid analysis classified the sequence as RC/Helitron based on the predicted ORF.
   - However, BLAST annotation results had low statistical reliability (*p-value* too high), requiring further confirmation.
```
./TE-Aid -T --min-orf 150 -q /content/rnd1_fam3.fasta -g d_muelleri_up.fna -o TE_aid_out3
```
---

## **Results**

### **Repeat Selection Based on Clustering Results**

After clustering the repeats obtained de novo using RepeatModeler, as well as analyzing the ORFs (Open Reading Frames) and the number of hits in the genome (based on BLAST results), a final table was compiled. From this table, the following were selected: repeats with a high number of hits (Table 1), unknown repeats in which ORFs were found (Table 4).

*Table 1. Repeats with a high number of hits*

| Name               | Order   | Superfamily | Length in nucleotides | Family_Size | Number of good BLAST hits | MSA_Size | Localized_Contigs | Total_Contigs | Number of Pfam conserved domains |
|---------------------|---------|----|---------|---------|---------|---------|---------|---------|---------|
| rnd-1_family-3      | Unknown | NA | 658     | 1464    | 697     | 100     | 9327    | 11027   | 0       |
| rnd-1_family-39     | Unknown | NA | 525     | 323     | 701     | 90      | 9327    | 11027   | 0       |
| rnd-1_family-5      | Unknown | NA | 642     | 1396    | 692     | 100     | 9327    | 11027   | 0       |
| rnd-1_family-246    | Unknown | NA | 547     | 80      | 691     | 79      | 9327    | 11027   | 0       |
| rnd-1_family-423    | Unknown | NA | 433     | 50      | 690     | 50      | 9327    | 11027   | 0       |
| rnd-1_family-219    | Unknown | NA | 351     | 87      | 602     | 83      | 9327    | 11027   | 0       |
| rnd-1_family-70     | Unknown | NA | 698     | 193     | 152     | 100     | 9327    | 11027   | 0       |
| rnd-1_family-51     | Unknown | NA | 658     | 246     | 131     | 100     | 9327    | 11027   | 0       |
| rnd-1_family-78     | Unknown | NA | 515     | 179     | 129     | 100     | 9327    | 11027   | 0       |
| rnd-1_family-1036   | Unknown | NA | 295     | 20      | 110     | 20      | 9327    | 11027   | 0       |
| rnd-1_family-34     | Unknown | NA | 684     | 364     | 106     | 100     | 9327    |11027   |0       |
| rnd-1_family-37     |Unknown |NA |312     |331     |104     |98      |9327   |11027   |0       |
| rnd-1_family-30     |Unknown |NA |306     |391     |103     |100     |9327   |11027   |0       |
| rnd-1_family-7      |Unknown |NA |2767    |1068    |35      |100     |9327   |11027   |0       |

---

**Detailed Analysis of the *RND-1_FAMILY-3* Repeat**

Particular attention was given to the analysis of the *rnd-1_family-3* repeat, which in previous studies constituted a significant portion of the genome (about 15%). However, in the current analysis, the number of hits found using BLAST was lower than the family size value provided by RepeatModeler (Table 3).

*Table 2. rnd-1_family-3 repeat information*

| Name               | Order   | Superfamily | Length in nucleotides | Family_Size | Number of good BLAST hits | MSA_Size | Localized_Contigs | Total_Contigs | Number of Pfam conserved domains |
|--------------------|---------|-------------|------------------------|-------------|----------------------------|----------|--------------------|---------------|----------------------------------|
| rnd-1_family-3     | Unknown | NA          | 658                    | 1464        | 697                        | 100      | 9327              | 11027         | 0                                |


The alignment did not show the presence of TSD (Target Site Duplication), which are typically used as a marker for repeat classification.

*Figure 1. Alignment results of the rnd-1_family-3 repeat.*
<img width="1029" alt="Снимок экрана 2025-03-08 в 15 28 29" src="https://github.com/user-attachments/assets/f4eed598-9169-4338-b355-50e2646555b2" />


**Analysis Using TE-Aid**

The program TE-Aid conducted a comprehensive analysis of the repeat sequence. The following are a summary of the steps and results:

*Figure 2.1 Genome hits (horizontal lines), located relative to the consensus sequence (X-axis), divergence degree (Y-axis).*
*Figure 2.2 Pileup of hits relative to the consensus.*
*Figure 2.3 Self dot-plot.*
*Figure 2.4 ORFs, matches with TE proteins.*
<img width="755" alt="Снимок экрана 2025-03-10 в 14 01 03" src="https://github.com/user-attachments/assets/5b754e86-9108-4731-a7b5-fc320faac293" />

*Table 3. Classification results for EMBOSS_001 repeat.*

| Name          | Class               | Domain                     | Percent Similarity | Length of Match | Mismatches | Gap | Start1 | End1 | Start2 | End2 | p-value | Score |
|---------------|---------------------|---------------------------|--------------------|------------------|------------|-----|--------|------|--------|------|---------|-------|
| EMBOSS_001_1  | RC/Helitron         | Helitron-1_NV_hel         | 42.857             | 28               | 16         | 0   | 57     | 84   | 2248   | 2275 | 0.65    | 28.5  |

```
>EMBOSS_001_1 [181 - 441] Helitron-1_NV_hel
WXFHEFLFFTTFCRDASPHSSPHLGESLLLHCHIRPSLNQLYHTGTTVXLYYNYIXYDRL
MSFPHYLLKSDVSGIRTTILKFYIQEC
```
**Biology of Helitron (Rolling-Circle Mechanism)**

*RC/Helitron* refers to transposons that use the Rolling-Circle mechanism for replication. This process includes:

- Initiation by nicking one strand of DNA by the Rep protein.
- Replication with strand displacement.
- Formation of a circular intermediate.
- Integration into a new genomic site.

Helitron Features:

- Gene and other sequence capture.
- Contribution to genome evolution through mobility.
- Presence in centromeres and other genomic regions.

---

### **Unknown Repeats with ORFs (Domain Analysis)**

Among the repeats with predicted ORFs (Table 5), the following domains were identified:

* Integrase_H2C2
* HTH_Tnp_Tc5
* FLYWCH
* gag-asp_proteas

*Table 4. Unknown repeats with identified ORFs and their domains.*

| Name                | Order   | Superfamily | Length in nucleotides | Family_Size | No of good blast hits | MSA_Size | Localized_Contigs | Total_Contigs | No of Pfam conserved domains | Domain             |
|---------------------|---------|----|---------|---------|---------|---------|---------|---------|---------|---------------------|
| rnd-1_family-15     | Unknown | NA | 576     | 497     | 6       | 100     | 9327    | 11027   | 1       | HTH_Tnp_Tc5         |
| rnd-1_family-134    | Unknown | NA | 1452    | 122     | 5       | 100     | 9327    | 11027   | 1       | rve                 |
| rnd-1_family-196    | Unknown | NA | 442     | 95      | 3       | 95      | 9327    | 11027   | 1       | FLYWCH              |
| rnd-1_family-358    | Unknown | NA | 778     | 58      | 2       | 58      | 9327    | 11027   | 1       | Integrase_H2C2      |
| rnd-1_family-379    | Unknown | NA | 1423    | 55      | 3       | 54      | 9327    | 11027   | 1       | rve                 |
| rnd-1_family-678    | Unknown | NA | 327     | 32      | 3       | 32      | 9327    | 11027   | 1       | FLYWCH              |
| rnd-1_family-944    | Unknown | NA | 531     | 22      | 9       | 22      | 9327    | 11027   | 1       | FLYWCH              |
| rnd-1_family-1074   | Unknown | NA | 810     | 19      | 4       | 19      | 9327    | 11027   | 1       | FLYWCH              |
| rnd-1_family-1241   | Unknown | NA | 373     | 15      | 7       | 15      | 9327    | 11027   | 1       | HTH_Tnp_Tc5         |
| rnd-1_family-1260   | Unknown | NA | 377     | 15      | 7       | 15      | 9327    |11027   |1       |FLYWCH              |
| rnd-3_family-439    |Unknown |NA |1747    |27      |5       |16      |NA     |NA     |1       |gag-asp_proteas     |


- **Integrase_H2C2** — integrase, an enzyme for integrating viral DNA, contributes to the formation of repeats.

- **HTH_Tnp_Tc5** — transposase that recognizes specific DNA regions and moves transposons.

- **FLYWCH** — motif involved in DNA regulation and protein interactions.

- **gag-asp_proteas** — a protein with protease activity that may participate in processes related to repeats and viral elements.

> **Important**: The number of hits in the genome for these repeats turned out to be small (less than 10), so their significance requires further study.

## Conclusion
This study identified and analyzed repeats in the *D. muelleri* genome. Special attention was given to the *rnd-1_family-3* repeat, which is present in significant amounts in the genome. Alignments and classification analyses preliminarily assigned it to the RC/Helitron family, but final confirmation requires additional research. Future work will focus on more detailed structural analysis and functional annotation of the repeats.

