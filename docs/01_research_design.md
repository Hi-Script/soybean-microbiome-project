# 01 — Research Design

## Title

**Predictive Modeling and Multivariate Analysis of Soybean Root-Associated Bacterial Communities Across Genotypes, Developmental Stages, and Spatial Compartments**

## Aim

To quantify the relative and interactive effects of soybean genotype, developmental stage, and root-associated spatial compartment on bacterial community composition using multivariate ecological statistics and predictive machine-learning approaches.

## Objectives

1. Retrieve and preprocess publicly available 16S rRNA sequencing data from PRJNA970087.
2. Generate high-quality ASVs using DADA2.
3. Characterize alpha and beta diversity.
4. Quantify independent and shared effects of genotype, developmental stage, and spatial compartment using PERMANOVA and variance partitioning.
5. Develop and evaluate Random Forest models for predicting genotype, developmental stage, and spatial compartment, subject to assessment of the final sample design.
6. Identify bacterial taxa contributing to predictive performance.

## Research questions

1. How does soybean genotype influence bacterial community composition?
2. How do communities change across developmental stages?
3. How do communities differ among spatial compartments?
4. Which ecological factor explains the greatest proportion of community variation?
5. Can microbial community profiles predict genotype, developmental stage, or spatial compartment?
6. Which taxa contribute most strongly to prediction?

## Scope

The current working dataset contains 12 runs, of which `SRR24519474` was used as a pilot/test sample and the remaining 11 form the main DADA2 analytical set.

The broader research proposal contains additional biological levels. The final downstream statistical scope will be determined from the verified metadata and final analytical sample set.
