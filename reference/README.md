# Reference Files

This folder is intentionally empty in the repository. Large reference files are not tracked in git.

## Files you need to place here

| File | Source | Size (approx) |
|------|--------|---------------|
| `transcriptoma.fna` | NCBI RefSeq — CDS FASTA for your strain | ~5–15 MB |
| `kraken_db/` | Kraken2 standard 8GB database | ~8 GB |

## How to download

### Transcriptome reference
1. Go to https://www.ncbi.nlm.nih.gov/datasets/genome/
2. Search your organism and strain
3. Download → RefSeq → "CDS from genomic" (.fna format)

### Kraken2 database
```bash
wget https://genome-idx.s3.amazonaws.com/kraken/k2_standard_08gb_20240112.tar.gz
tar -xvf k2_standard_08gb_20240112.tar.gz -C kraken_db/
```

## Why are these not in the repository?

- Raw FASTQ files can be several GB per sample
- Reference databases are hundreds of MB to several GB
- Git and GitHub are not designed for binary files of this size

For large data archiving, consider using **Zenodo** or depositing raw reads in **NCBI SRA**.
