# Characterization-of-epigenomic-dynamics-of-tomato-
 DNA methylation and RNA sequencing assay for characterisation of (epi)genetic changes on BABA primed tomato plants

**Keywords**

DNA methylation, Whole genome bisulfite sequencing (WGBS), Methylation contexts in plants (CpG, CHG, CHH), Analysis of Differentially methylated region (DMR), Plant priming, Transposable elements

**Objective(s)**

To characterize the epigenomic dynamics of tomato (Solanum lycopersicum) during fruit development and tissue differentiation, I created a comlete, strand-aware spatial methylome profiling pipeline. This workflow integrates differentially methylated regions (DMRs) in both CHH and CHG sequence contexts with transposable element (TE) structural annotations from the REPET database. The complete analysis quantifies family-specific TE targeting, genome-wide enrichment relative to background repeat abundance, and fine-scale spatial distribution relative to 5' transposon boundaries.
The data was taken from the following study [1].

# Experimental setup

Investigation of DNA methylation profile of leaves and fruits of Solanum lycopersicum, from plants exposed to ß-aminobutyric (BABA) at two different developmental stages (2 weeks post germination, 12 weeks pst germination) or treated with water (control).

# Bioinformatics processing Pipeline

The complete bioinformatics processing pipeline is shown on Figure 1. Complete flow was done in several phases, described in subsequent sections.

![Bioinformatics pipeline](/Images/Complete_processing_flow.png)
**Figure 1: Complete processing flow**

# Upstream data processing**

Upstream data processeing was done in usegalaxy platform. Upstream data processing included processing of raw reads obtained from [1] in following steps:
 - Download of reads from NCBI (Fasterq download)
 - Quality control (fastqc, multiqc)
 - Adapter trimming (Cutadapt, Trim Galore)
 - Reorganization of samples (Treated vs. control, 2 wpg vs. 12 wpg) 
 - Bisulfite genome alignment (bismarck, bwameth)
 - Methylation calling and extraction of metrics for CpG, CHG and CHH contexts (Methyldackel)

