	java -Xmx200g -jar /share/Trimmomatic-0.32/trimmomatic-0.32.jar PE \  
	-phred33 -threads 32 -baseout clam_trim \  
	clam_1.fq \  
	clam_2.fq \  
	ILLUMINACLIP:/share/Trimmomatic-0.32/barcodes.fa:2:40:15 \  
	LEADING:2 \  
	TRAILING:2 \  
	SLIDINGWINDOW:4:2 \  
	MINLEN:25
	

Input Read Pairs: 4762093 Both Surviving: 540972 (11.36%) Forward Only Surviving: 76763 (1.61%) Reverse Only Surviving: 49732 (1.04%) Dropped: 4094626 (85.98%)

Something is seriously wrong with these data. Quality v. low, GC fucked up. amongst other things, there is a ton of adapter contamination. 



Trinity assembly:

	