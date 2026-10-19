# Predictive Modeling and Multivariate Analysis of Soybean Root-Associated Bacterial Communities

**Project type:** Pilot-scale reanalysis of public 16S rRNA amplicon data  
**Data source:** NCBI BioProject [PRJNA970087](https://www.ncbi.nlm.nih.gov/bioproject/PRJNA970087)  
**Current status:** Exploratory bioinformatics, multivariate statistics, and pilot machine-learning analysis completed for an 11-sample subset; larger-scale validation remains future work.

## Project overview

This project reanalyses publicly available soybean root-associated bacterial community data to explore how three biological factors relate to community composition:

1. **Root compartment** — the sampled root-associated habitat.
2. **Soybean genotype** — the host genetic background.
3. **Developmental stage** — the plant's developmental state.

The central question is whether bacterial community structure is more strongly associated with root compartment, soybean genotype, or developmental stage. A secondary question is whether community profiles contain enough information to distinguish these factors in a small exploratory classification exercise.

This is a **pilot-scale analysis**, not a definitive biological conclusion or a validated prediction system. The current downstream analysis uses only 11 samples, so estimates and classification results are uncertain and require confirmation with a larger, appropriately designed dataset.

## Research questions

- Which of the three factors is most strongly associated with bacterial community composition in the analysed subset?
- How much community variation is associated with each factor after accounting for the others?
- Do alpha-diversity patterns differ among compartments, genotypes, or developmental stages?
- Can exploratory Random Forest models distinguish these factors from bacterial community profiles, and how reliable are those predictions at the current sample size?

## Data and scope

The study uses 16S rRNA amplicon data associated with **NCBI BioProject PRJNA970087**. The project handbook records an 11-sample main analysis set. A separate pilot sample, **SRR24519474**, was used to test primer trimming and was excluded from the 11-sample downstream analysis.

The primer sequences documented for this dataset are:

- Forward primer (341F): `CCTACGGGNGGCWGCAG`
- Reverse primer (805R): `GACTACHVGGGTATCTAATCC`

The sample accession list is provided in [`data_metadata/sample_accessions.csv`](data_metadata/sample_accessions.csv). This repository documentation does not redistribute raw sequencing reads. Retrieve data from NCBI and follow the source repository's data-use conditions.

## Workflow

The documented workflow includes:

1. Retrieve SRA sequencing data and convert to FASTQ.
2. Remove primers with Cutadapt.
3. Assess read quality with FastQC and summarize quality reports with MultiQC.
4. Process reads in QIIME 2 using DADA2 for denoising and amplicon sequence variant (ASV) inference.
5. Assign taxonomy against the SILVA 138 reference database.
6. Import and organize feature, taxonomy, and sample metadata tables for downstream analysis.
7. Remove organelle-associated features from the analysis table.
8. Explore taxonomic composition and alpha diversity.
9. Calculate beta-diversity/community-distance patterns and test factor associations with PERMANOVA.
10. Use variance partitioning to explore unique and shared contributions of the factors.
11. Collapse ASV counts to genus level for exploratory Random Forest classification because the ASV feature count greatly exceeded the number of samples.

For the fuller documented workflow and important caveats, see [`docs/methods_and_workflow.md`](docs/methods_and_workflow.md).

## Results at the current pilot scale

The figures below are the values recorded in the project pipeline handbook. They should be interpreted as **exploratory results from only 11 samples**, not as generalizable estimates for soybean microbiomes.

| Analysis | Result recorded in the handbook | Interpretation and limitation |
|---|---|---|
| DADA2 denoising | 647,119 reads; 6,312 ASVs | Initial denoising output before organelle filtering. |
| Taxonomic assignment | 6,280 of 6,312 ASVs matched taxonomically (99.49%) | Taxonomic match rate reported by the workflow; not a guarantee that every assignment is correct at species level. |
| Organelle filtering | 6,265 features and 543,195 reads retained; 47 ASVs and 103,924 reads removed | Organelle filtering removed about 16.06% of reads. |
| Alpha diversity | Root compartment: p = 0.0116; genotype and stage not significant in the reported tests | Exploratory evidence of differences among compartments in this subset. |
| PERMANOVA | Compartment: R² = 0.6447, F = 7.26, p = 0.003; genotype: R² = 0.0495, p = 0.701; stage: R² = 0.1189, p = 0.280 | Compartment had the strongest reported association with community composition. Small sample size and study design limit inference. |
| Variance partitioning | Unique adjusted R² reported: compartment = 0.6095; stage = 0.0869; genotype = 0.006 | The handbook notes collinearity warnings and negative adjusted shared fractions. The genotype contribution was not separately tested in the same way as the reported significant terms. |
| Random Forest | OOB accuracy: compartment = 72.7%; stage = 54.5%; genotype = 18.2% | These are unstable, exploratory estimates from n = 11, not validated predictive performance. Genotype classification was poor. |

A more detailed explanation is in [`docs/results_and_interpretation.md`](docs/results_and_interpretation.md).

## Main interpretation — with appropriate caution

Within this 11-sample subset, root compartment showed the strongest reported association with bacterial community structure. Developmental stage may account for some variation after compartment is considered, while the analysed data did not provide a meaningful genotype-classification signal.

These patterns are **preliminary**. The small sample count, possible imbalance or confounding among factors, and the limitations of estimating model performance with so few observations mean the results should not be generalized to soybean microbiomes overall. PERMANOVA interpretation also depends on study design and the dispersion assumption; those checks should be explicitly documented in a larger, confirmatory analysis.

## Current limitations

- Only 11 samples were included in the current downstream analysis.
- The number of microbial features is large relative to the number of samples.
- Factors may be confounded or collinear in this subset.
- Random Forest out-of-bag estimates are highly uncertain at this sample size; a reliable independent test set or robust cross-validation is not feasible with the current data.
- The results are exploratory and are not presented as a publication-ready or independently validated predictive model.
- A larger, balanced subset of the available BioProject data should be considered before making strong biological claims.

## Next steps

1. Review sample availability and metadata across the broader BioProject.
2. Select a larger subset with a clear, balanced design and sufficient replication across factors.
3. Re-run the workflow with the selection criteria and software/database versions recorded.
4. Check PERMANOVA assumptions, including multivariate dispersion, and evaluate confounding among factors.
5. Reassess variance partitioning with adequate sample size.
6. Evaluate predictive models using a suitable validation strategy only after sample size and class balance support it.
7. Add reproducible scripts, software-version records, and generated figures/tables to this repository as they are finalized.

## Repository contents

- `README.md` — project overview, current status, key exploratory results, and limitations.
- `docs/methods_and_workflow.md` — stepwise workflow and methods notes.
- `docs/results_and_interpretation.md` — detailed results and interpretation cautions.
- `data_metadata/sample_accessions.csv` — accession list for the documented main set and the separate primer-trimming pilot.
- `results/summary_results.csv` — machine-readable summary of the values documented in the pipeline handbook.

This package updates the project's **documentation** to match the work recorded in the pipeline handbook. It does not include raw sequencing data, generated result figures, or a complete executable workflow; those should be added only when the actual files and commands are ready to publish.

## Acknowledgement and citation

Data source: NCBI BioProject **PRJNA970087**. Please cite the original study associated with the BioProject (Kifushi et al., 2024, as identified in the project handbook) and the relevant database record when reusing the data. Confirm the full bibliographic details from the NCBI record or original publication before final submission.

## Contact

Project repository: [Hi-Script/soybean-microbiome-project](https://github.com/Hi-Script/soybean-microbiome-project)  
Website: [HiScript Projects](https://hiscript.com.ng/projects.html)
