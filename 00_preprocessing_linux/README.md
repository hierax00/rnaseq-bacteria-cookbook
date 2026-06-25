# 00 · Linux Preprocessing

Run these scripts **in order** from your WSL/Linux terminal before opening R.

## Pipeline overview

```
Raw FASTQ (paired-end)
        │
        ▼
  01_quality_control.sh     fastp — filter by quality (Q≥30) and length (≥50bp)
        │
        ▼
  02_taxonomic_check.sh     Kraken2 + Krona — confirm reads are your target organism
        │
        ▼
  03_multiqc_report.sh      MultiQC — aggregate all QC reports in one HTML
        │
        ▼
  04_build_index.sh         Kallisto index — build transcript reference index
        │
        ▼
  05_quantification.sh      Kallisto quant — pseudoalignment and abundance estimation
        │
        ▼
    abundance.tsv files  ← input for R analysis (tximport)
```

## Why Kraken2 before Kallisto?

Kraken2 is a **quality control step**, not a quantification step. It answers:
*"Are my reads actually from the organism I think they are?"*

If your sample is contaminated (host DNA, another bacterium), Kallisto will still
quantify — but you will be quantifying the wrong thing. Always run taxonomic
classification first.

## Input files expected

```
your_working_directory/
├── sample1_R1.fastq     # or .fastq.gz
├── sample1_R2.fastq
├── sample2_R1.fastq
├── sample2_R2.fastq
├── ...
├── kraken_db/           # Kraken2 database (download separately — see below)
└── transcriptoma.fna    # CDS reference from NCBI RefSeq (see below)
```

## Reference files

### Kraken2 database
Download the standard 8GB database:
```bash
# Option A: prebuilt (recommended)
wget https://genome-idx.s3.amazonaws.com/kraken/k2_standard_08gb_20240112.tar.gz
tar -xvf k2_standard_08gb_20240112.tar.gz -C kraken_db/
```

### Transcriptome reference (bacteria)
Download CDS from NCBI RefSeq for your strain:
1. Go to https://www.ncbi.nlm.nih.gov/datasets/
2. Search your organism (e.g., *Pectobacterium versatile*)
3. Download → RefSeq → CDS from genomic FASTA (.fna)

## Software installation (conda/mamba recommended)

```bash
mamba create -n rnaseq fastp kraken2 multiqc kallisto -y
conda activate rnaseq

# KronaTools (requires post-install step)
mamba install -c bioconda krona -y
ktUpdateTaxonomy.sh
```
