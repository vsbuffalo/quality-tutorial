# Sequencing Quality Pipeline

This tutorial will describe how to use do quality control for Illumina
data. First off, this assumes your data will be of:

 - FASTQ format (gzipped is preferable, no reason to uncompress)
 - Sanger quality encoded. Illumina data run through the CASAVA
   Pipeline with a version >= 1.8 uses Sanger quality. Illumina's
   quality encoding scheme (offset of 64) was used for pipeline
   versions between 1.3 and 1.7. Solexa quality encoding was used for
   pre 1.3 pipelines. Most new data we encounter is Sanger
   encoded. Data downloaded from the SRA will also be Sanger encoded.

## Background Information on FASTQ Quality

 - [Illumina's introduction to sequencing quality][1]. This introduces
   quality encoding and what it means in terms of incorrect bases.
 - 
 
[1]: http://res.illumina.com/documents/products/technotes/technote_q-scores.pdf
 
## Guidelines for Quality Pipelines and Monitoring

1. Quality pipelines should be taken in the context of a
   project. Assembly may require more aggressive adapter removal (so
   even 4-mers that match an adapter sequence are removed) because
   this can confound k-mer based de Bruijn graph assemblers. However,
   in the context of RNA-seq or variant calling, minor adapter
   contamination will just lead to fewer reads mapping. Adjust your
   quality pipeline's aggressiveness in removing possible contaminants
   or low-quality bases based on your project.
   
2. Assess quality at every step. This is the point of
   [seqqs](https://github.com/vsbuffalo/seqqs). An example of why this
   is important, suppose in an RNA-seq a lane has significantly lower
   quality in the final ten bases compared to other lanes. These will
   be trimmed off during read quality trimming, but this may lead to
   [batch effects][2], which can seriously confound RNA-seq and
   genotyping assays.
   
   [2]: http://www.nature.com/nrg/journal/v11/n10/abs/nrg2825.html

## 
