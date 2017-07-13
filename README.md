## Galaxy docker image

* github repository: [https://github.com/MingChen0919/docker-galaxy-grreport-dibbs](https://github.com/MingChen0919/docker-galaxy-grreport-dibbs)
* Build docker image from the github repository
```
git clone https://github.com/MingChen0919/docker-galaxy-dibbss.git
cd docker-galaxy-grreport-dibbs
docker build -t "docker-galaxy-grreport-dibbs" .
```
* Start a container and launch galaxy

```
docker run -i -t -p 8080:80 -p 8021:21 -p 8022:22 \
  -e "GALAXY_CONFIG_ADMIN_USERS=example@gmail.com" \
  mingchen0919/docker-galaxy-grreport-dibbs \
  /bin/bash
```

```
## Launch galaxy
startup
```

* Go to: [http://127.0.0.1:8080/](http://127.0.0.1:8080/)
* Register an account with the email address: `your_email@gmail.com`, then you will have admin access.





## Galaxy workflows schedule
### RNA
* (P01)Transcriptome assembly. May 1, 2016 
    * Input: raw reads in fastq format
    * Tool: Trimmomatic -> Trinity
    * Output: fasta file 
* (P02)RNASeq alignment to a reference
    * Input: raw reads in fastq format
    * Input: reference genome
    * Input: reference annotation (gff3)
    * Tool: Trimmomatic -> Tophat
    * Output: bam file (either all in 1 file w/ RG or each lib in different file)
* (P03)RNASeq Differential Expression analysis (Control vs Treatment with biological replicates). May 1, 2016
    * Input: bam file (either all in 1 file w/ RG or each lib in different file)
    * Tool: HTSeq -> DESeq2
    * Output: DESeq2 matrix file with p-values
* (P04)RNASeq Variant discovery (against the reference). June 1, 2016
      * Input: bam file (either all in 1 file w/ RG or each lib in different file)
      * Tool: mpileup -> samtools
      * Output: vcf
      * Downstream possible feature: deal with ploidy, SNPEff to determine impact of variation 
* (P05)RNASeq Variant discovery (between samples). June 1, 2016
      * Input: bam file (either all in 1 file w/ RG or each lib in different file)
      * Tool: mpileup -> samtools -> need to investigate last step - can we use vcftools or custom script to filter results
      * Output: filtered vcf
      * Downstream possible feature: deal with ploidy, SNPEff to determine impact of variation 
* (P06)Gene co-expression network construction.	July 1, 2016 (Talk to Miriam about this one)
      * Input: bam file (either all in 1 file w/ RG or each lib in different file)
      * Tool: htseq -> WGCNA
      * Output: network file?
* (P07)MiRNA analysis. August 1, 2016  (Talk to Thomas about this one)
      * Input: raw reads in fastq format
      * Input: MIRBase gff3 for organism (if available)
      * Tool: trimmomatic (stringent length filter and adapter) -> compare to MIRBase ->  determine known/unknown miRNA loci 
      * Output: raw counts of known miRNAs by library
      * Downstream possible feature: map to reference and discover novel elements, normalize counts
      * [MiRDeep2](https://www.mdc-berlin.de/36105849/en/research/research_teams/systems_biology_of_gene_regulatory_elements/projects/miRDeep/documentation#top)
      * Public galaxy server for miRNA analysis: [http://cefap.icb.usp.br/galaxy/](http://cefap.icb.usp.br/galaxy/)
### DNA
* (P08)DNASeq Re-sequencing alignment. September 1, 2016
    * Input: raw reads in fastq format
    * Input: reference genome
    * Tool: Trimmomatic -> Bowtie2
    * Output: bam file (either all in 1 file w/ RG or each lib in different file)
* (P09)DNASeq Variant discovery (against the reference). October 1, 2016
      * Input: bam file (either all in 1 file w/ RG or each lib in different file)
      * Tool: mpileup -> samtools
      * Output: vcf
      * Downstream possible feature: deal with ploidy, SNPEff to determine impact of variation 
* (P10)DNASeq Variant discovery (between samples). October 1, 2016
      * Input: bam file (either all in 1 file w/ RG or each lib in different file)
      * Tool: mpileup -> samtools -> need to investigate last step - can we use vcftools or custom script to filter results
      * Output: filtered vcf
      * Downstream possible feature: deal with ploidy, SNPEff to determine impact of variation 
* (P11)Prediction of functional genetic variants (SNPEff or annovar). November 1, 2016
