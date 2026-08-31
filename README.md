# Predictive Modeling and Multivariate Analysis of Soybean Root-Associated Bacterial Communities

**Project status:** 🟡 In progress  
**Current stage:** SILVA 138 / QIIME 2 VSEARCH taxonomic classification

This repository documents the computational analysis of publicly available soybean root-associated bacterial 16S rRNA sequencing data from **NCBI BioProject PRJNA970087**.

## Research aim

To quantify the relative and interactive effects of soybean genotype, developmental stage, and root-associated spatial compartment on bacterial community composition using multivariate ecological statistics and predictive machine-learning approaches.

## Research questions

1. How does soybean genotype influence root-associated bacterial community composition?
2. How do bacterial communities change across developmental stages?
3. How do bacterial communities differ among spatial compartments?
4. Which ecological factor explains the greatest proportion of community variation?
5. Can microbial community profiles predict soybean genotype, developmental stage, or spatial compartment?
6. Which bacterial taxa contribute most strongly to predictive classification?

## Current workflow

```text
PRJNA970087
    ↓
SRA data retrieval
    ↓
FASTQ conversion
    ↓
FastQC
    ↓
MultiQC
    ↓
V3–V4 primer removal with Cutadapt
    ↓
Post-trimming QC
    ↓
QIIME 2 import
    ↓
DADA2 denoising
    ↓
ASV table + representative sequences
    ↓
SILVA 138
    ↓
VSEARCH taxonomic classification
    ↓
CURRENT STAGE
    ↓
Taxonomy review
    ↓
Metadata/ASV integration
    ↓
Diversity analysis
    ↓
PERMANOVA / variance partitioning
    ↓
Predictive modelling
```

## Progress

### Completed

- [x] Research proposal and research questions
- [x] PRJNA970087 dataset identified
- [x] 12-run working dataset retrieved
- [x] One run (`SRR24519474`) used as the pilot/test sample
- [x] Pilot FastQC/MultiQC assessment
- [x] Cutadapt 5.2 installed
- [x] V3–V4 primer removal
- [x] Post-trimming QC
- [x] QIIME 2 installed/configured under WSL2
- [x] Trimmed reads imported into QIIME 2
- [x] DADA2 denoising completed for the main 11-sample dataset
- [x] 6,312 ASVs generated from 647,119 reads across 11 samples
- [x] SILVA 138 reference database prepared
- [x] VSEARCH taxonomic classification started

### Important sample accounting

The 12-run working dataset includes one **pilot/test sample**, `SRR24519474`.

That pilot was used to establish and validate the primer-removal/trimming workflow before applying the workflow to the remaining samples. Therefore, the documented DADA2 result of **11 samples** refers to the main analytical set and should **not** be interpreted as an accidentally missing sample.

The pilot should be retained and documented separately from the main 11-sample DADA2 analysis unless it is deliberately incorporated into a later analysis.

### In progress

- [ ] Complete VSEARCH taxonomic classification
- [ ] Review taxonomy assignments
- [ ] Confirm final sample/metadata structure for downstream analysis

### Planned

- [ ] Integrate ASV, taxonomy, and metadata
- [ ] Alpha diversity
- [ ] Beta diversity
- [ ] PERMANOVA
- [ ] Variance partitioning
- [ ] Assess Random Forest feasibility and validation strategy
- [ ] Feature importance
- [ ] Identify important bacterial taxa
- [ ] Final figures, tables, and biological interpretation

## Current 12-run working set

| SRA accession | Role |
|---|---|
| SRR24519456 | Main dataset |
| SRR24519462 | Main dataset |
| SRR24519469 | Main dataset |
| SRR24519474 | **Pilot/test sample** |
| SRR24519497 | Main dataset |
| SRR24519502 | Main dataset |
| SRR24519531 | Main dataset |
| SRR24519534 | Main dataset |
| SRR24519541 | Main dataset |
| SRR24519548 | Main dataset |
| SRR24519551 | Main dataset |
| SRR24519615 | Main dataset |

## DADA2 result

The documented main DADA2 run produced:

- **6,312 unique ASVs**
- **647,119 reads**
- **11 main analytical samples**

The pilot sample, `SRR24519474`, was used separately to test/validate the preprocessing workflow.

## Current taxonomic-classification stage

Taxonomic classification is being performed using **SILVA 138** with QIIME 2 `classify-consensus-vsearch`.

The classification command and parameters are documented in `docs/06_taxonomic_classification.md`.

## Data-management principle

Raw FASTQ files are retained unchanged. Large sequencing files and QIIME 2 artifacts should not be committed directly to GitHub. The `.gitignore` file is configured to help prevent accidental uploads.

## Repository structure

```text
soybean-microbiome-project/
├── README.md
├── .gitignore
├── docs/
│   ├── 01_research_design.md
│   ├── 02_data_and_sample_design.md
│   ├── 03_quality_control.md
│   ├── 04_primer_removal.md
│   ├── 05_qiime2_dada2.md
│   ├── 06_taxonomic_classification.md
│   └── 07_next_steps.md
├── scripts/
├── data_metadata/
└── results/
```
