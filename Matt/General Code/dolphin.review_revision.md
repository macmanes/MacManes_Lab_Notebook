Dolphin Revision Review 
--



I continue to assert that an unreplicated RNAseq study is simply not scientifically sound. The assemblies and sequence data are very valuable and need to be published, but the analysis of differential expression is unsound. I could accept the inclusion of these data but only is there were a **very** strong disclaimer (e.g. Differences could be the result of any of the following: the animals were deceased, different ages, different sex, different reason for death, different time between death and tissue collection, etc.). This disclaimer is not currently included in the manuscript.

>I would suggest that the authors publish the trancriptomes, but remove the parts about differential expression and orthology as an unreplicated RNAseq study simply is not scientifically sound.  There is absolutely no way you can distinguish noise from signal in your experiment, given that you have n=1 for both. Even in a perfectly controlled experiment this would be the same. You're design is unfortunately not perfect, given the animals were deceased, different ages, different sex, different reason for death, different time between death and tissue collection. Any of these could result in differences in expression. 
 


1. Were the libraries made using a stranded or unstranded protocol? 

		In response, there are 2 different protocols that are commonly used to generate RNAseq libraries, stranded (where only 1 strand is used) and un-stranded, where the this info is unknown. This matters to the assembly process. See http://seqanswers.com/forums/showthread.php?t=28025 for more details.


2. BLASTn itself does not contain an algorithm for reciprocal best blast ID. How did you do this analysis?

		While you included some details in the response, these should be included in the manuscript. 
	
 
11. Are the assembled contigs deposited anywhere? They have to made available to the reviewers and readers. 

		These contigs are the primary output from this research. In my opinion, they **must** be deposited. It would be comparable to doing a study of histology and not releasing the microscope images. 



8. What specifically did you use as your input to DESeq? RPKM, count data, something else?

		RPKM is inappropriate as input into DESeq. These should be count data. This is a critical mistake and has to be corrected. See section 1 of http://bioconductor.org/packages/release/bioc/vignettes/DESeq/inst/doc/DESeq.pdf 

13. How did you find coding sequence, e.g. line 151?

		While you included some details in the response, these should be included in the manuscript. 

