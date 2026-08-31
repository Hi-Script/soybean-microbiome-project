# 06 — Taxonomic Classification

## Status

🟡 **In progress**

## Reference

**SILVA 138**

## Method

Taxonomic classification is being performed with QIIME 2:

```text
classify-consensus-vsearch
```

The current classification uses the DADA2 representative sequences and SILVA 138 reference reads/taxonomy.

## Command

```bash
qiime feature-classifier classify-consensus-vsearch --i-query 03_qiime2/rep-seqs.qza --i-reference-reads 05_taxonomy/silva-138-99-seqs.qza --i-reference-taxonomy 05_taxonomy/silva-138-99-tax.qza --p-threads 1 --o-classification 05_taxonomy/taxonomy.qza --o-search-results 05_taxonomy/vsearch-results.qza --verbose
```

## Current state

VSEARCH taxonomic classification has been launched and is the current project stage.

Taxonomy will be marked complete only after the process finishes successfully and the resulting assignments are reviewed.

## Expected output

```text
taxonomy.qza
vsearch-results.qza
```
