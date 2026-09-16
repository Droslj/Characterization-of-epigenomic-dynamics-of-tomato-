# Characterization-of-epigenomic-dynamics-of-tomato-
 DNA methylation and RNA sequencing assay for characterisation of (epi)genetic changes on BABA primed tomato plants

**Keywords**

DNA methylation, Whole genome bisulfite sequencing (WGBS), Methylation contexts in plants (CpG, CHG, CHH), Analysis of Differentially methylated region (DMR), Plant priming

**Objective(s)**

To characterize the epigenomic dynamics of tomato (Solanum lycopersicum) during fruit development and tissue differentiation, I created a comlete, strand-aware spatial methylome profiling pipeline. This workflow integrates differentially methylated regions (DMRs) in both CHH and CHG sequence contexts with transposable element (TE) structural annotations from the REPET database. The complete analysis quantifies family-specific TE targeting, genome-wide enrichment relative to background repeat abundance, and fine-scale spatial distribution relative to 5' transposon boundaries.
THe data was taken from the following study [1].

# Experimental setup

Investigation of DNA methylation profile of leaves and fruits of Solanum lycopersicum, from plants exposed to ß-aminobutyric (BABA) at two different developmental stages (2 weeks post germination, 12 weeks pst germination) or treated with water (control).

# Bioinformatics processing Pipeline**

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
Identification of DMR Genomic Regions (using metilene tool) identified differentially methylation regions for all relevant contexts (CpG, CHG and CHH). Final results were filtered for difference in methylation and adjusted p-value (|Δmeth| ≥ 10% (CpG, CHG), 20% (CHH); p adj. < 0.01)Pairwise genomic contrasts were conducted across developmental stages and tissue types (e.g., Fruit vs. Leaves at 2 WPG, Fruits: 2 vs. 12 WPG, Leaves vs. Fruits at 12 WPG, and Leaves: 2 vs. 12 WPG). DMRs were defined based on significant methylation differences across contiguous cytosines in CHH and CHG contexts. Genomic coordinates (chromosome, start, end, and strand) were recorded for each identified region.

![Genome wide DMR distribution for CpG context](Images/CpG_DMR_Density_Composite_2x2.png)

**Figure 2: Genomic distribution map showing identified CpG counts across chromosomes for each developmental contrast**

![Genome wide DMR distribution for CHG context](Images/CHG_DMR_Density_Composite_2x2.png)

**Figure 3: Genomic distribution map showing identified CHG DMR counts across chromosomes for each developmental contrast**

![Genome wide DMR distribution for CHH context](Images/CHH_DMR_Density_Composite_2x2.png)

**Figure 4: Genomic distribution map showing identified CHH DMR counts across chromosomes for each developmental contrast**

# Functional gene annotation

To determine the potential regulatory impact of epigenomic variations identified across Solanum lycopersicum tissues and developmental stages, differentially methylated regions (DMRs) across CpG, CHG, and CHH contexts were mapped against genomic feature annotations (ITAG4.0 gene models). Additionally, obtained genes were extracted for pathway enrichment (see following section). Only genes that fall within  promoter region (i.e. < 2000 b.p.) were retained.

## Pathway enrichment

Genes obtained in the previous step were extracted and used for pathway enrichment (gProfiler). Results obtained are summarized in the Table 1'

![Summary of pathway enrichment](Images/Pathway_enrichment.png)

**Table 1: Summary of pathway enrichment** 

**Comment on pathway enrichment**

1) CpG context
CpG Focuses on Seed/Embryo Maturation: The primary CpG epigenetic shifts during fruit transition (2 to 12 WPG Fruit) specifically target embryo and seed development (GO:0009790, GO:0009793, GO:0048316), matching the internal biological shifts of ripening tomato fruits preparing for seed dormancy.

2) CHH context
CHH Focuses on Membrane & Stress Signaling: CHH changes dynamically target cell surface signaling (plasma membrane and cell periphery) during fruit maturation, as well as broader stress responsiveness (cellular response to stimulus) during early tissue differentiation.

# Genomic Feature Distribution

Genomic feature distribution of differentially methylated contexts comparing experimental factors (Factor 1 - Tisue: Leaf vs. Fruit, Factor 2 - time after germination: 2 vs. 12 weeks) for all three contexts were extracted from data by intersecting with gff gene model (ITAg4.0_gene_models.gff). Genomic feature distribution shows percentage of total DMRs falling into each genomic feature category and is shown on Figures 5 - 7.

![Genomic feature distribution CpG](Images/Genomic_feature_distribution_CpG.png)

**Figure 5: Genomic feature distribution for CpG context**

![Genomic feature distribution CHG](Images/Genomic_feature_distribution_CHG.png)

**Figure 6: Genomic feature distribution for CHG context**

![Genomic feature distribution CHH](Images/Genomic_feature_distribution_CHH.png)

**Figure 7: Genomic feature distribution for CHH context**

