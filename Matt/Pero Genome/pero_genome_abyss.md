Pero_ABySS and Aggressive Trimming Trimming
--

Trimmomatic PE data

    java -Xmx300g -jar /share/Trimmomatic-0.32/trimmomatic-0.32.jar PE \
    -threads 40 -baseout Pero360_550bp.P20.gz \
    $RAID/pero_genome/raw_reasd/nygc.550.1.cor.fq.gz \
    $RAID/pero_genome/raw_reasd/nygc.550.2.cor.fq.gz \
    LEADING:20 TRAILING:20 SLIDINGWINDOW:4:10 MINLEN:25
    
and 

    java -Xmx300g -jar /share/Trimmomatic-0.32/trimmomatic-0.32.jar PE \
    -threads 40 -baseout Pero360_300bp.P20.gz \
    $RAID/pero_genome/raw_reasd/hcgs.300.1.cor.fq \
    $RAID/pero_genome/raw_reasd/hcgs.300.2.cor.fq \
    LEADING:20 TRAILING:20 SLIDINGWINDOW:4:10 MINLEN:25

ABySS
--

	export TMPDIR=/mnt/data0/	

	for k in 71 81 91; do
		mkdir k$k
		abyss-pe -C k$k np=40 k=$k name=pero$k l=25 n=5 \
		lib='pe1 pe2' mp1_l=30 mp1_l=30 mp3_l=30 mp4_l=30 \
		mp='mp1 mp2 mp3 mp4' long=long1 v=-v \  
		pe1='$RAID/pero_genome/raw_reasd/Pero360_550bp.P20_1P.gz \
		$RAID/pero_genome/raw_reasd/Pero360_550bp.P20_2P.gz' \
		pe2='$RAID/pero_genome/raw_reasd/Pero360_300bp.P20_1P.gz \
		$RAID/pero_genome/raw_reasd/Pero360_300bp.P20_2P.gz' \
		mp1='$RAID/pero_genome/raw_reasd/peer5kb.clipped.1.fq \
		$RAID/pero_genome/raw_reasd/peer5kb.clipped.2.fq' \
		mp2='$RAID/pero_genome/raw_reasd/peer8kb.clipped.1.fq \
		$RAID/pero_genome/raw_reasd/peer8kb.clipped.2.fq' \
		mp3='$RAID/pero_genome/raw_reasd/peer7kb.clipped.1.fq \
		$RAID/pero_genome/raw_reasd/peer7kb.clipped.2.fq' \
		mp4='$RAID/pero_genome/raw_reasd/peer3kb.clipped.1.fq \
		$RAID/pero_genome/raw_reasd/peer3kb.clipped.2.fq' \


	
	
	
	
		long1=''
		
		
		
