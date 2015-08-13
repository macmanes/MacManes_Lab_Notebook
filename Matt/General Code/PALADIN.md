Paladin
--

```
cd data/
wget ftp://ftp.uniprot.org/pub/databases/uniprot/current_release/knowledgebase/complete/uniprot_sprot.fasta.gz
gzip -d uniprot_sprot.fasta.gz
cd ..
paladin index -r2 data/uniprot_sprot.fasta
```

TESTS
--

These data: http://metagenomics.anl.gov/?page=MetagenomeOverview&metagenome=4520320.3


in `/mouse/PALADIN/data`

	cat 4520320.R1.fq 4520320.R2.fq > merged.fq

	grep -c @M merged.fq #how many reads are in the merged fastQ
	294088


	/share/pear-0.9.6-bin-64/pear-0.9.6-bin-64 -j 10 -f 4520320.R1.fq -r 4520320.R2.fq -o 4520320_merged	
	
```
 ____  _____    _    ____
|  _ \| ____|  / \  |  _ \
| |_) |  _|   / _ \ | |_) |
|  __/| |___ / ___ \|  _ <
|_|   |_____/_/   \_\_| \_\

PEAR v0.9.6 [January 15, 2015]

Citation - PEAR: a fast and accurate Illumina Paired-End reAd mergeR
Zhang et al (2014) Bioinformatics 30(5): 614-620 | doi:10.1093/bioinformatics/btt593

Forward reads file.................: 4520320.R1.fq
Reverse reads file.................: 4520320.R2.fq
PHRED..............................: 33
Using empirical frequencies........: YES
Statistical method.................: OES
Maximum assembly length............: 999999
Minimum assembly length............: 50
p-value............................: 0.010000
Quality score threshold (trimming).: 0
Minimum read size after trimming...: 1
Maximal ratio of uncalled bases....: 1.000000
Minimum overlap....................: 10
Scoring method.....................: Scaled score
Threads............................: 10

Allocating memory..................: 200,000,000 bytes
Computing empirical frequencies....: DONE
  A: 0.215552
  C: 0.298214
  G: 0.287161
  T: 0.199073
  5542 uncalled bases
Assemblying reads: 100%

Assembled reads ...................: 135,769 / 147,044 (92.332%)
Discarded reads ...................: 0 / 147,044 (0.000%)
Not assembled reads ...............: 11,275 / 147,044 (7.668%)
Assembled reads file...............: 4520320_merged.assembled.fastq
Discarded reads file...............: 4520320_merged.discarded.fastq
Unassembled forward reads file.....: 4520320_merged.unassembled.forward.fastq
Unassembled reverse reads file.....: 4520320_merged.unassembled.reverse.fastq
```

	grep -c @M 4520320_merged.assembled.fastq #how many reads are in the PEAR'd fastQ
	135769
	
PALADIN test
--

	paladin align -u 2 data/uniprot_sprot.fasta data/merged.fq > merged_paladin.txt
	

	#number of hits
	
	awk '{ sum += $1 } END { print sum }' merged_paladin.txt
	297183 (294k original reads)


	93698 entries to UniProt

-
	paladin align -t 4 -u 2 data/uniprot_sprot.fasta data/4520320_merged.assembled.fastq > pear_paladin2.txt

	awk '{ sum += $1 } END { print sum }' pear_paladin.txt
	164996 (139k original reads)

	81695 entries to UniProt
	
comparison of uniprot results
--

```
head pear_paladin.txt merged_paladin.txt
==> pear_paladin.txt <==
Count	UniProtKB	ID	Organism	Protein Names	Genes	Pathway	Features	Gene Ontology	Reviewd	Existence	Comments
324	sp|P85153|CO2A1_MAMAE
243	sp|P0C2W2|CO1A1_TYREX
233	sp|P49756|RBM25_HUMAN
222	sp|P19275|VTP3_TTV1V
213	sp|B2RY56|RBM25_MOUSE
182	sp|P16274|IFEA_HELPO
180	sp|Q54YZ9|DHKJ_DICDI
173	sp|Q86AH4|Y8592_DICDI
168	sp|P04917|SRGN_RAT

==> merged_paladin.txt <==
Count	UniProtKB	ID	Organism	Protein Names	Genes	Pathway	Features	Gene Ontology	Reviewd	Existence	Comments
3017	sp|P85153|CO2A1_MAMAE
2344	sp|P0C2W2|CO1A1_TYREX
1463	sp|P16274|IFEA_HELPO
1036	sp|O19816|MATK_ALLCA
898	sp|P14277|CB2F_SOLLC
830	sp|P14274|CB2A_SOLLC
814	sp|P14276|CB2E_SOLLC
771	sp|P14275|CB2C_SOLLC
513	sp|O48085|CYB_ERYTA

```

sample_data

```
make_check
	cd sample_data && \
	paladin prepare -r0 && \ 
	paladin align -t 4 -u 2 uniprot_sprot.fasta.gz sample_data/4520320_merged.assembled.fastq.gz > paladin_uniprot_report.txt
```



version 1.0.0
--

```
paladin prepare -r0

curl http://api.metagenomics.anl.gov//download/mgm4520306.3?file=050.1 > root_S13.R1.fq

curl http://api.metagenomics.anl.gov//download/mgm4520307.3?file=050.1 > root_S13.R2.fq


pip install --upgrade setuptools
pip install khmer

interleave-reads.py root_S13.R1.fq root_S13.R2.fq > interleaved.fq

```



















