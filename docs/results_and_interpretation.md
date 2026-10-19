# Results and interpretation notes

## Scope

The results below reproduce the numerical values recorded in the project pipeline handbook. They come from an 11-sample downstream analysis and should be described as exploratory pilot results.

## Sequencing and feature table

- DADA2 output: 647,119 reads and 6,312 ASVs.
- Taxonomy matched: 6,280 of 6,312 ASVs (99.49%).
- After organelle filtering: 6,265 features and 543,195 reads.
- Filtering removed 47 ASVs and 103,924 reads, about 16.06% of reads.

## Taxonomic observation

The handbook records *Bradyrhizobium* at 88.3% in a nodule sample/group and notes that this is consistent with the expected association of *Bradyrhizobium* with soybean nodules. This is a descriptive observation in the current subset, not proof of a broader pattern across genotypes, stages, or environments.

## Alpha diversity

The handbook reports a significant association for compartment (p = 0.0116), while genotype and developmental stage were not significant in the reported tests. The exact diversity metric and test specification should be confirmed from the analysis output/scripts before publication.

## Community composition: PERMANOVA

| Factor | R² | F | p-value | Summary |
|---|---:|---:|---:|---|
| Root compartment | 0.6447 | 7.26 | 0.003 | Strongest reported association in this subset |
| Soybean genotype | 0.0495 | Not recorded in the summary | 0.701 | No significant association reported |
| Developmental stage | 0.1189 | Not recorded in the summary | 0.280 | No significant association reported in this PERMANOVA result |

The R² values are reported as documented. Because n = 11, the apparent magnitude of the compartment effect should not be generalized without replication in a larger and appropriately balanced sample set. The PERMANOVA model and dispersion diagnostics should be made available for reproducibility.

## Variance partitioning

The handbook reports unique adjusted R² estimates of 0.6095 for compartment, 0.0869 for developmental stage, and 0.006 for genotype. It also records collinearity warnings and negative adjusted shared fractions. These warnings matter: shared/unique fractions can be unstable when predictors are correlated and the number of observations is small. The genotype value should not be treated as proof of no genotype effect.

## Random Forest

The analysis collapsed ASV features to genus level and used 845 genus-level taxa. Reported OOB classification accuracy:

| Target | OOB accuracy | Cautious reading |
|---|---:|---|
| Compartment | 72.7% | Exploratory signal; very small sample |
| Developmental stage | 54.5% | Uncertain and not independently validated |
| Genotype | 18.2% | Poor classification in this pilot |

With only 11 samples, these scores can change substantially with a small change in the sample set. They should not be described as validated model accuracy or as evidence that microbiome profiles can reliably predict the factors. Independent validation or robust cross-validation should be considered only after the dataset is expanded sufficiently.

## Overall interpretation

The current subset suggests that root compartment is the factor most strongly associated with bacterial community structure among those tested. Evidence for independent developmental-stage or genotype effects is weaker in these data. The result is useful for refining the next analysis, but not sufficient to establish general biological conclusions.

## Recommended next analysis

1. Inspect the full BioProject metadata and available sample counts.
2. Design a larger subset with replication across genotype, stage, and compartment.
3. Explicitly assess confounding and group balance.
4. Report PERMANOVA model details and test multivariate dispersion.
5. Recompute variance partitioning with adequate sample size.
6. Use a prespecified validation strategy for any classification model.
7. Add the actual plots and machine-readable model outputs to the repository once checked.
