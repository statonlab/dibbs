## README

Two workflows are included in this pipeline. The `Galaxy-Workflow-RNASeq_differential_expression_analysis_2.1.ga` generates htseq counts files for each sample. The `Galaxy-Workflow-RNASeq_differential_expression_analysis_2.2.ga` does differential expression analysis.

At this point, these two workflows can not be integrated into one. Also, once the DESeq2 workflow is built, it can not add more factors and factor levels. The current workflow is designed for one primary factor with two levels.

The ID attribute entered in the htseq-count tool should be the same as the ID in your .gff file

![ID_Attribute_dff](https://github.com/statonlab/dibbs/blob/master/p03_RNASeq_differential_expression_analysis/ID_Attribute_gff.png)

In this gff file, the ID attribute is __ID__. So replace __gene_Id__ with __ID__

![ID_Attribute](https://github.com/statonlab/dibbs/blob/master/p03_RNASeq_differential_expression_analysis/ID-Attribute.png)



[useful link](https://github.com/bgruening/training-material/blob/master/rna-seq/rna-seq.md)
