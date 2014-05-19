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
number contigs - used sed to remove extra characters.
run mapping
omega.sh

omegaMap
--


	nohup /home/macmanes/pero_transcriptome/omega.sh -f pero.transdecoder.cds -o omega.ini -t 40 &

