# 04 — Primer Removal with Cutadapt

## Target

The workflow targets the V3–V4 region of the 16S rRNA gene.

Working primers:

### 341F

```text
CCTACGGGNGGCWGCAG
```

### 805R

```text
GACTACHVGGGTATCTAATCC
```

## Software

Cutadapt **5.2** was installed and used for primer removal.

## Pilot validation

The pilot/test sample was:

`SRR24519474`

Documented pilot results:

- 85,023 read pairs processed
- R1 primer detection: 99.6%
- R2 primer detection: 98.5%
- 83,456 read pairs retained
- Approximately 98.2% read-pair retention

The validated trimming strategy was then applied to the remaining samples.

## Main dataset

The remaining 11 samples were processed using the validated primer-removal strategy. Documented retention was approximately 97.6–98.3% across the processed samples.

## Principle

Raw sequencing files were not overwritten or deleted. Trimmed files were kept separately for downstream QIIME 2 processing.
