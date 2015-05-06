sync blast output
-

Transdocoder

Mus

	TransDecoder --CPU 20 Mus_musculus.GRCm38.75.cdna.all.fa  --search_pfam /share/transdecoder_rel16JAN2014/pfam/Pfam-AB.hmm.bin
Rat

	TransDecoder --CPU 15 -t Rattus_norvegicus.Rnor_5.0.75.cdna.all.fa  --search_pfam /share/transdecoder_rel16JAN2014/pfam/Pfam-AB.hmm.bin
leucopus

	TransDecoder --CPU 15 -t Pleucopus_Transcriptome_Contigs.fasta  --search_pfam /share/transdecoder_rel16JAN2014/pfam/Pfam-AB.hmm.bin &	
PEMA:

	##Need to do
	TransDecoder --CPU 15 -t Pleucopus_Transcriptome_Contigs.fasta  --search_pfam /share/transdecoder_rel16JAN2014/pfam/Pfam-AB.hmm.bin &

**Need to extract out complete and 3' contigs**

>> unwrap

>> grep

BLAST


--
--
--
--
--
--
--

BLAST LEUCOPUS-MUS

	blastn -db mus -query ../leucopus/leucopus.cds -evalue 1e-50 -num_threads 32 -outfmt "6 qseqid sacc slen length" -max_hsps 1 -max_target_seqs 1 > mus-pele.blast


BLAST PEMA-MUS

	blastn -db mus -query ../pema/pema.cds -evalue 1e-50 -num_threads 32 -outfmt "6 qseqid sacc slen length" -max_hsps 1 -max_target_seqs 1 > mus-pema.blast
	
BLAST PEER-MUS

	blastn -db mus -query ../peer/peer.genes.fasta -evalue 1e-50 -num_threads 32 -outfmt "6 qseqid sacc slen length" -max_hsps 1 -max_target_seqs 1 > mus-peer.blast

BLAST PEER-RAT

	blastn -db mus -query ../rat/rat.cds \
	-evalue 1e-50 -num_threads 32 \
	-outfmt "6 qseqid sacc slen length" \
	-max_hsps 1 -max_target_seqs 1 > mus-rat.blast

Format BLAST

	cat mus-pema.blast | awk '.8>$4/$3{next}1' > mus-pema-good.blast
	cat mus-peer.blast | awk '.8>$4/$3{next}1' > mus-peer-good.blast
	cat mus-rat.blast | awk '.8>$4/$3{next}1' > mus-rat-good.blast
	cat mus-pele.blast | awk '.8>$4/$3{next}1' > mus-pele-good.blast
	

SYNC THE 2 BLAST RESULTS FILES

	total=19074
	n=1
	while [ $n -lt $total ]; do
		var1=$(sed -n "${n}p" mus-pema-good.blast | awk '{print $1 "\t" $2}')
		echo $var1 > tmp
		var3=$(awk '{print $2}' tmp)
		grep -w --max-count=1 $var3 mus-rat-good.blast | paste - tmp >> mus.rat.pema.blast
		echo "Line $n = $var1"
		let n=n+1
	done


EXTRACT HITS WHERE ALL ARE PRESENT

	grep ^'cds.ENSR' mus.rat.pema.blast > mus.rat.pema.blast.final



SYNC THE 3rd BLAST RESULTS file to the other one

	total=19074
	n=1
	while [ $n -lt $total ]; do
		var1=$(sed -n "${n}p" mus-peer-good.blast | awk '{print $1 "\t" $2}')
		echo $var1 > tmp
		var3=$(awk '{print $2}' tmp)
		grep -w --max-count=1 $var3 mus.rat.pema.blast.final | paste - tmp >> mus.peer.pema.rat.blast
		echo "Line $n = $var1"
		let n=n+1
	done





EXTRACT HITS WHERE ALL ARE PRESENT & FORMAT

	grep ^'cds.ENSR' mus.peer.pema.rat.blast > mus.peer.pema.rat.blast.final
	cat mus.peer.pema.rat.blast.final | awk '{print $1 "\t" $2 "\t" $7 "\t" $13}' > 4species.blast





SYNC FILES TO GET FASTA OUTPUT	

	#!/bin/bash

	total=13000
	n=1
	while [ $n -lt $total ]; do
		var1=$(sed -n "${n}p" 4s.blast)
		echo $var1 > tmp
		var2=$(awk '{print $1}' tmp)
		var3=$(awk '{print $2}' tmp)
		var4=$(awk '{print $3}' tmp)
		var5=$(awk '{print $4}' tmp)
		grep -A1 -w --max-count=1 $var2 ../rat/rat.cds > ../4sp-coding/aligned/$n.hits.fa
		grep -A1 -w --max-count=1 $var3 ../mus/mus.cds >> ../4sp-coding/aligned/$n.hits.fa
		grep -A1 -w --max-count=1 $var4 ../pema/pema.cds >> ../4sp-coding/aligned/$n.hits.fa
		grep -A1 -w --max-count=1 '>'$var5 ../peer/peer.genes.fasta >> ../4sp-coding/aligned/$n.hits.fa
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

	$HOME/pero_transcriptome/sync.branch.site.sh

This gives you:

	1.hits.out 	 branch-site 	 0 	 1.00000
	2.hits.out 	 branch-site 	 0 	 1.00000
	3.hits.out 	 branch-site 	 0 	 1.00000
	4.hits.out 	 branch-site 	 0 	 1.00000
	5.hits.out 	 branch-site 	 2.6e-05 	 1.07268
	6.hits.out 	 branch-site 	 0 	 1.00000


Critical Value is:

	/share/paml4.8/src/chi2 2 22.6
	> p.adjust(0.000012373, method='BH', n=4000)
	[1] 0.049492

Get sig hits #there are 164 using star, 86 using real phylogeny
	cat branch-site.txt | sort -rnk 3 | more


	for i in `awk '{print $1}' sig.hits.star.txt | awk -F "." '{print $1}'`; do sed -n '7p' aligned/$i.hits.fa; done




















