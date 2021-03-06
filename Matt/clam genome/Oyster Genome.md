Trimming

	
	java -Xmx400g -jar /share/Trimmomatic-0.32/trimmomatic-0.32.jar PE \
	-phred33 -threads 64 -baseout oyster_trim \
	$RAID/macmanes/oyster_genome/1914-KO-1_1_sequence.fq \
	$RAID/macmanes/oyster_genome/1914-KO-1_2_sequence.fq \
	ILLUMINACLIP:/share/Trimmomatic-0.32/barcodes.fa:2:40:15 \
	LEADING:2 \
	TRAILING:2 \
	SLIDINGWINDOW:4:2 \
	MINLEN:55  
	

	Input Read Pairs: 594639181 Both Surviving: 492330600 (82.79%) Forward Only Surviving: 2599252 (0.44%) Reverse Only Surviving: 98602465 (16.58%) Dropped: 1106864 (0.19%)

split

	cat /mnt/data3/macmanes/oyster_genome/oyster_trim_* | split -l 80000000
	
Assemble unitigs:

	nohup for k in 75
		do cd $HOME/oyster/oyster$k; mpirun -np 64 ABYSS-P -k$k --coverage-hist=k$k.hist \
		-o oyster$k reads/x*
	done & 
	
Assemble scaffolds:

	nohup for k in 75 71 65
		do cd $HOME/oyster/oyster$k; mpirun -np 32 abyss-pe j=32 v=-v k=$k name=oyster$k n=5 lib='oyster' \
		oyster='$$RAID/macmanes/oyster_genome/oyster_trim_1P $$RAID/macmanes/oyster_genome/oyster_trim_2P' \
		se='$$RAID/macmanes/oyster_genome/oyster_trim_1U $$RAID/macmanes/oyster_genome/oyster_trim_2U'
	done &


SGA preqc

	sga preprocess --pe-mode 1 $RAID/macmanes/oyster_genome/oyster_trim_1P $RAID/macmanes/oyster_genome/oyster_trim_2P > clam.fq
	sga index -a ropebwt --no-reverse -t 32 clam.fq
	sga preqc -t 32 clam.fq > clam.preqc
	/share/sga/src/bin/sga-preqc-report.py clam.preqc /share/sga/src/examples/preqc/*.preqc