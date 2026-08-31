# 03 — Quality Control

## FastQC

FastQC was used to assess sequencing-read quality before and after preprocessing.

The QC assessment included:

- Per-base sequence quality
- Per-sequence quality scores
- Per-base sequence content
- GC content
- N content
- Sequence-length distribution
- Duplication levels
- Overrepresented sequences
- Adapter content

## MultiQC

MultiQC 1.35 was used to aggregate the FastQC reports for the working sequencing set.

The QC findings were interpreted in the context of targeted 16S amplicon sequencing. Warnings were not automatically treated as reasons to discard reads.

## Pilot

`SRR24519474` served as the pilot/test sample and was used to validate the preprocessing strategy.

## Data integrity

Raw FASTQ files were retained unchanged. Processed reads were written separately.
