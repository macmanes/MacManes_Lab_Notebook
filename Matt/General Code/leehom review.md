I have just finished reading the manuscript 'Adaptor trimming and merging for next-generation sequencing reads'. It is a fine work, proposing a novel extension to existing methods and may be useful for those working on aDNA. Below are my specific comments. 

--Matt MacManes


Review For NAR 'Adaptor Trimming and merging'
--

1. I think that the title is incongruous with the manuscript which focuses on the analysis of Ancient DNA. I would advise the reworking of the title to reflect this focus. Also, maybe include the name of the software in the title.

2. Introduction, line 37. Reference 1 should be placed at the end of the sentence, not after the words 'recent improvements'

3. Intro line 52: Merging is expected to reduce *sequencing* error, but not the more troublesome types of errors that are typical of aDNA, or PCR errors.

4. As it is right now, you cannot claim that the method is particularly useful for 'other cases where short molecules are sequenced;, given you've only tested with aDNA, which is special in it's properties. 

5. Regarding the prior in sequence length - would you advise the log-normal distribution for both aDNA and modern DNA? Under what circumstances would you advice a uniform prior? You should spell this out in the paper and in the software help info. 

6. Figure 2: xaxis 'data' needs to be changed. Is this molecule length? If so, if the molecule length of modern DNA really the length of the molecule that is sequenced, i.e. after Illumina library prep which includes fragmentation?

7. In fig2 legend Theoretical misspelled.

8. Page 4, col2, line 45. Don't you assume that sequencing error equally likely to produce *any nucleotide*, including the correct one. Not sure if this is a wording issue or a conceptual issue.

9. Page 5 col2 aDNA sequencing data: You refer to the previous section 'same programs were used as described in previous section'. I think the ordering of the sections has changed, since the previous section has to do with consensus generation of overlapping regions. 

10. I think the header 'results subsection one' can be removed.

11. What software did you use to simulate aDNA? Alternatively, where is the code. These simulated data should be made available.  

12. What BWa settings were used for mapping?

Software
--
Readme is succinct yet sufficient in most cases
git cloned successfully. 
Program builds on UBUNTU 14.04 following the instructions.
Test dataset runs as expected


1. In the output message, `Total 50000; Merged (trimming) 40542; Merged (overlap) 7376; Kept PE/SR 1953; Trimmed SR 0; Adapter dimers/chimeras 129; Failed Key 0` it might be good to describe in the README a little bit more what each of these categories means. 

2. When processing fastQ data, there is no output message describing the success or failure of the run. This should be included (like it is for processing BAM)

3. The `--scale` and `--loc` flags does not seem to work. `src/leeHom -f AGATCGGAAGAGCACACGTCTGAACTCCAG -s GGAAGAGCGTCGTGTAGGGAAAGAGTGTAG --ancientdna  --scale -o testData/reconsAncientDNA.bam testData/rawAncientDNA.bam` returns `Utils.cpp: destringify() Unable to convert string="-o"` I assume I am using these incorrectly, but there is no info about how to properly use.

4. Might be good to allow users to input adapter sequences via a fasta file (like Trimmomatic does). Perhaps possible to deduce the forward or reverse by /1 and /2 suffixes in fasta header? Will users ever want to test against many different adapters?

5. How does the BAM file need to be sorted? Would the std output from bowtie/bwa/novoalign work, or should it be sorted in some way. Should include this info in the readme.