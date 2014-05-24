sync blast output
-

BLAST

	blastn -db peer -query pema/rna.fa -evalue 1e-50 -num_threads 32 -outfmt "6 qseqid stitle pident slen length evalue" -max_hsps 1 -max_target_seqs 1 > peer-pema.blast
	
BLAST2

	blastn -db pema -query ../mus/Mus_musculus.GRCm38.75.cdna.all.fa -evalue 1e-50 -num_threads 32 -outfmt "6 qseqid stitle pident slen length evalue" -max_hsps 1 -max_target_seqs 1 > mus-pema.blast

Format BLAST

	cat peer-pema.blast | awk '.9>$6/$5{next}1' > peer-pema-good.blast
	cat mus-pema.blast | awk '.9>$6/$5{next}1' > mus-pema-good.blast
	

SYNC THE 2 BLAST RESULTS FILES

	total=15000
	n=1
	while [ $n -lt $total ]; do
		var1=$(sed -n "${n}p" mus-pema-good.blast)
		echo $var1 > tmp
		var3=$(awk '{print $2}' tmp)
		grep -w --max-count=1 $var3 peer-pema-good.blast | paste - tmp >> mus.peer.pema.blast
		echo "Line $n = $var1"
		let n=n+1
	done





EXTRACT HITS WHERE ALL ARE PRESANT & FORMAT

	grep ^'gi|' mus.peer.pema.blast > mus.peer.pema.blast.final
	cat mus.peer.pema.blast.final | awk '{print $1 "\t" $8 "\t" $2 "\t" $3}' > 3species.blast





SYNC FILES TO GET FASTA OUTPUT	

	#!/bin/bash

	total=13000
	n=1
	while [ $n -lt $total ]; do
		var1=$(sed -n "${n}p" 3species.blast)
		echo $var1 > tmp
		var2=$(awk '{print $1}' tmp)
		var3=$(awk '{print $2}' tmp)
		var4=$(awk '{print $3}' tmp)
		grep -A1 -w --max-count=1 $var2 ../pema/pema.rna.fa > ../ortholog/$n.hits.fa
		grep -A1 -w --max-count=1 $var4 ../peer/peer.genes.fasta >> ../ortholog/$n.hits.fa
		grep -A1 -w --max-count=1 $var3 ../mus/mus.genes.fa >> ../ortholog/$n.hits.fa
		echo "Line $n = $var1"
		let n=n+1
	done


PAML Process

1. macse alignment
2. get rid of !
3. change names to pema, peer, mus

	`sed -i "s/ENS.*/mus/g" 1014.hits.fa`
	`sed -i "s/gi.*/pema/g" 1014.hits.fa`
	`sed -i "s/[0-9].*/peer/g" 1014.hits.fa`
4. make newick tree with #1
	`((peer #1, pema), mus)`
5. fq2phy
6. codeml.ctl



























