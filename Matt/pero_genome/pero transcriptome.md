6 May 14
--

in `/mnt/data3/macmanes/pero_for_annont/pero_trancriptome` there is the final assembly file `pero.final.fas`

in this folder are express results for the different tissue types.

in Evernote, there are directions for how doing the ANGSD analysis. 

On Github, there is an omegav4.sh file for going the omega analyses. 

in `/mnt/data0/macmanes/pero_transcriptome`

	nohup /home/macmanes/pero_transcriptome/pero_trim_assembly.mk CPU=20 MEM=10 RUN=pero READ1=/mnt/data3/macmanes/pero_for_annont/Pero.1.fastq READ2=/mnt/data3/macmanes/pero_for_annont/Pero.2.fastq &

May 16 2014
--
	
Raw Assembly:

		n:500	n:N50	min	N80	N50	N20	E-size	max sum name
	690000	219501	42411	500	825	1978	4510	2866	32647	316e6	pero.Trinity.fasta

there are 104735 contigs with TMP>1

	/mnt/data3/macmanes/pero_trans_assembly/pero.xprs$ cat results.xprs | awk '1>$15{next}1' | awk '{print $2}' | sed '1,1d' > list

Will exrtact those from full assembly. 

	sed ':begin;$!N;/[ACTGNn-]\n[ACTGNn-]/s/\n//;tbegin;P;D' pero.Trinity.fasta > pero.Trinity.fa # unwrap fasta
	
	for i in `cat pero.xprs/list`; do  grep --max-count=1 -A1 $i pero.Trinity.fa >> pero.final.fa; done &
	
Run Transdecoder
-
	nohup TransDecoder --CPU 50 -t pero.Trinity.fasta -S --search_pfam /share/transdecoder_rel16JAN2014/pfam/Pfam-AB.hmm.bin
	
extract complete and 3prime (has start codon) CDS - 50k of these

**number contigs - used sed to remove extra characters.**


>>run mapping


	$HOME/pero_transcriptome/pero_mapping.mk -j 4 CPU=10 REF=pero.transdecoder.cds


>> run omega.sh


	nohup /home/macmanes/pero_transcriptome/omega.sh -f pero.transdecoder.cds -o omega.ini -t 40 &
	for i in `ls om*out`; do summarize 2000 $i > $i.results; done
<<<<<<< HEAD
	for i in `ls omega/om*results`; do sed -n '4p' $i >> summary.file; done
	
=======
	for i in `ls om*results`; do sed -n '4p' $i >> summary.file; done
	for i in `ls om*results`; do F=`basename $i .out.results`; echo $F >> names.fa; done; paste names.fa summary.file > selection.txt
	cat selection.txt |  awk '0.5>$6{next}1' | awk '{print $1 "\t" $4 "\t" $6}'
>>>>>>> FETCH_HEAD



angsd
--
	
>> in `/mnt/data0/macmanes/pero_mapping_omega/bams`


	angsd -bam list -doSaf 1 -anc ../pero.transdecoder.cds  -GL 2 -P 14 -out outFold -fold 1
	/share/angsd0.598/misc/emOptim2 outFold.saf 11 -P 12 > outFold.sfs
	angsd -bam list -out outFold -doThetas 1 -doSaf 1 -pest outFold.sfs -anc ../pero.transdecoder.cds -GL 2 -fold 1