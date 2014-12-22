Starling genome evaluation
---

in `/mouse/starling/reapr`


> **AllPaths Assembly** NO gap filling, PB inclusions, etc. 


	reapr smaltmap -n 15 Starling_MacManes_AllPathsLG.fasta.facheck.fa \
	/mnt/data3/macmanes/starling/illumina/paired_end/Liver500.corr.trim_1P.fq \
	/mnt/data3/macmanes/starling/illumina/paired_end/Liver500.corr.trim_2P.fq \
	allpaths.starling.bam
	
	reapr pipeline Starling_MacManes_AllPathsLG.fasta.facheck.fa allpaths.starling.bam allpaths
	
> **ABySS Assembly**

	reapr smaltmap -n 15 ../starling.abyss.gapfilled.ectools.fasta \
	/mnt/data3/macmanes/starling/illumina/paired_end/Liver500.corr.trim_1P.fq \
	/mnt/data3/macmanes/starling/illumina/paired_end/Liver500.corr.trim_2P.fq \
	abyss.starling.bam
	
	reapr pipeline ../starling.abyss.gapfilled.ectools.fasta abyss.starling.bam abyss
