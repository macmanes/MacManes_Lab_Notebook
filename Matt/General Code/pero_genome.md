	java -Xmx300g -jar /share/Trimmomatic-0.32/trimmomatic-0.32.jar PE \
	-threads 20 -baseout peroL1 \
	$RAID/macmanes/pero_genome/131008/pero360_L1.1.fq \
	$RAID/macmanes/pero_genome/131008/pero360_L1.2.fq \
	ILLUMINACLIP:/share/Trimmomatic-0.32/barcodes.fa:2:40:15 \
	LEADING:2 TRAILING:2 SLIDINGWINDOW:4:2 MINLEN:75
	
L1
--
Input Read Pairs: 108590493 Both Surviving: 107858557 (99.33%) Forward Only Surviving: 334901 (0.31%) Reverse Only Surviving: 314832 (0.29%) Dropped: 82203 (0.08%)
TrimmomaticPE: Completed successfully

L2
--
Input Read Pairs: 101221019 Both Surviving: 93383010 (92.26%) Forward Only Surviving: 3130088 (3.09%) Reverse Only Surviving: 293458 (0.29%) Dropped: 4414463 (4.36%)
TrimmomaticPE: Completed successfully

