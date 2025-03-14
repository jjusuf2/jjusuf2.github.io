---
layout: post
title: Downloading raw sequencing data from NCBI Sequence Read Archive (SRA)
---

The SRA contains the raw reads (e.g., FASTQ files) from publications. It is particularly useful if one needs to realign existing data, say to a newer reference genome.

```%%bash
export PATH=$PATH:$PWD/sratoolkit.3.0.10-ubuntu64/bin
prefetch -v --max-size u <SRA_accession_number>
fastq-dump --outdir <output_directory> --dumpbase --skip-technical --clip --read-filter pass --gzip --split-files <SRA_accession_number>
```

Generally, always keep the following flags:
* `--dumpbase`: formats sequence using base space
* `--skip-technical`: dump only biological reads, skip the technical reads
* `--clip`: some sequences contain tags that need to be removed; this removes them
* `--read-filter pass`: only returns reads that pass filtering (without `N`s).
* `--gzip`: compress the output

For paired-end reads only:
* `--split-files`: put the mates in two separate files

**Tip:** If the command `fastq-dump` is not found, try running `export PATH=$PATH:$PWD/sratoolkit.3.0.10-ubuntu64/bin` from the home directory first.

**Tip:** It is recommended to run this command from a directory on a disk that has a lot of space (such as `/mnt/coldstorage`). One can navigate to the desired directory after running the `export` command.