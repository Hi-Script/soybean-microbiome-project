# 02 — Data and Sample Design

## Source

**NCBI BioProject:** PRJNA970087

## Working dataset

The project initially assembled 12 SRA runs:

- SRR24519456
- SRR24519462
- SRR24519469
- SRR24519474
- SRR24519497
- SRR24519502
- SRR24519531
- SRR24519534
- SRR24519541
- SRR24519548
- SRR24519551
- SRR24519615

## Pilot/test sample

`SRR24519474` was intentionally used as the **pilot/test sample**.

It was used to establish and validate the preprocessing workflow before applying the same approach to the remaining samples.

Therefore, the DADA2 result of 11 samples represents the **main analytical dataset after the pilot was treated separately**, rather than an unexplained loss of one sample.

## Metadata

The NCBI SRA Run Table is the source for sample metadata. The local copy is maintained as `SraRunTable.csv`.

Metadata fields used for design checking include genotype, developmental stage, spatial compartment, and replicate information.

## Important design consideration

Before final inferential analysis, the metadata and replication structure must be checked against the research questions. Technical paired-end reads are not independent biological replicates.
