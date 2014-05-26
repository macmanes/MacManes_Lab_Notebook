sync blast output
-

BLAST PEMA-MUS

	blastn -db mus -query ../pema/rna.fa -evalue 1e-50 -num_threads 32 -outfmt "6 qseqid sacc pident slen length evalue" -max_hsps 1 -max_target_seqs 1 > mus-pema.blast
	
BLAST PEER-MUS

	blastn -db mus -query ../peer/peer.genes.fasta -evalue 1e-50 -num_threads 32 -outfmt "6 qseqid sacc pident slen length evalue" -max_hsps 1 -max_target_seqs 1 > mus-peer.blast

BLAST PEER-RAT

	blastn -db mus -query ../rat/Rattus_norvegicus.Rnor_5.0.75.cds.all.fa \
	-evalue 1e-50 -num_threads 12 \
	-outfmt "6 qseqid sacc pident slen length evalue" \
	-max_hsps 1 -max_target_seqs 1 > mus-rat.blast

Format BLAST

	cat mus-pema.blast | awk '.8>$5/$4{next}1' > mus-pema-good.blast
	cat mus-peer.blast | awk '.8>$5/$4{next}1' > mus-peer-good.blast
	cat mus-rat.blast | awk '.8>$5/$4{next}1' > mus-rat-good.blast
	

SYNC THE 2 BLAST RESULTS FILES

	total=10074
	n=1
	while [ $n -lt $total ]; do
		var1=$(sed -n "${n}p" mus-pema-good.blast)
		echo $var1 > tmp
		var3=$(awk '{print $2}' tmp)
		grep -w --max-count=1 $var3 peer-pema-good.blast | paste - tmp >> mus.peer.pema.blast
		echo "Line $n = $var1"
		let n=n+1
	done


EXTRACT HITS WHERE ALL ARE PRESENT

	grep ^'gi|' mus.peer.pema.blast > mus.peer.pema.blast.final



SYNC THE 3rd BLAST RESULTS file to the other one

	total=12074
	n=1
	while [ $n -lt $total ]; do
		var1=$(sed -n "${n}p" rat-peer.blast)
		echo $var1 > tmp
		var3=$(awk '{print $2}' tmp)
		grep -w --max-count=1 $var3 mus.peer.pema.blast.final | paste - tmp >> mus.peer.pema.rat.blast
		echo "Line $n = $var1"
		let n=n+1
	done





EXTRACT HITS WHERE ALL ARE PRESENT & FORMAT

	grep ^'gi|' mus.peer.pema.rat.blast > mus.peer.pema.rat.blast.final
	cat mus.peer.pema.rat.blast.final | awk '{print $1 "\t" $2 "\t" $3 "\t" $8 "\t" $8}' > 4species.blast





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


PAML Models 0 1 2 7 8
-	

 in `/mnt/data0/macmanes/comparative_desert/`
 
	$HOME/pero_transcriptome/run_paml.sh -t 25

Process:

	$HOME/pero_transcriptome/process_paml.sh

M1.txt, M2.txt, M8.txt have results


BRANCH-SITE PAML
-

in `/mnt/data0/macmanes/comparative_desert/branch`

with codeml that sets `model = 2 NSsites = 2`

	$HOME/pero_transcriptome/run_paml.sh -t 25
	
Alternative model sets `omega=1`

	$HOME/pero_transcriptome/run_paml_branch.sh -t 40

Process results






















