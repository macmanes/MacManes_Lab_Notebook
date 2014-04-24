---
layout: post
category : lessons
tagline: "Supporting tagline"
tags : [Maker, CEGMA, Augustus, GeneMark]
---
{% include JB/setup %}


This is the code for running the training module of Augustus

	~/augustus-3.0.2/scripts/autoAug.pl --genome=jelly.out.fasta --pasa --pasapolyAhints -singleCPU --cdna=augustus.complete.cds --species=peer --utr --hints=augustus.gff3 --optrounds=2

	export PASAHOME

	~/augustus-3.0.2/scripts/autoAug.pl --genome jelly.out.fasta --species peer --hints augustus.gff3 --optrounds 2 --trainingset augustus.complete.cds --singleCPU

	macmanes@macmanes:/media/macmanes/hd3/pero-genome/augustus$ ~/augustus-3.0.2/scripts/autoAug.pl --genome jelly.out.fasta --pasa --pasapolyAhints -singleCPU --cdna augustus.complete.cds --species peer --utr --hints augustus.gff3 --optrounds 2
	
This is what I really did: (in `/media/macmanes/hd3/maker/augustus`)

	~/augustus-3.0.2/scripts/autoAug.pl --genome=../../pero-genome/jelly.out.fasta --species=peer \
	--cdna=../augustus.complete.cds --trainingset=../cegma/genome.gff3 --singleCPU -v --useexisting
	
I got an error message: `Number of training genes is with 17 too low (at least 100 genes required)! Training aborted.`

> I'll have to run maker on Blacklight a little *or maybe a lot* longer...


