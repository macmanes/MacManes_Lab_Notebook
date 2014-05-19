READemption Review
--

(.md formatted document)

>>General Comments

I have just finished reading the paper and running the software -- both are extremely well written. For researchers interested in using a pipeline for RNAseq,  who don't mind being locked into a single (more obscure?) mapper, this is perfect. It is clean that the authors have invested a lot of time into the online documentation, which is really wonderful! 

>>Specific Comments from Paper and Software

1. **Most Critically**, the pipeline does not trim sequencing adapters from reads, nor does it perform quality trimming (though care with this - see http://journal.frontiersin.org/Journal/10.3389/fgene.2014.00013/). These things could be included with `--align`, but don't seem to be currently, unless they are a part of `--segemehl_accuracy`. You should either state in the paper that adapters must be trimmed from the input read data prior to the pipeline, or do this task automatically.

2. Intro line 48-9 'and is about to replace microarrays'. Wording is awkward. I would say something like '..having been shown to be more powerful to detect changes in gene expression than microarrays (ref)'

3. I think it the paper (software) would be substantially improved by allowing users to use other mappers- I know that some of the authors are involved in the development of segemehl, but I am not sold on the quality of that aligner relative to other (for instance, bwa-mem or STAR) and I might be dissuaded from using READemption because of this. Mappers have come a long way since the 2009 segemehl paper was published, and while it was competitive then, maybe not now. I think it would be easy enough to make this change, given BAM file output. *This is a suggestion for improvement, but not a  requirement for publication*.  

4. I wish figure 1 were bigger. Particularly 1B- it is really too small to see.

5. I wish there were just a little more detail in the paper about what the software was doing - how the defaults were selected, how the data were being handled. I can see from the code what is happening, but the average person will not take that time. 

6. A few of the parameters have no default value listed (e.g. `--min_read_length` in `align`)

7. FWIW, I compiled the program on a standard installation of Ubuntu 14.04. The directions were clear and correct. I ran the test dataset and inspected the output files. Again, that such wonderful documentation existed was a huge strength.    

--Matt MacManes