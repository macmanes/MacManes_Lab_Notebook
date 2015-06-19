RCorrector Review
--

The manuscript under review, written by Li Song and Liliana Florea describe a new software contribution -- Rcorrector. This is a well written manuscript and the authors have a demonstrated track record of writing similar excellent software for correction of WGS reads (Lighter). The authors rightly identify an important gap in our technical tool box, that few RNAseq correction tools exist and the one that does exist uses a tremendous amount of RAM and time thus making it infeasible for many users. 

I fully expect that this software will be extremely useful and impactful, though I could not exactly get it to work, as described below.


Manuscript
--
0. Minor pedantic issue, but Rcorrector makes me think the software is implemented in R (the stats package). Maybe this is not a big deal, but may cause some initial confusion for some..
1. There are many places in the introduction that lack citations. For instance
	- ".. error correction of whole genome sequencing proven to increase the quality .." 
	- ".. biases and errors .. can significantly impact bioinforrmatic analyses .. "
	- " .. error correctors for WGS reads are generally not well suited for RNAseq .." - see http://biorxiv.org/content/early/2015/05/29/020123 and https://peerj.com/articles/113/. There are other papers that speak to this point, but I obviously know mine best so I list them here. 
	
2. When you talk about the 3 methods for error correction (MSA, suffix tree, kmer spectra) you should include SEECER in the appropriate category.  

3. For the read datasets:
	- What specific command did you use to generate the simulated reads?
	- Did you use the default kmer for Rcorrector?
	- what specific commands did you use for the other correction software. What kmer length did you use?
	- what specific command did you use in running TopHat?
	- What version and commands did you use for assembling using Oases? Did you do any kmer optimization?
	
4. Would you be willing to add in Heng Li's BFC error correction method to your paper? I found this to be quite good for RNAseq reads using my metrics and having you compare would make for a nice bridge between your paper and the rest of the literature. Not a hard requirement for review, just a suggestion/request. 

5. I think it would be really helpful if you included in the manuscript/github repo the code you used for the analysis of TP and FP. Basically how you want from SAM to the numbers in the table. This would go a long way towards making the manuscript fully reproducible. 

Software 
--


1. Make
	- why build.sh? Why not just a makefile that builds jellyfish 1st? It's fine, but slightly non standard.. 
	- Can you look to see if the appropriate version of Jellyfish is already in the users $PATH rather than just installing it again?

2. Help info
	- can you include a small test dataset to ensure help users check the installation has been successful?
	- `-r` is for single end reads, while `-p` is for paired end, I think? At a minimum this needs to be more explicit in the help info. You might consider a more canonical set of input flags, e.g., `-l` and `-r` or `-1` and `-2` with `-s` for single end reads. Make it a comma separated list if many files were being inputted


	```
	-1 pair1.1.fq,pair2.1.fq,pair3.1.fq -2 pair1.2.fq,pair2.2.fq,pair3.2.fq
	```
	
3. Running
	- can it handle interleaved read files properly?
	- No gzip input support? This is critical. 

	```
    perl /share/Rcorrector/run_rcorrector.pl -p raw.20M.SRR797058_1.fastq.gz raw.20M.SRR797058_2.fastq.gz
    Count the kmers
    terminate called after throwing an instance of 'std::runtime_error'
    what():  Unsupported format
    Failed to parse bloom filter file 'tmp.bc'
    Dump the kmers
    Failed to open input file 'tmp.mer_counts': No such file or directory
    ```
	- Using redirection seems to work (no error), but I it actually does not, as empty output files. It would be great for general streaming as well as it would be a way to implement gzip support. 


	```
	perl /share/Rcorrector/run_rcorrector.pl -p <(gzip -cd raw.20M.SRR797058_1.fastq.gz) \
	<(gzip -cd raw.20M.SRR797058_2.fastq.gz) -t 40
	Count the kmers
	Dump the kmers
	Error correction
	Processed 0 reads
        Corrected 0 bases.
	```
	- for setting threads, `-t40` != `-t 40`. When no space between the flag and integer, it is not parsed correctly. For instance, only 1 thread is used during jellyfish when flag is `-t40` (no space).
	- when I run an uncompressed read dataset that consists of 20M PE reads, I get 0 corrected. this is confirmed by a simple diff (lots of instances of unfixable_error). Something wrong here, but I'm not sure what. Other correction software will correct this dataset (in fact, this is the same 20M read dataset that is used in the bioRxiv paper listed above) Maybe do `jellyfish histo` for help troubleshooting? It is at least fast. 
	
	```
	perl /share/Rcorrector/run_rcorrector.pl -p test1.fq test2.fq -t 40
	Count the kmers
	Dump the kmers
	Error correction
	Processed 40000000 reads
        Corrected 0 bases.
	```
	- If `run_rcorrector.pl` fails (or is killed by user) during error correction but has completed the Jellyfish steps, Ideally when the program is restarted it would check to see if kmer counting or kmer dumping has been performed -- and if so, then not do those steps again.  