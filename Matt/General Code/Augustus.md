This is the code for running the training module of Augustus

	~/augustus-3.0.2/scripts/autoAug.pl --genome=jelly.out.fasta --pasa --pasapolyAhints -singleCPU --cdna=augustus.complete.cds --species=peer --utr --hints=augustus.gff3 --optrounds=2

	export PASAHOME

	~/augustus-3.0.2/scripts/autoAug.pl --genome jelly.out.fasta --species peer --hints augustus.gff3 --optrounds 2 --trainingset augustus.complete.cds --singleCPU

	macmanes@macmanes:/media/macmanes/hd3/pero-genome/augustus$ ~/augustus-3.0.2/scripts/autoAug.pl --genome jelly.out.fasta --pasa --pasapolyAhints -singleCPU --cdna augustus.complete.cds --species peer --utr --hints augustus.gff3 --optrounds 2