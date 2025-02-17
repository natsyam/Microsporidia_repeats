# **Part 2. Microsporidia_repeats**

**Laboratory journals:**

[Part 1. Host DB](https://colab.research.google.com/drive/1ecwUyJ3eySWaThJAYqe-W5jgIK0e5q0Y?usp=sharing)

[Part 2. TRF](https://colab.research.google.com/drive/1Vxq8kZDsPDLfZRLhjDhqolMdON9RYUVV?usp=sharing)

## **Introduction**

Microsporidia are intracellular parasites characterized by compact genomes and significant variation in genome size. One of the hypotheses proposed to explain this diversity is the possibility of horizontal transfer of repeats from the host to the parasite. In this study, we examine the hypothesis that parasites—specifically, microsporidia—may acquire repeats from their hosts, potentially contributing to changes in their genome sizes. To test this hypothesis, the genomes of two microsporidia parasitizing the same host, as well as that of the host itself, were analyzed. The organisms under investigation were *Dictocoela muelleri* and *Nosema granulosis* as representatives of the parasites, and *Gammarus roeselli* as the host.
 
## **Methods**

The analysis began with a **de novo** search for repeats in the genomes of both the host and the parasites using RepeatModeler and RepeatMasker. Subsequently, a comparative assessment of the identified repeats was performed using BLAST, which allowed evaluation of the similarity between the parasite repeats and the host repeat library and the calculation of their contribution to the parasite genomes. Initial results indicated that the contribution of repeats similar to those in the host was extremely low—less than 1%.

Next, an approach based on using the repeat library identified in the host was applied to annotate the parasite genomes with RepeatMasker. Based on the obtained data, Kimura plots were constructed to evaluate the distribution of repeats by divergence. This analysis allowed us to compare the relative age of the integrated elements in the microsporidia genomes.

In addition to the analysis of overall repeats, a separate search for tandem repeats (TRF) was conducted for *Dictocoela muelleri* using Tandem Repeats Finder (TRF). The TRF results were compared with the RepeatMasker annotation to assess the degree of overlap and to identify novel elements not represented in the RepeatModeler libraries.

For visualization of the repeat distribution along the genome, the IGV program was used. However, given that the genome assembly did not reach chromosomal level, the visualization was not sufficiently convenient for detailed analysis.

## **Results**

**Host repeats database + parasites**

The initial analysis using BLAST revealed that the contribution of repeats similar to the host elements to the microsporidia genomes is less than 1%. This indicates an absence of widespread horizontal transfer of repeats from the host to the parasite.

| Species       | Unknown Repeat % | LINE/CR1 Repeat % |
|---------------|------------------|-------------------|
| d_muelleri    | 0.119512         | 0.047269          |
| n_granulosis  | 0.018082         | 0.453435          |

Subsequent analysis using RepeatMasker and construction of Kimura plots produced the following results. In the genome of *Dictocoela muelleri*, the overall repeat content exceeded 8%, of which approximately half consisted of nearly simple (presumably tandem) repeats, typical for many organisms, while the remaining repeats were unclassified. The distribution of repeats by divergence showed that the majority of elements fall within the 15–30% divergence range, indicating their ancient origin.

The results obtained indicate that the hypothesis of extensive horizontal transfer of repeats from the host to microsporidia is not supported. The low contribution of repeats similar to the host library (about 4%), along with the predominance of repeats with high divergence (15–30%), suggests that the majority of the integrated elements are ancient. This may mean that these repeats were either acquired before a long time ago or represent false-positive annotations during the repeat identification process.

*Figure 1. Visualization of repeat landscapes using Kimura Plots for Dictocoela muelleri*
<img width="1357" alt="Снимок экрана 2025-02-09 в 13 24 37" src="https://github.com/user-attachments/assets/3e78c38b-c44a-4565-b143-8002f815039e" />

In the genome of *Nosema granulosis*, the repeat content similar to the host's one was about 3%. Here, the distribution of repeats along the Kimura axis exhibited a peak at around 10–15% divergence, and elements with low divergence (K < 5) were extremely rare. This suggests that active transposition from host is either very limited or absent in recent evolutionary times.

*Figure 2. Visualization of repeat landscapes using Kimura Plots for Nosema granulosis*
<img width="1357" alt="Снимок экрана 2025-02-09 в 13 24 19" src="https://github.com/user-attachments/assets/42b3125e-5a89-417b-8f26-7d77a860d70d" />
<img width="1352" alt="Снимок экрана 2025-02-09 в 13 23 57" src="https://github.com/user-attachments/assets/ebe7fb06-bd23-41aa-9d88-9f189c5a683b" />

**Analysis of tandem repeats (TRF)**

A separate analysis of tandem repeats in the *D. muelleri* genome, performed using TRF, showed that tandem repeats occupy 9.16% of the genome. The total number of TRF-detected repeats was 45,733, of which 30,270 (66.19%) overlapped with the RepeatMasker annotation, while the remaining 15,463 repeats were novel. The total length of TRF repeats was 4,542,284 bp, with 3,414,238 bp (75.17%) matching the RepeatMasker results.

| Metric                                            | Value            |
| -------------------------------------------------- | ---------------- |
| Percentage of genome occupied by tandem repeats (TRF) | 9.16%            |
| TRF repeats overlapping with RepeatMasker          | 30270 (66.19%)   |
| Length of TRF repeats overlapping with RepeatMasker (bp) | 3414238 (75.17%) |

Visualization of the repeat distribution using IGV confirmed the general trends; however, the low quality of the genome assembly limited the detail of the analysis. Due to the genome assembly not reaching chromosomal level, visualization via IGV was limited. It is necessary to consider alternative visualization methods that would allow a clearer representation of the repeat distribution across the genome.

**Combined repeats visualization**

*Figure 3. Repeat distribution using IGV for D. mueller. Pink track is for RM repeats, green is TRF repeats and blue is genes annotation*
<img width="964" alt="Снимок экрана 2025-02-09 в 22 25 21" src="https://github.com/user-attachments/assets/7adf0838-2d04-49fd-82d0-c11665564b14" />


## **Future Plans**

- **Multi-step Execution of RepeatMasker:**
  - Try the method described in the [Harvard professor's tutorial](https://darencard.net/blog/2022-07-09-genome-repeat-annotation/), which involves multiple runs of RepeatMasker using different repeat libraries [+manual TE curation guide](https://link.springer.com/article/10.1186/s13100-021-00259-7).
  - **Goal:** Reduce the percentage of "unknown" repeats and provide a more detailed characterization of the remaining elements.

- **Search for Primate-Specific Repeats:**
  - Check for the presence of Alu and SVA repeats in the genomes of microsporidia that parasitize humans, as these repeats are considered primate-specific.

- **Phylogenetic Analysis of Repeats:**
  - Consider using GPAC (or similar programs) to construct a phylogeny of repeats.
  - Optionally, perform a similar analysis on a set of microsporidia to evaluate the evolutionary relationships among their repeat elements.
 [Example from the article](https://link.springer.com/protocol/10.1007/978-1-4939-9074-0_6#Sec16)
<img width="1032" alt="Снимок экрана 2025-02-10 в 10 21 00" src="https://github.com/user-attachments/assets/8a0a7f28-2923-45e1-946f-f471f2ca96b8" />

- **Comparison of Repeat Detection Methods:**
  - Use the REPET program, which is recommended for analyzing repeats in non-model invertebrates, and compare its results with those obtained using RepeatModeler/RepeatMasker. [Article](https://link.springer.com/protocol/10.1007/978-1-0716-2883-6_1?fromPaywallRec=false).


## **Conclusion**

The analysis of repeats in the genomes of microsporidia *Dictocoela muelleri* and *Nosema granulosis*, in comparison with their host *Gammarus roeselli*, did not support the hypothesis of recent horizontal transfer of repeats. The data indicate that most of the detected elements are ancient, and the activity of mobile elements in recent evolutionary times is extremely limited. The results obtained, along with the questions raised, will serve as a basis for further studies aimed at refining the characterization of repeats and elucidating the evolutionary mechanisms underlying genome formation in microsporidia.
