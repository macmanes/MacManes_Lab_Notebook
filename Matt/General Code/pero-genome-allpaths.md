 	
 	
 	
 	nohup PrepareAllPathsInputs.pl \
 	DATA_DIR=$RAID/macmanes/allpaths/peer/mydata/ \
 	GENOME_SIZE=2600000000 OVERWRITE=True PLOIDY=2 \
 	FRAG_COVERAGE=45 HOSTS=12 &
 	
in_groups.csv
--
       file_name, library_name, group_name
	/mnt/data3/macmanes/pero_genome/131008/peroL1_*P.fq,L1,      frags1
	/mnt/data3/macmanes/pero_genome/131008/peroL2_*P.fq,L1,      frags2
	/mnt/data3/macmanes/pero_genome/131023/peroL3_*P.fq,L1,      frags3
	/mnt/data3/macmanes/pero_genome/131219/peroL4_*P.fq,L1,      frags4
	/mnt/data3/macmanes/pero_genome/131219/peroL5_*P.fq,L1,      frags5
	/mnt/data3/macmanes/pero_genome/131008/peroL1_*U.fq,L1_UP,      frags6
	/mnt/data3/macmanes/pero_genome/131008/peroL2_*U.fq,L1_UP,      frags7
	/mnt/data3/macmanes/pero_genome/131023/peroL3_*U.fq,L1_UP,      frags8
	/mnt/data3/macmanes/pero_genome/131219/peroL4_*U.fq,L1_UP,      frags9
	/mnt/data3/macmanes/pero_genome/131219/peroL5_*U.fq,L1_UP,      frags10
	/mnt/data3/macmanes/pero-mate-pair/peer3kb.clipped.*.fq,3kb,      jumps3
	/mnt/data3/macmanes/pero-mate-pair/peer7kb.clipped.*.fq,7kb,      jumps7
	

in_libs.csv
--

	library_name, project_name, organism_name,     type, paired, frag_size, frag_stddev, insert_size, insert_stddev, read_orientation, genomic_start, genomic_end
	L1,peer_genome,peer, fragment,1,300,50,            ,              ,           inward,0,0
	L1,peer_genome,peer, fragment,1,300,50,            ,              ,           inward,0,0
	L1,peer_genome,peer, fragment,1,300,50,            ,              ,           inward,0,0
	L1,peer_genome,peer, fragment,1,300,50,            ,              ,           inward,0,0
	L1,peer_genome,peer, fragment,1,300,50,            ,              ,           inward,0,0
	L1_UP,peer_genome,peer, fragment,0,300,50,            ,              ,           inward,0,0
	L1_UP,peer_genome,peer, fragment,0,300,50,            ,              ,           inward,0,0
	L1_UP,peer_genome,peer, fragment,0,300,50,            ,              ,           inward,0,0
	L1_UP,peer_genome,peer, fragment,0,300,50,            ,              ,           inward,0,0
	L1_UP,peer_genome,peer, fragment,0,300,50,            ,              ,           inward,0,0
	3kb,peer_genome,peer,  jumping,1,          ,            ,3000,500,          outward,0,0
	7kb,peer_genome,peer,  jumping,1,          ,            ,7000,500,          outward,0,0
	


RunAllPaths
--
	nohup RunAllPathsLG THREADS=32 FIX_ASSEMBLY_BASE_ERRORS=TRUE \
 	PRE=$RAID/macmanes/allpaths/ \
 	DATA_SUBDIR=mydata \
 	RUN=peer1 \
 	REFERENCE_NAME=peer \
 	TARGETS=standard \
 	CONNECT_SCAFFOLDS=TRUE HAPLOIDIFY=TRUE &
 	
8 May
--

Run failed during the PathReads step after ~90 hours - ran out of memory. I was running a big-ish trinity assembly concurrantly.

	nohup RunAllPathsLG THREADS=32 FIX_ASSEMBLY_BASE_ERRORS=TRUE \
 	PRE=$RAID/macmanes/allpaths/ \
 	DATA_SUBDIR=mydata \
 	RUN=peer1 \
 	REFERENCE_NAME=peer \
 	TARGETS=standard \
 	CONNECT_SCAFFOLDS=TRUE HAPLOIDIFY=TRUE OVERWRITE=TRUE&