[MultiQC initial](https://droslj.github.io/Characterization-of-epigenomic-dynamics-of-tomato-/MultiQC_initial.html)

[MultiQC after adapter trimming](https://droslj.github.io/Characterization-of-epigenomic-dynamics-of-tomato-/MultiQC_post_T.html)

# Differential methylation analysis

Calling differentially methylated regions (using metilene tool) identified DMRs for all relevant contexts (CpG, CHG and CHH). Pairwise genomic contrasts were conducted across developmental stages and tissue types (e.g., Fruit vs. Leaves at 2 WPG, Fruits: 2 vs. 12 WPG, Leaves vs. Fruits at 12 WPG, and Leaves: 2 vs. 12 WPG). Final results were filtered for difference in methylation and adjusted p-value (|Δmeth| ≥ 10% (CpG, CHG), 20% (CHH); p adj. < 0.01). DMRs were defined based on significant methylation differences across contiguous cytosines in CHH and CHG contexts. Genomic coordinates (chromosome, start, end, and strand) were recorded for each identified region.<br>

## Chromosomal DMR distribution map

Using results from previous step, Chromosomal DMR distribution map for all three contexts was extracted (Figures 2 - 4).

![Genome wide DMR distribution for CpG context](Images/CpG_DMR_Density_Composite_2x2.png)

<br>

**Figure 2: Genomic distribution map showing identified CpG counts across chromosomes for each developmental contrast**
<br>

![Genome wide DMR distribution for CHG context](Images/CHG_DMR_Density_Composite_2x2.png)

<br>

**Figure 3: Genomic distribution map showing identified CHG DMR counts across chromosomes for each developmental contrast**
<br>

![Genome wide DMR distribution for CHH context](Images/CHH_DMR_Density_Composite_2x2.png)
<br>
**Figure 4: Genomic distribution map showing identified CHH DMR counts across chromosomes for each developmental contrast**
<br>
<br>

# Functional gene annotation
<br>
To determine the potential regulatory impact of epigenomic variations identified across Solanum lycopersicum tissues and developmental stages, differentially methylated regions (DMRs) across CpG, CHG, and CHH contexts were mapped against genomic feature annotations (ITAG4.0 gene models). Additionally, obtained genes were extracted for pathway enrichment (see following section). Only genes that fall within  promoter region (i.e. < 2000 b.p.) were retained.
<br>

## Pathway enrichment
 <br>
Genes obtained in the previous step were extracted and used for pathway enrichment (gProfiler). Results obtained are summarized in the Table 1'
<br>

![Summary of pathway enrichment](Images/Pathway_enrichment.png)

**Table 1: Summary of pathway enrichment** 
<br>
**Observations**
CpG context focuses on Seed/Embryo Maturation. The primary CpG epigenetic shifts during fruit transition (2 to 12 WPG Fruit) specifically target embryo and seed development (GO:0009790, GO:0009793, GO:0048316), matching the internal biological shifts of ripening tomato fruits preparing for seed dormancy.<br>
<br>
CHH context focuses on Membrane & Stress Signaling. CHH changes dynamically target cell surface signaling (plasma membrane and cell periphery) during fruit maturation, as well as broader stress responsiveness (cellular response to stimulus) during early tissue differentiation.<br>
<br>
CHG context didn't provide any significantly enriched pathways.<br>
<br>
# Genomic Feature Annotation and Distribution<br>
<br>
Genomic feature distribution of differentially methylated contexts comparing experimental factors (Factor 1 - Tisue: Leaf vs. Fruit, Factor 2 - time after germination: 2 vs. 12 weeks) for all three contexts were extracted from data by intersecting with gff gene model (ITAg4.0_gene_models.gff). Spatial intersections were computed using bedtools intersect, capturing both direct physical overlaps (Distance = 0 bp) and proximal flanking relationships (up to 2000 bp upstream/downstream) for all three contexts Genomic feature distribution shows percentage of total DMRs falling into each genomic feature category and is shown on Figures 5 - 7.<br>
<br>

![Genomic feature distribution CpG](Images/Genomic_feature_distribution_CpG.png)

**Figure 5: Genomic feature distribution for CpG context**

![Genomic feature distribution CHG](Images/Genomic_feature_distribution_CHG.png)

**Figure 6: Genomic feature distribution for CHG context**

![Genomic feature distribution CHH](Images/Genomic_feature_distribution_CHH.png)

**Figure 7: Genomic feature distribution for CHH context**

<br>

**Observations**<br>

**Overall observation**<br>
The distribution of genomic features shown in the images suggests a strong noncoding/intergenic bias in differentially methylated regions (DMRs), especially for CHG and CHH methylation. That pattern is biologically plausible in tomato because intergenic regions are rich in repetitive DNA and transposable elements, which are major targets of plant DNA-methylation pathways. <br>

**Intergenic enrichment**<br>
Roughly 60–80% of DMRs fall in intergenic sequences. This is consistent with methylation changes occurring in transposon-rich or heterochromatic regions rather than primarily inside protein-coding exons.<br>

**CHG and CHH contexts**<br>
Their low representation in exons and stronger association with intergenic regions fits the expected behavior of non-CG methylation. CHH methylation is commonly associated with RNA-directed DNA methylation (RdDM) and transposon silencing, while CHG methylation is often maintained by CMT3-related pathways.<br>

**CpG context**<br>
The relatively greater representation of CpG DMRs in introns and promoter-proximal regions is also plausible. CpG methylation can occur within gene bodies and regulatory regions, where it may be associated with transcriptional regulation or, in some cases, alternative splicing.<br>

**Low exon overlap**<br>
Fewer than 5% of CHG and CHH DMRs overlapping coding exons suggests that methylation remodeling may avoid directly altering protein-coding regions.<br>
<br>

# Transposable element Feature Annotation and distribution<br>
<br>
Similarly as with the genomic feature distribution, identified DMRs were mapped to genomic repeats by intersecting with REPET annotation (ITAG4.0_REPET_repeats_aggressive.gff). Transposons were classified into structural categories, including Class I LTR (Copia, Gypsy), Class I non-LTR (LINE, SINE), Class II (Helitron), Host Gene Exons/Fragments, and Unclassified / Degraded elements.<br>
<br>

![TE features](Images/Transposable_feature_distribution_CHG.png)

**Figure 8: Transposable feature content for CHG context**

![TE features](Images/Transposable_feature_distribution_CHH.png)

**Figure 9: Transposable feature content for CHH context**
<br>

**Observations**<br>

**CHH DMRs near LTRs and truncated/degraded repeats**<br>
This is consistent with CHH methylation being involved in active or RNA-directed transposon control. CHH methylation is more dynamic than CHG methylation, so it may respond strongly to BABA treatment or developmental changes.<br>

**CHG DMRs distributed across several repeat categories** <br>
The broader CHG distribution including degraded repeats, Helitrons, and host-gene/exonic repeat fragments suggests that CHG changes are not restricted to intact LTR elements. This could reflect maintenance or remodeling of methylation across older, fragmented, and gene-proximal repeats.<br>

**Copia and Gypsy representation** <br>
Finding both LTR superfamilies is reasonable because they are abundant in plant genomes. However, their presence among DMRs does not by itself demonstrate preferential targeting. That conclusion depends on the whole-genome background enrichment analysis.<br>

**Degraded or unclassified repeats**<br>
These categories should not be dismissed as uninformative. They may represent old TE insertions that have accumulated mutations but retain regulatory or chromatin effects. However, they are also more vulnerable to annotation ambiguity and fragmented interval definitions.<br>
<br>

# Integration of Genomic Features and Transposable Elements

Direct intersection between genomic DMR intervals and the ITAG4.0_REPET_repeats_aggressive.gff repeat annotation files provides  DMR overlap across all transposable element superfamilies (Copia, Gypsy, Helitrons, LINEs, etc.) that were identified by the REPET pipeline. 

![DMR distribution across REPET for CHG context](Images/DMR_distribution_across_REPET_CHG.png)

**Figure 10: DMR Distribution Across REPET Categories for CHG context**

![DMR distribution across REPET for CHH context](Images/DMR_distribution_across_REPET_CHH.png)

**Figure 11: DMR Distribution Across REPET Categories for CHH context**

**Observations**

**Non-CG Enrichment at Repeats and Intergenic Regions**
CHG and CHH DMRs heavily skew toward transposable elements and intergenic spaces, reflecting active, localized maintenance of heterochromatic silencing and repeat suppression via the RNA-directed DNA methylation (RdDM) pathway.

**Proximity at Gene-TE Boundaries**
The distance filter (< 2,000 bp upstream and gene bodies) reveals that a targeted subset of non-CG DMRs localizes to repetitive elements situated within proximal promoter regions or long introns.

**Superfamily Target Profiles**
Across the analyzed transposable element intersections, LTR retrotransposons (predominantly Copia and Gypsy superfamilies) capture the majority of non-CG differential methylation events.

# Whole-Genome Background Enrichment Analysis

To determine whether dynamic methylation non-randomly targets specific repeat families, hypergeometric enrichment testing was conducted against the whole-genome REPET background. Observed DMR counts per TE category were compared against total genome-wide REPET feature frequencies. This step established statistically significant enrichment (p < 0.05) for truncated/degraded repeat fragments and specific LTR subfamilies relative to background genomic expectations.

![Whole genome background enrichment - CHG context](Images/BG_enrichment_CHG.png)

**Figure 12: Whole genome background enrichment (CHG context)**

![Whole genome background enrichment - CHH context](Images/BG_enrichment_CHH.png)

**Figure 13: Whole genome background enrichment (CHH context)**

**Observations**<br>

**Copia (Enriched) vs. Gypsy (Depleted) in DMRs**
Even though both are Class I LTR retrotransposons, their differential methylation (DMR) behavior often comes down to evolutionary age, genomic positioning, and saturation:

Gypsy Elements (Static / Saturated): Gypsy elements in plant genomes (like tomato) tend to be massive, ancient, and concentrated into dense pericentromeric blocks. Because they have been locked down for millions of years, they are constitutively and densely hypermethylated across the board. They are so thoroughly silenced that they rarely change their methylation state under normal developmental or environmental shifts. Consequently, they don't show up often in differential methylation analyses because they never switch—they appear "depleted" in DMRs simply because they are permanently static.

Copia Elements (Dynamic / Transitional): Copia families, on average, tend to be younger, more transcriptionally active, or located closer to euchromatic-heterochromatic boundaries. Because they sit in these transitional zones, they are much more susceptible to dynamic gains or losses of methylation in response to stress or development, making them heavily enriched in DMR sets.

**LINEs: Enriched in CHG, Depleted in CHH**
The inverse pattern for LINEs (enriched in CHG maintenance, depleted in asymmetric CHH) points to how non-LTR elements interact with specific plant methylation pathways:

Why CHG Enrichment? CHG methylation in plants is tightly maintained by CMT3 in a self-reinforcing loop with H3K9me2 histone marks. If LINE elements reside in chromatin compartments where this maintenance loop is actively operating, they will stably accumulate and maintain high levels of CHG methylation as part of standard transposon gene-body silencing.

Why CHH Depletion? CHH methylation is predominantly driven by RdDM (RNA-directed DNA methylation), which heavily targets the edges and boundaries of repeats where small RNAs are generated. If the LINE elements in your annotation are positioned away from active boundaries (e.g., deeply embedded or structurally isolated), they bypass the intense small-RNA surveillance that drives sharp CHH enrichment peaks.

**Why SINEs Favor CHH Universally**
Euchromatic Proximity: SINEs (Short Interspersed Nuclear Elements) are short, tRNA-derived elements that typically insert themselves into gene-rich, euchromatic regions rather than deep heterochromatic deserts.

Constant RdDM Surveillance: Because they sit close to genes and active transcription units, they are continuously monitored by the RdDM pathway (RNA-directed DNA methylation), which targets short, accessible repeats and maintains a steady baseline of asymmetric CHH methylation across all developmental states and tissue comparisons.

2. Is the CHG Appearance at 2 WPG Real or an Artifact?
SINEs have a much lower total copy number and genomic footprint in plants compared to massive LTR retrotransposons like Gypsy or Copia. This low abundance makes them uniquely sensitive to both biological and statistical factors:

The Low-Count / Sample Size Effect (Statistical Noise): Because the absolute number of SINE-associated DMRs is small, a minor shift in a handful of elements can artificially push a category past a significance threshold in one specific contrast. When sample sizes are small, sporadic signals are common.

A True Developmental Window (2 WPG Divergence): If it is biological, 2 WPG represents a critical juncture of rapid tissue divergence where vegetative (leaves) and reproductive (fruit) programs are branching sharply. Transient, highly specific shifts in CMT3/CHG maintenance can occur during early developmental transitions when chromatin states are being actively re-patterned.

Given how small the SINE pool usually is, it is very likely a combination of both: the low count makes them prone to fluctuation, but the 2 WPG contrast captures a unique window of maximum tissue-type divergence.

**Why Helitrons Favor CHG Maintenance (Enriched in 2 vs. 12 WPG Timepoints)**
Replication and Intragenic Niche: Helitrons replicate via a rolling-circle mechanism and have a unique habit of capturing gene fragments and nesting inside or very close to gene bodies.

Developmental Repression Over Time: The 2 vs. 12 WPG contrasts capture developmental progression (early juvenile/fruit-set vs. mature sink/source stages). During plant maturation and aging, stable gene-body or proximal repeats often undergo sustained maintenance methylation via the CMT3-H3K9me2 pathway (CHG) to keep them securely locked down as transcriptional profiles stabilize. Because Helitrons are frequently caught in the act of altering gene proximity or capturing sequences, they become hotspots for dynamic CHG modulation specifically when comparing developmental time points.

2. Why They Are Simultaneously Depleted in CHH in Those Same Contrasts
Avoidance of Active RdDM Boundaries: CHH methylation is governed by the RdDM pathway, which targets edge-delimited, small-RNA-producing heterochromatic boundaries.

The "Internal" Nature of Helitron Activity: Helitrons are notorious for inserting themselves inside genes or low-copy regions where heavy small-RNA-generating machinery (RdDM/CHH) is actively suppressed to prevent collateral damage to the host gene. When you look at differential dynamics across time points (2 vs. 12 WPG), the changes happening to Helitrons are predominantly driven by internal maintenance mechanisms (CHG) rather than fresh boundary-invasion events (CHH). Consequently, while CHG shifts highlight their developmental regulation, CHH remains conspicuously absent or depleted because they avoid active RdDM fronts.

This clean separation—CHG capturing the temporal/developmental tightening of these elements, and CHH reflecting a lack of boundary-level small RNA stress—gives you a very cohesive story for your Helitron population!

**HOST/EXON fragments**

1. Why CHG is Present (Bulk Heterochromatin & Maintenance)
The Legacy of Transposon Capture: Host-gene exon fragments found outside of normal gene contexts are frequently the result of past Helitron-mediated exon transduction or ancient, degenerated transposable element insertions.

The CMT3-H3K9me2 Maintenance Loop: Once these fragments are trapped inside or adjacent to repetitive DNA, they are treated by the cell as part of the repeat machinery. They become blanketed by the CHG methylation pathway, which is maintained by CMT3 in a self-reinforcing loop with H3K9me2 histone modifications. This systemic, maintenance-driven CHG methylation covers the entire body of the older repeat or captured fragment, independent of active transcription.

2. Why CHH is Virtually Absent (The "Edge-Only" Rule of RdDM)
Asymmetric CHH Requires Boundaries: CHH methylation in plants is heavily dictated by the RdDM (RNA-directed DNA methylation) pathway. RdDM does not efficiently target the deep interiors of long, established repeats or trapped fragments. Instead, it is an edge-driven phenomenon that focuses heavily on the borders where open euchromatin meets closed heterochromatin.

Lack of Small RNA Signatures: Because host-gene exon fragments embedded within repeats are usually locked down by maintenance machinery rather than undergoing fresh, boundary-driven small-RNA invasion, they completely lack the localized small-RNA flux needed to recruit de novo CHH methyltransferases (like DRM2).

# Spatial Metaplot Analysis Around 5' TE Boundaries

To resolve the precise spatial targeting of methylation relative to transposon architecture, distance vectors were computed from each DMR center to the 5' insertion edge of the nearest TE.
To maintain biological orientation across both forward (+) and reverse (-) strand transposons, a strand-aware coordinate transformation was applied.

![Spatial metaplot analysis - CHG context](Images/Spatial_metaplot_CHG.png)

**Figure 14: Spatial metaplot (CHG context)**

![Spatial metaplot analysis - CHH context](Images/Spatial_metaplot_CHH.png)

**Figure 15: Spatial metaplot (CHH context)**

**Note**
Negative distances (-1000 to -1 bp) represent the 5' euchromatic outer flank (5' promoter-proximal region).
Zero (0 bp) represents the physical insertion boundary
Positive distances (+1 to +2000 bp) represent internal regions within the TE body
Calculated distances were grouped into 100 bp continuous bins spanning -1000 bp to +2000 bp

**References**
[1] Developmentally regulated generation of a systemic signal for long-lasting defence priming in tomato [WGBS], Project PRJNA1144133, NCBI (https://www.ncbi.nlm.nih.gov/bioproject/PRJNA1144133)
