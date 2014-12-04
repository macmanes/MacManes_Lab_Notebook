Mytilus Transcriptome
--

in `/mouse/Mytilus/raw_reads`

in `/mouse/Mytilus/working_reads/`

	at LesserM*R2*gz > mytilus.muscle.2.fq.gz
	at LesserM*R1*gz > mytilus.muscle.1.fq.gz
	at LesserG*R1*gz > mytilus.gill.1.fq.gz
	at LesserG*R2*gz > mytilus.gill.2.fq.gz	
	
> error Correction

	lighter -t 48 -r mytilus.muscle.1.fq.gz -r mytilus.muscle.2.fq.gz -k 25 6000000000 .1
	
> fastqc
		
	fastqc -t8 mytilus.muscle.2.fq.gz
	fastqc -t8 mytilus.muscle.1.fq.gz