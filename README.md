# 2026 GGG201B: Visual exploration of genomic data with the Integrative Genomics Viewer (IGV)

> About me: Daniela Soto, Ph.D. IGG graduate. Former student of Dr. Megan Dennis. Postdoctoral scholar, UCSB. For questions/comments/etc. email me to dcsoto@ucdavis.edu.
    
## 1. Why to use interactive genome browsers

Genomic data visualization and exploration is a key aspect of genomics research.

**Q1:** Why is good to visualize and interactively explore genomes?
* Visualize catch errors that are obvious to us but not to the algorithm
* It's cool :)

**Q2:** What type of genomic data do you use in your research and need to visualize?
* de novo transcriptome assembly with RNA-seq data
* whole-genome sequencing
* metagenomics

## 2. Tools for visual genome exploration

There are several tools for visual genome exploration, but the two most widely used are:

* UCSC Genome Browser: https://genome.ucsc.edu/
 
![](https://i.imgur.com/uzc5DuF.png)

* Integrative Genome Viewer (IGV): https://igv.org/
 
![](https://i.imgur.com/cLJSAqZ.png)

Note: Other genome browsers include Jbrowse and Integrative Genome Browser (IGB).

**Q3:** Have you used other genome visualization tool? Which one have you used in class?
* SNAPGene plasmids
* NCBI genome data viewer

## 3. IGV vs UCSC

My ratings:

|                      | UCSC Genome Browser | IGV     |
| -------------------- | ------------------- | ------- |
| Online availability  | ★★★★★               | ★★☆☆☆   |
| Offline availability | ☆☆☆☆☆               | ★★★★★   |
| Reference genomes    | ★★★★★               | ★★★★☆   |
| Custom genomes       | ★★☆☆☆               | ★★★★★   |
| Public resources     | ★★★★★               | ★★☆☆☆   |

Both options can visualize:
* Genome assemblies (fasta)
* Gene annotations (gff, gtf)
* Reads mappings (bam, cram) 
    * WGS, RNA-seq, etc.
* Genomic variants (vcf)
* Genomic regions (bed)
* Epigenetic datasets
  * Loops, ChIP-seq, ATAC-seq, etc.

Which one to use? Ultimately, it's up to personal preference.

**In this session, we will learn to use IGV.**

## 4. Online versus desktop IGV

Today, we will work interactively with IGV's online version: https://igv.org/app/

(If we have time, I will show you how to use the desktop version, which is truly the best way to use all the capabilities of IGV!)

**Homework**: Download IGV desktop app. Go to: https://software.broadinstitute.org/software/igv/

## 5. Exploring the IGV graphic interface

1. Selecting a genome
    * Load Hg38 genome
2. Browsing by coordinate
    * Go to chr15:32,293,372-33,150,812
    * Expand the height of the RefSeq track to 400
    * Zoom in to _ARHGAP11A_
    * You can go directly to _ARHGAP11A_ locus using the gene name.

> Note that IGV and UCSC use 1-start fully closed coordinate system. This article explains the diffrence between genomic coordinate systems: https://genome-blog.soe.ucsc.edu/blog/2016/12/12/the-ucsc-genome-browser-coordinate-counting-systems/

3. Preloaded tracks
    * Go to Tracks > ENCODE signals > ChIP-seq
    * Search and add the following accession numbers:
        * ENCFF649LLS (H3K27ac) 
        * ENCFF298AQY (H3K4me3)

What are we looking at?
<img src="https://hackmd.io/_uploads/BJrnbBBnp.png" width="400">
_Yashar et al. 2022. Genome Biol._

## 6. Case study 1: Variant calling in _ARHGAP11_ gene family

The Dennis Lab performed targeted PacBio HiFi sequencing of genes _ARHGAP11A_ and _ARHGAP11B_ in a cohort of ~200 individuals to accurately identify genomic variation in these highly identical loci. 

### 6.1 Visualizing long-read alignments and variant files

1. Download PacBio reads mapped to Hg38 from individual HG002:
- bam file: https://bioshare.bioinformatics.ucdavis.edu/bioshare/download/cpqqdfge5lfvovq/dcsoto/GGG201B/ARHGAP11.Hg38.bam
- index: https://bioshare.bioinformatics.ucdavis.edu/bioshare/download/cpqqdfge5lfvovq/dcsoto/GGG201B/ARHGAP11.Hg38.bam.bai

> Important note: For this tutorial, we are loading local files. However, when using the IGV desktop app, files can be loaded from local folders as well as URLs.

2. Upload both the bam file and the index simultaneously using Tracks > Local File.

3. Download the variants in VCF format from here and load them into IGV:
https://bioshare.bioinformatics.ucdavis.edu/bioshare/download/cpqqdfge5lfvovq/dcsoto/GGG201B/ARHGAP11.Hg38.vcf

We should see the reads aligned to the locus as depicted below:
![](https://i.imgur.com/ont6B5q.png)

Default nucleotide colors in IGV:
![Screenshot 2024-02-22 at 2.06.00 PM](https://hackmd.io/_uploads/ry5DBSB2T.png)

### 6.2 Visualizing short-read alignments and variant files

For comparison, we will visualize short-read Illumina reads from the same individual (HG002) mapped to Hg38.

1. Download Illumina reads mapped to Hg38 from individual HG002:
* bam file: https://bioshare.bioinformatics.ucdavis.edu/bioshare/download/cpqqdfge5lfvovq/dcsoto/GGG201B/ARHGAP11.HG002.illumina.sort.bam
* bam index: https://bioshare.bioinformatics.ucdavis.edu/bioshare/download/cpqqdfge5lfvovq/dcsoto/GGG201B/ARHGAP11.HG002.illumina.sort.bam.bai

2. Upload both the bam file and the index simultaneously using Tracks > Local File.

We should now have both, long and short reads, aligned to Hg38:
![](https://i.ibb.co/gFyz2fhg/Screenshot-2026-02-12-at-10-41-33-AM.png)

**Q4**: What are the main differences between long and short read sequencing alignments in this locus?
* Length of the reads
* Illumina reads have the same size, PacBio reads don't
* Low map quality reads are white

## 7. Case study 2: Visualizing your assembly from last Friday

Now we will learn to visualize custom genomes in IGV (this is where IGV shines!).

### 7.1. Adding a custom reference genome

First, let's download the custom genome assembly of E. coli that you assembled last Friday to our local computer.

In case you don't have access to the files, you can download them from the following links:
* Genome: https://bioshare.bioinformatics.ucdavis.edu/bioshare/download/cpqqdfge5lfvovq/dcsoto/GGG201B/SRR2584857-assembly.fa
* Genome index: https://bioshare.bioinformatics.ucdavis.edu/bioshare/download/cpqqdfge5lfvovq/dcsoto/GGG201B/SRR2584857-assembly.fa.fai

> To add a custom genome assembly, go to Genome > Local file, and select _both_ the `.fa` and `.fai` files simultaneously.

### 7.2. Adding the alignments files

Importantly, we need to change the name of the bam files and generate a bam index (IGV only accepts `.bam` and `.bam.bai` as extensions). The final file names should be:
- SRR2584857_reads.x.SRR2584857_assembly.bam.sorted.bam
- SRR2584857_reads.x.SRR2584857_assembly.bam.sorted.bam.bai

In case you don't have access to the files, you can download these files from here:
* BAM files: https://bioshare.bioinformatics.ucdavis.edu/bioshare/download/cpqqdfge5lfvovq/dcsoto/GGG201B/SRR2584857_reads.x.SRR2584857_assembly.bam.sorted.bam
* Index file: https://bioshare.bioinformatics.ucdavis.edu/bioshare/download/cpqqdfge5lfvovq/dcsoto/GGG201B/SRR2584857_reads.x.SRR2584857_assembly.bam.sorted.bam.bai

> To add the alignment files go to Tracks > Local file, and select _both_ the `.bam` and `.bai` files simultaneously.

The assembly and alignment files should look like:
![](https://i.ibb.co/jP6rcKrd/Screenshot-2026-02-12-at-9-43-28-AM.png)

**Q5**: Do the reads always agree with the genome assembly? Identify regions of concordance and discrepancies.
* No, because there are sequencing errors in the reads.

## 8. Additional resources

To learn more visit the IGV web documentation:
https://igvteam.github.io/igv-webapp/

Or the IGV Desktop user guide:
https://software.broadinstitute.org/software/igv/userguide

