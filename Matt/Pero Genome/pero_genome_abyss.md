Pero_ABySS and Aggressive Trimming Trimming
--

Trimmomatic PE data

    java -Xmx300g -jar /share/Trimmomatic-0.32/trimmomatic-0.32.jar PE \
    -threads 40 -baseout Pero360_550bp.P20.gz \
    $RAID/pero_genome/raw_reasd/nygc.550.1.cor.fq.gz \
    $RAID/pero_genome/raw_reasd/nygc.550.2.cor.fq.gz \
    LEADING:20 TRAILING:20 SLIDINGWINDOW:4:10 MINLEN:25
    
Input Read Pairs: 276768820 Both Surviving: 276742084 (99.99%) Forward Only Surviving: 14493 (0.01%) Reverse Only Surviving: 12237 (0.00%) Dropped: 6 (0.00%)
    
and 

    java -Xmx300g -jar /share/Trimmomatic-0.32/trimmomatic-0.32.jar PE \
    -threads 20 -baseout Pero360_300bp.P20.gz \
    $RAID/pero_genome/raw_reasd/hcgs.300.1.cor.fq \
    $RAID/pero_genome/raw_reasd/hcgs.300.2.cor.fq \
    LEADING:20 TRAILING:20 SLIDINGWINDOW:4:10 MINLEN:25


Input Read Pairs: 636610594 Both Surviving: 614893659 (96.59%) Forward Only Surviving: 21535179 (3.38%) Reverse Only Surviving: 145136 (0.02%) Dropped: 36620 (0.01%)

ABySS
--

	export TMPDIR=/mnt/data0/	

	split -l 116000000 --additional-suffix=aaa <(zcat ../Pero360_550bp*gz) &
	split -l 116000000 --additional-suffix=zzz <(zcat ../Pero360_300bp*{P,U}.gz) &

	for k in 91 71 81; do
		mkdir /mouse/abyss/k$k
		cd /mouse/abyss/k$k
		mpirun -np 64 ABYSS-P -v -k$k \
		--coverage-hist=coverage.hist \
		-o peer$k-1.fa /mnt/data3/macmanes/pero_genome/raw_reasd/split/*;
	done




	for k in 91; do
		abyss-pe -C k$k np=40 k=$k name=peer$k l=25 n=5 \
		lib='pe1 pe2' mp1_l=30 mp1_l=30 mp3_l=30 mp4_l=30 \
		mp='mp1 mp2 mp3 mp4' long=long1 v=-v \
		pe1='$$RAID/pero_genome/raw_reasd/Pero360_550bp.P20_1P.gz \
		$$RAID/pero_genome/raw_reasd/Pero360_550bp.P20_2P.gz' \
		pe2='$$RAID/pero_genome/raw_reasd/Pero360_300bp.P20_1P.gz \
		$$RAID/pero_genome/raw_reasd/Pero360_300bp.P20_2P.gz' \
		mp1='$$RAID/pero_genome/raw_reasd/peer5kb.clipped.1.fq \
		$$RAID/pero_genome/raw_reasd/peer5kb.clipped.2.fq' \
		mp2='$$RAID/pero_genome/raw_reasd/peer8kb.clipped.1.fq \
		$$RAID/pero_genome/raw_reasd/peer8kb.clipped.2.fq' \
		mp3='$$RAID/pero_genome/raw_reasd/peer7kb.clipped.1.fq \
		$$RAID/pero_genome/raw_reasd/peer7kb.clipped.2.fq' \
		mp4='$$RAID/pero_genome/raw_reasd/peer3kb.clipped.1.fq \
		$$RAID/pero_genome/raw_reasd/peer3kb.clipped.2.fq' \
		long1='/mnt/data3/macmanes/pero_trans_paper/merged/mapping/Pero.BLTK.fasta';
	done
		
		
		