**Observation on genomic feature distribution**<br>
<br>
Ad 1) Intergenic Dominance Across All Contexts<br>
Across CpG, CHG, and CHH DMR sets, intergenic sequences represent the largest single category, consistently capturing between 60 and 80% of all differentially methylated regions. This robust intergenic skew reflects large-scale developmental remodeling within transposon-rich and non-coding heterochromatic domains of the tomato genome.<br>
<br>
Ad 2) Non-CG (CHH and CHG) Enrichment in Repetitive Spaces <br>
The CHH and CHG contexts exhibit a heavy restriction to intergenic spaces with minimal representation in coding exons (< 5%). This strongly conforms to canonical RNA-directed DNA methylation (RdDM) and CMT-mediated maintenance pathways, which target transposable elements and repetitive intergenic regions to maintain genome stability without disrupting protein-coding transcription.<br>
<br>
Ad 3) Gene-Body and Intronic Integration in CpG Methylation <br>
In contrast to non-CG contexts, the CpG DMR distributions display a much higher relative abundance within intronic regions (~15-30%) and promoter zones (< 2kb). This structural partitioning matches the expected functional role of symmetrical CG methylation, which frequently populates gene bodies and regulatory interfaces to modulate transcriptional activity and alternative splicing during plant development.<br>
<br>
Ad 4) Developmental and Tissue-Specific Plasticity<br>
The consistent proportional stability across leaf and fruit comparisons (both 2 vs. 12 WPG) demonstrates that while specific loci undergo targeted methylation changes during tissue maturation and organogenesis, the global genomic compartments targeted by epigenetic modifiers remain tightly conserved.<br>
<br>
# Transposable element Feature distribution<br>
<br>
Similarly as with the genomic feature distribution, identified DMRs were mapped to genomic repeats by intersecting with REPET annotation (ITAG4.0_REPET_repeats_aggressive.gff). Spatial intersections were computed using bedtools intersect, capturing both direct physical overlaps (Distance = 0 bp) and proximal flanking relationships (up to 2000 bp upstream/downstream) for all three contexts. Transposons were classified into structural categories, including Class I LTR (Copia, Gypsy), Class I non-LTR (LINE, SINE), Class II (Helitron), Host Gene Exons/Fragments, and Unclassified / Degraded elements.<br>
<br>

![TE features](Images/Transposable_feature_distribution_CHG.png)

**Figure 8: Transposable feature content for CHG context**


![TE features](Images/Transposable_feature_distribution_CHH.png)

**Figure 9: Transposable feature content for CHH context**
<br>

**Observations**

Both non-CG contexts (CHG and CHH) exhibit a heavy positional skew toward intergenic regions and promoter-proximal spaces, reflecting characteristic epigenetic targeting of non-coding and heterochromatic compartments.
LTR Retrotransposon Enrichment
DMRs in both CHG and CHH contexts are predominantly driven by Class I LTR retrotransposons, specifically balancing across Gypsy and Copia superfamilies. This aligns with canonical plant heterochromatin silencing models via CMT and RdDM pathways.
Host Gene and Degraded Fraction Involvement 
Substantial intersections with Host Gene / Exonic Fragments and Unclassified / Degraded repeat fractions highlight a complex overlap between transposable element insertions and gene-proximal regulatory regions.


Quantification of DMR occurrences across REPET feature categories revealed distinct targeting preferences between cytosine contexts. While CHH DMRs preferentially localized near truncated remnants and LTR elements, CHG DMRs showed broader distribution across degraded repeat fragments, host gene exons, and Helitrons.

# Integration of Genomic Features and Transposable Elements

Direct intersection between genomic DMR intervals and the ITAG4.0_REPET_repeats_aggressive.gff repeat annotation files provides  DMR overlap across all transposable element superfamilies (Copia, Gypsy, Helitrons, LINEs, etc.) that were identified by the REPET pipeline. 

![DMR distribution across REPET for CHG context](Images/DMR_distribution_across_REPET_CHG.png)

**Figure 10: DMR Distribution Across REPET Categories for CHG context**

![DMR distribution across REPET for CHH context](Images/DMR_distribution_across_REPET_CHH.png)

**Figure 11: DMR Distribution Across REPET Categories for CHH context**


# Whole-Genome Background Enrichment Analysis

To determine whether dynamic methylation non-randomly targets specific repeat families, hypergeometric enrichment testing was conducted against the whole-genome REPET background. Observed DMR counts per TE category were compared against total genome-wide REPET feature frequencies. This step established statistically significant enrichment (p < 0.05) for truncated/degraded repeat fragments and specific LTR subfamilies relative to background genomic expectations.

![Whole genome background enrichment - CHG context](Images/BG_enrichment_CHG.png)

**Figure 12: Whole genome background enrichment (CHG context)**

![Whole genome background enrichment - CHH context](Images/BG_enrichment_CHH.png)

**Figure 13: Whole genome background enrichment (CHH context)**


# Spatial Metaplot Analysis Around 5' TE Boundaries

To resolve the precise spatial targeting of methylation relative to transposon architecture, distance vectors were computed from each DMR center to the 5' insertion edge of the nearest TE.
To maintain biological orientation across both forward (+) and reverse (-) strand transposons, a strand-aware coordinate transformation was applied.

![Spatial metaplot analysis - CHG context](Images/Spatial_metaplot_CHG.png)

**Figure 14: Spatial metaplot (CHG context)**

![Spatial metaplot analysis - CHH context](Images/Spatial_metaplot_CHH.png)

**Figure 15: Spatial metaplot (CHH context)**


Under this framework:
Negative distances (-1000 to -1 bp): Represent the 5' euchromatic outer flank (5' promoter-proximal region).
Zero (0 bp): Represents the physical insertion boundary
Positive distances (+1 to +2000 bp): Represent internal regions within the TE body
Calculated distances were grouped into 100 bp continuous bins spanning -1000 bp to +2000 bp u)

**References**
[1] Developmentally regulated generation of a systemic signal for long-lasting defence priming in tomato [WGBS], Project PRJNA1144133, NCBI (https://www.ncbi.nlm.nih.gov/bioproject/PRJNA1144133)
