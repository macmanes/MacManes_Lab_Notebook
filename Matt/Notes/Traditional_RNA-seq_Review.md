Traditional RNA-seq versus 3' RNA-seq review
--

General Comments:

- I worry that the 3' procedure as described is of limited value, at least as it is described here. It performs worse in many of the evaluated metrics (contigs length, %annotated, mapping, expression quantitation, etc). While it resulted in more DE genes, until the authors can demonstrate that these DE genes are not false positives, most readers, including myself will be very suspicious.

- The code need to be made available. This includes all of the in-house scripts. Available from the author is generally not sufficient. Many free repositories for this information exist (e.g. GitHub). Methods sections should be detailed enough to allow the reader to replicate your experiment. When these types of scripts are used and not presented you violate one of the most basic principles of scientific publishing. 

- The data (sequencing reads and assembled transcriptomes) had to be made available in public repositories (FigShare/Dryad/NCBI, etc)

- A study that lacks biological replicates has very little ability to speak to the biological phenomenon under consideration. I fear that nobody will ever be convinced of anything given no replicates. 

- There are numerous typos and misspellings. 

- There are many serious issues with the methods (described below)

- Given the un-replicated design, that you find more DE genes in the 3' design is **extremely** unconvincing. This seems much more likely to be the result of false positives, though you likely have great difficulty trying to disentangle the 2. 


> Methods
- RNA seq experiments
	- The classic Illumina protocol poly-A selection followed by fragmentation, then cDNA synthesis. This is different from the authors 3' protocol, which involves fragmentation THEN poly A selection (order reversed), and cDNA synthesis. I suppose that this *could* work for quantitation, but this assumes that the polyA selection process is highly efficient and specific to polyA tails, but that (for instance) a significant number of reads derived from rRNA exist in polyA selected samples suggests that this is not the case.
	- Was the library made in a stranded or unstranded fashion? 
- Preprocessing of reads:
	- On what type of machine were the reads produced. 
	- what is the read length
	- what was the total number of reads used for the analyses
	- were adapters trimmed and how? (in house scripts not made available NOT acceptable)
	- Why was the Phred trimming threshold of 20 chosen, given there is substantial evidence (e.g. http://www.ncbi.nlm.nih.gov/pmc/articles/PMC3908319/ and http://www.ncbi.nlm.nih.gov/pubmed/24575122) that this is detrimental to assemblies? Should change this at a minimum justify your approach. 
- Counting the poly(A)-rich reads
	- where is the 'in house python script' deposited? 
	- What was the threshold of % A's that you used for inclusion into the study?
	- how were the reads mapped (what command used)?
	- what version of bowtie was used?
	- you mention mapping against contigs before you describe where these contigs came from. 
- De novo assembly
	- What version of trinity was used?
	- What Trinity command was used?
	- How did you do the 'read collapsing'?
	- what proportion of the reads were removed by the collapsing procedure?
	- How do you know there was no reduction in accuracy using the collapsing procedure? 
	- Again, the use of unavailable in house perl scripts is not acceptable. 
	- what version of blast was used?
- Abundance estimation
	- It is impossible to evaluate this section without the script you used.
- Differentially Expressed
	- What version of edgeR and R did you use?
	- What commands did you use to test for differential expression?
	
---

> Results
- Comparison of expression profiles
	- "We found more DE contigs with the 3' RNA-seq (~ 1.57 times more) than with the standard RNA-seq (Table 5 & Fig. 5). This suggests that we potentially have greater power to detect DE contigs with the 3' RNA-seq." CRITICALLY: how can you say this without considering the potential for increase in false positives. In an unreplicated design, I find this **extremely** unconvincing! 