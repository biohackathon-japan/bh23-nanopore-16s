---
title: 'Standardization of Nanopore-based 16S rRNA amplicon sequencing analysis'
title_short: 'Nanopore sequencing for 16S rRNA amplicon'
tags:
  - Nanopore
  - 16S rRNA amplicon sequencing
  - Microbiome
authors:
  - name: Ryo NIWA
    orcid: 0000-0002-5959-7804
    affiliation: 1
  - name: Hiroshi Mori
    orcid: 0000-0003-0806-7704
    affiliation: 2
affiliations:
  - name: Graduate School of Medicine, Kyoto University, Kyoto, Japan
    index: 1
  - name: National Institute of Genetics, Mishima, Japan
    index: 2
date: 30 June 2023
cito-bibliography: paper.bib
event: BH23JP
biohackathon_name: "BioHackathon Japan 2023"
biohackathon_url:   "https://2023.biohackathon.org/"
biohackathon_location: "Kagawa, Japan, 2023"
group: R2
# URL to project git repo --- should contain the actual paper.md:
git_url: https://github.com/geedrn/nanopore_microbiome/tree/main
# This is the short authors description that is used at the
# bottom of the generated paper (typically the first two authors):
authors_short: Ryo NIWA \emph{et al.}
---

# Background

Nanopore sequencing is a third-generation next-generation sequencing technique that is compatible with long nucleic acid reads (Wang et al., 2021). Conventional next-generation sequencing provides accurate short reads in a manner of massively parallel sequencing (Goodwin et al., 2016), but the nanopore-based sequencing mechanism reads the changes in electric potential as DNA passes through protein pores, so it can sequence DNA reads that exceed 10 kb. However, the quality per base is significantly lower than that of sequencing technology called Sequencing by Synthesis. Since its initial release, sequencing cost has decreased considerably, and libraries and sequences can be prepared in a short time. 

The main applications thus far are to detect structural variations, isoforms, and genome sequencing (Aw et al., 2021; Cretu Stancu et al., 2017); however, in recent years, it has been used for 16S rRNA amplicon sequencing (Johnson et al., 2019). However, there is a technical issue of low quality per base in the reads. In 16S rRNA amplicon sequencing, one read was assumed to be one taxonomic classification, and the microbiome community was determined as a compilation of reads. Using the nanopore sequencer, taxonomic classification can be performed with the almost full length of V1-V9 region in 16S rRNA, instead of using narrowed amplicons like V1-V2 or V3-V4 region. This could potentially lead to analyses with higher classification accuracy. Given that the nanopore sequencer is among the most accessible models of next-generation sequencers available to date, the benchmark of the analysis pipelines is highly demanding.

Several studies have reported microbiome analysis using nanopore sequencer (Kerkhof, 2021). In this study, the pipeline reported in BioHackason 2021 (Naoya Oec and Bono, 2021), was improved to be user-friendly and presumably more accurate. In the future, this pipeline will be used as a control for benchmarking and compared with previous reports to determine the best practices in amplicon sequencing.


# Outcomes

