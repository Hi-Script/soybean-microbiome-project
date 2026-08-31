# 05 — QIIME 2 and DADA2

## Environment

QIIME 2 was installed and used under WSL2/Ubuntu.

## Import

Primer-trimmed paired-end FASTQ files were imported into QIIME 2.

Read quality was inspected using:

```bash
qiime demux summarize
```

## DADA2

DADA2 was used for quality filtering, truncation, error learning, denoising, paired-end merging, ASV inference, and chimera removal.

Selected truncation settings:

```text
Forward: 240 bp
Reverse: 200 bp
```

The settings were selected from the observed read-quality profiles.

## Main DADA2 result

The completed main DADA2 analysis produced:

- **6,312 unique ASVs**
- **647,119 reads**
- **11 samples**

Expected artifacts:

```text
table.qza
rep-seqs.qza
denoising-stats.qza
```

## Pilot accounting

`SRR24519474` was the pilot/test sample and was used to establish the preprocessing workflow. The documented 11-sample DADA2 result therefore corresponds to the remaining main analytical samples.

This is intentional and should not be described as an unexplained missing sample.
