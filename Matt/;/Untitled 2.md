in `/mnt/ebs_1/blast`


	sed -i ':begin;$!N;/[ACTGNn-]\n[ACTGNn-]/s/\n//;tbegin;P;D' trin.fasta
	
	for i in `cat trin.allsig.txt`; do grep -wA1 $i trin.fasta; done > trin.sig.contigs
	
	blastn -query trin.sig.contigs -db dmel -outfmt "6 qseqid stitle pident length evalue"   > trin.sig.blast
	
	for i in `cat soap.xprs.blast | sort -uk 1,1 | awk '{print $2}'`; do grep -w --max-count=1 $i trin.xprs.blast >> common; done
	


SOAP

	sed -i ':begin;$!N;/[ACTGNn-]\n[ACTGNn-]/s/\n//;tbegin;P;D' soap.fasta
	
	for i in `cat soap.allsig.txt`; do grep -wA1 $i soap.fasta; done > soap.sig.contigs
	
	blastn -query soap.sig.contigs -db dmel -outfmt "6 qseqid stitle pident length evalue"   > soap.sig.blast
	
	for i in `cat soap.sig.blast | sort -uk 1,1 | sort -uk 2,2 | awk '{print $2}'`; do grep -w --max-count=1 $i trin.sig.blast >> in.soap.and.trin; done
	


Trinity identified 146 diff expressed genes
86 of these are in SOAP. 

SOAP identified 104 uniq genes
75 of these were in the Trinity assembly












































