Pero Revisions
--

in `/mnt/data3/macmanes/pero_trans_paper/merged/omega/`

	grep -A1 Transcript_49049 ../Pero.BLTK.fasta
	
	TransDecoder -t Hnrnph1.fa
	
	java -Xmx1000m -jar /share/bin/macse_v1.01b.jar \
	-prog alignSequences -seq Hnrnph1.fa.transdecoder.cds \
	-out_NT Hnrnph1.fa.transdecoder.cds.aln


	python ../fa2phy.py aqp9.aln aqp9.phy
	
	codeml