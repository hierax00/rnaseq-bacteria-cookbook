# Example Data for Steps 02–06

This folder contains **fully fictional** example data to make the cookbook
reproducible without requiring real experimental data.

## Files

| File | Used by | Description |
|------|---------|-------------|
| `metadata_all.csv` | Steps 02, 03, 05, 06 | 4 samples: 2 Control + 2 Treatment, 2 batches |
| `annotation.tsv` | Steps 05, 06 | 50 genes with eggNOG-mapper columns (COG, GO, KEGG) |
| `counts/C1.tsv` … `T2.tsv` | Step 02 | Kallisto-format pseudo-count tables |

## How to use

In each Rmd script, the paths assume you run from the `scripts/` working
directory:

```r
metadatos   <- read.csv("../data/metadata_all.csv", row.names = 1)
eggnog_data <- read.delim("../data/annotation.tsv")
```

Replace these with your own files when adapting the cookbook to your organism.
