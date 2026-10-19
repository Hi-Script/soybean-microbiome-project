# Methods and workflow notes

This document summarizes the workflow recorded in the project's pipeline handbook. It is a documentation of the work reported so far, not a substitute for versioned executable scripts or a full computational environment specification.

## 1. Data retrieval and sample scope

The source dataset is associated with NCBI BioProject PRJNA970087. The current main downstream analysis set contains 11 accessions. SRR24519474 was used separately as a pilot for testing primer removal and was not included in the 11-sample downstream analysis. The sample list is in `../data_metadata/sample_accessions.csv`.

## 2. Primer removal and read quality control

The documented primers are 341F (`CCTACGGGNGGCWGCAG`) and 805R (`GACTACHVGGGTATCTAATCC`). Cutadapt is used to remove primers before downstream denoising. FastQC is used to inspect raw/processed read quality and MultiQC to aggregate quality-control reports.

The repository should eventually record the exact commands, versions, input/output filenames, and any sample-specific trimming failures. This package does not invent command lines or software versions that were not supplied in the handbook.

## 3. Denoising and feature inference

Reads are processed in QIIME 2 with DADA2 to infer amplicon sequence variants (ASVs), remove likely sequencing errors, and generate feature tables and representative sequences. The handbook reports 647,119 reads and 6,312 ASVs after DADA2 for the main analysis set.

## 4. Taxonomy assignment and filtering

Taxonomic classification is performed using SILVA 138. The handbook reports taxonomy matches for 6,280 of 6,312 ASVs (99.49%). Organelle-associated features are then removed. After filtering, 6,265 features and 543,195 reads remained; 47 ASVs and 103,924 reads were removed (about 16.06% of reads).

## 5. Community summaries and diversity

Taxonomic composition is summarized at appropriate taxonomic levels. Alpha diversity is used to compare within-sample diversity, and beta-diversity/community-distance analysis is used to examine differences in community composition across the recorded factors.

The handbook reports an alpha-diversity association with compartment (p = 0.0116), while genotype and developmental stage were not significant in the reported tests. Exact indices, transformations, distance metrics, and test details should be linked to the actual analysis scripts/results before treating this documentation as a fully reproducible methods record.

## 6. PERMANOVA

PERMANOVA is used to evaluate the association between community composition and compartment, genotype, and developmental stage. Reported results:

- Compartment: R² = 0.6447, F = 7.26, p = 0.003.
- Genotype: R² = 0.0495, p = 0.701.
- Developmental stage: R² = 0.1189, p = 0.280.

Because the analysis includes only 11 samples, these results are exploratory. A larger confirmatory analysis should document the model formula, permutation scheme, sample independence, factor balance, and a test of multivariate dispersion. PERMANOVA can be affected by differences in within-group dispersion as well as differences in group centroids.

## 7. Variance partitioning

Variance partitioning was used to explore unique and shared contributions of the explanatory factors. The handbook reports unique adjusted R² values of 0.6095 for compartment, 0.0869 for developmental stage, and 0.006 for genotype. It also records collinearity warnings and negative adjusted shared fractions.

These results need cautious interpretation. With a small sample size and potentially correlated predictors, partitioned fractions can be unstable. The exact model specification and inferential testing should be reported from the actual scripts before these values are used in a formal manuscript.

## 8. Exploratory Random Forest

ASV-level features were collapsed to genus level because the ASV feature count (6,265 after filtering) greatly exceeded the number of samples. The handbook records 845 genus-level taxa and out-of-bag (OOB) classification accuracies of 72.7% for compartment, 54.5% for developmental stage, and 18.2% for genotype.

These estimates are not evidence of a validated prediction system. With n = 11, model estimates are highly unstable, and an independent test set or robust cross-validation is not feasible. Treat this as a pilot demonstration of an analysis approach only. Any larger follow-up should plan sample size, class balance, and validation before modelling.

## 9. Reproducibility information still to add

As the repository is updated, add the actual scripts and record:

- QIIME 2 release and plugin versions.
- DADA2, Cutadapt, FastQC, MultiQC, and R/package versions.
- SILVA database release and classifier details.
- Exact sample metadata and filtering criteria.
- Commands or workflow configuration for each step.
- Random seeds and model settings where applicable.
- The precise statistical formulas, distance metric, permutations, and dispersion diagnostics.
- Tables/figures generated by the scripts and a description of how to regenerate them.

Do not add placeholder commands as if they were the commands actually run.