A pivotal enhancement was made by employing the DDBJ 16S rRNA fasta file, commonly known as Ref16S, as the primary database for the SAQE pipeline (Naoya Oec and Bono, 2021). Ref16S is a curated repository of 16S rRNA sequences (available at https://www.ddbj.nig.ac.jp/news/en/2006-12-15-e.html). Based on prior research, utilizing Ref16S has been associated with superior results concerning the proportion of annotated reads, as it is a meticulously curated set of sequences. This use of Ref16S is expected to augment the accuracy and reliability of the taxonomic classifications made by the SAQE pipeline.

Kraken2, as an essential component of the SAQE pipeline, is instrumental in taxonomic classification. To maximize the efficacy of Kraken2, we modified the Python code responsible for generating the database. This modification was aimed at ensuring compatibility with the Ref16S dataset and optimizing the classification performance by fine-tuning various parameters and settings. As a result, Kraken2 is now capable of utilizing the Ref16S dataset to its full potential.

In an effort to further sophisticate the outcomes, Bracken (Bayesian Reestimation of Abundance with KrakEN) was integrated into the SAQE pipeline. Bracken is an advanced computational tool that refines the abundance estimates of the taxonomic classifications. By employing a Bayesian algorithm, Bracken optimizes the distribution of reads among different taxa and corrects possible biases or errors in the initial classification. This integration enhances the granularity and accuracy of the abundance data, facilitating a more nuanced understanding of the microbial communities being analyzed.

# Future work

In BH2023, we have made considerable advancements in updating the SAQE pipeline for metagenome analysis. While the updated SAQE pipeline is an important development, it is vital to acknowledge that several other pipelines such as Emu and NanoRTax have been reported in the past. A comprehensive evaluation and comparison of these pipelines, including the updated SAQE pipeline, is necessary to understand their respective strengths and limitations. This analysis should encompass various factors such as accuracy, efficiency, scalability, and ease of use. Understanding the comparative performance will guide researchers in selecting the most suitable pipeline for their specific objectives and datasets. Nanopore sequencing technology has the potential to revolutionize metagenome analysis due to its ability to produce long reads. However, there is a concern regarding the high error rate associated with nanopore sequencing. It is crucial to investigate whether nanopore sequencers can generate reliable annotations to the genus or species level, despite the high frequency of errors in reads. This involves evaluating the error-correction algorithms and understanding the trade-offs between read length and accuracy. Strategies for optimizing the utility of nanopore sequencing in metagenome analysis need to be developed. In this study, we adopted Ref16S as the core database for the SAQE pipeline based on previous research. However, Ref16S mainly focuses on 16S rRNA sequences. For a more detailed and precise taxonomic classification, it is imperative to have access to a curated database that extends to the species level. Future work should concentrate on the development and maintenance of such a database, which includes a comprehensive collection of genomic sequences and annotations. This would be a significant resource for metagenomics, allowing for high-resolution taxonomic profiling and a deeper understanding of microbial communities. These efforts will facilitate more accurate, detailed, and informative analyses, which are essential for the diverse applications of metagenomics in research and industry.

## Acknowledgements

We would like to thank the fellow participants at BioHackathon 2023 for their collaboration and constructive advice, which greatly influenced our project. We are grateful to the organizers for providing this platform and the developers of open source language models. R.N. thanks Prof. Hiromasa Bono and Naoya Oec for technical support and the Medical Innovation of Program at Kyoto University for their financial suopport for attending BioHackason 2023.

## References

1. Aw, J.G.A., Lim, S.W., Wang, J.X., Lambert, F.R.P., Tan, W.T., Shen, Y., Zhang, Y., Kaewsapsak, P., Li, C., Ng, S.B., Vardy, L.A., Tan, M.H., Nagarajan, N., Wan, Y., 2021. Determination of isoform-specific RNA structure with nanopore long reads. Nat. Biotechnol. 39, 336–346. https://doi.org/10.1038/s41587-020-0712-z
2. Cretu Stancu, M., Van Roosmalen, M.J., Renkens, I., Nieboer, M.M., Middelkamp, S., De Ligt, J., Pregno, G., Giachino, D., Mandrile, G., Espejo Valle-Inclan, J., Korzelius, J., De Bruijn, E., Cuppen, E., Talkowski, M.E., Marschall, T., De Ridder, J., Kloosterman, W.P., 2017. Mapping and phasing of structural variation in patient genomes using nanopore sequencing. Nat. Commun. 8, 1326. https://doi.org/10.1038/s41467-017-01343-4
3. Goodwin, S., McPherson, J.D., McCombie, W.R., 2016. Coming of age: ten years of next-generation sequencing technologies. Nat. Rev. Genet. 17, 333–351. https://doi.org/10.1038/nrg.2016.49
4. Johnson, J.S., Spakowicz, D., Hong, B.-Y., Petersen, L.M., Demkowicz, P., Lei Chen, Chen, L., Leopold, S.R., Hanson, B., Hanson, B.M., Agresta, H.O., Gerstein, M., Sodergren, E., Weinstock, G.M., 2019. Evaluation of 16S rRNA gene sequencing for species and strain-level microbiome analysis. Nat. Commun. 10, 5029–5029. https://doi.org/10.1038/s41467-019-13036-1
5. Kerkhof, L.J., 2021. Is Oxford Nanopore sequencing ready for analyzing complex microbiomes. FEMS Microbiol. Ecol. 97. https://doi.org/10.1093/femsec/fiab001
6. Naoya Oec, Bono, H., 2021. Rapid metagenomic workflow using annotated 16S RNA dataset. https://doi.org/10.37044/osf.io/gbt8p
7. Wang, Yunhao, Zhao, Y., Bollas, A., Wang, Yuru, Au, K.F., 2021. Nanopore sequencing technology, bioinformatics and applications. Nat. Biotechnol. 39, 1348–1365. https://doi.org/10.1038/s41587-021-01108-x

