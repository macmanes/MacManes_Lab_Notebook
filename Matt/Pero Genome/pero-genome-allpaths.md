 	
 	
 	
 	nohup PrepareAllPathsInputs.pl \
 	DATA_DIR=$RAID/allpaths/peer/mydata/ \
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
 	PRE=$RAID/allpaths/ \
 	DATA_SUBDIR=mydata \
 	RUN=peer1 \
 	REFERENCE_NAME=peer \
 	TARGETS=standard \
 	CONNECT_SCAFFOLDS=TRUE HAPLOIDIFY=TRUE &
 	
8 May
--

Run failed during the PathReads step after ~90 hours - ran out of memory. I was running a big-ish trinity assembly concurrantly.

	nohup RunAllPathsLG THREADS=32 FIX_ASSEMBLY_BASE_ERRORS=TRUE \
 	PRE=$RAID/allpaths/ \
 	DATA_SUBDIR=mydata \
 	RUN=peer1 \
 	REFERENCE_NAME=peer \
 	TARGETS=standard \
 	CONNECT_SCAFFOLDS=TRUE HAPLOIDIFY=TRUE OVERWRITE=TRUE &

3 June 14
--

Run Failed during Close Unipath 

	nohup RunAllPathsLG THREADS=32 FIX_ASSEMBLY_BASE_ERRORS=TRUE \
	PRE=$RAID/allpaths/ DATA_SUBDIR=mydata RUN=peer \
	REFERENCE_NAME=peer TARGETS=standard CONNECT_SCAFFOLDS=TRUE \
	HAPLOIDIFY=TRUE OVERWRITE=True &




--------------------------------------------------------------------------------
Mon Jun 02 20:15:08 2014 run on davinci, pid=44862 [May  3 2014 21:06:50 R49775 ]
CloseUnipathGaps NUM_THREADS=32                                                \
                 DIR=/mnt/data3/macmanes/allpaths/peer/mydata/peer             \
                 IN_HEAD=frag_reads_corr_cpd                                   \
                 UNIBASES=filled_reads.unibases.k96 UNIBASES_K=96              \
                 USE_LINKS=False OUT_HEAD=filled_reads.gap_closed WORKDIR=tmp  \
                 MM=True _MM_INTERVAL=10 _MM_SUMMARY=False                     \
                 _MM_OUT=/mnt/data3/macmanes/allpaths/peer/mydata/peer/makeinf \
                 o/filled_reads.gap_closed.CloseUnipathGaps.log.mm.CloseUnipat \
                 hGaps
--------------------------------------------------------------------------------


Redirecting standard output to the following files:
/mnt/data3/macmanes/allpaths/peer/mydata/peer/makeinfo/filled_reads.gap_closed.CloseUnipathGaps.log.out.CloseUnipathGaps
/mnt/data3/macmanes/allpaths/peer/make_log/mydata/peer/test/2014-05-31T09:20:31/CloseUnipathGaps.out

logging to /mnt/data3/macmanes/allpaths/peer/mydata/peer/filled_reads.gap_closed.CloseUnipathGaps.log
Mon Jun 02 20:15:08 2014: Loading input files...

Mon Jun 02 20:33:27 2014: Finding seeds for unipath gaps
Mon Jun 02 20:33:27 2014: Creating KmerParcel files for FindUnipathGapSeeds
Mon Jun 02 20:33:27 2014: n_reads = 744366469
Mon Jun 02 21:19:28 2014: Creating seeds...
Mon Jun 02 21:19:28 2014: compute seeds[query_ID].size() for each query_ID.
Mon Jun 02 21:24:45 2014: reserve space for seeds[query_ID].
Mon Jun 02 21:25:17 2014: store seeds in seeds[query_ID].
Mon Jun 02 21:30:11 2014: 744366469 number of reads processed.
Mon Jun 02 21:30:11 2014: 870235112 seeds created.
Mon Jun 02 21:40:57 2014: Creating KmerParcel files for FindUnipathGapSeeds
Mon Jun 02 21:40:57 2014: n_reads = 744366469
Mon Jun 02 22:16:10 2014: Creating seeds...
Mon Jun 02 22:16:10 2014: compute seeds[query_ID].size() for each query_ID.
Mon Jun 02 22:18:24 2014: reserve space for seeds[query_ID].
Mon Jun 02 22:18:57 2014: store seeds in seeds[query_ID].
Mon Jun 02 22:23:24 2014: 744366469 number of reads processed.
Mon Jun 02 22:23:24 2014: 848079426 seeds created.
Mon Jun 02 22:35:10 2014: Loading read quality scores so we can build extenders
Mon Jun 02 22:41:36 2014: Building those extenders

Tue Jun 03 15:40:53 2014.  Child process 44865 was killed with signal 9. Stopping.

Generating a backtrace...
Killed
make: *** [/mnt/data3/macmanes/allpaths/peer/mydata/peer/filled_reads.gap_closed.CloseUnipathGaps.log] Error 137
make: *** Deleting file `/mnt/data3/macmanes/allpaths/peer/mydata/peer/filled_reads.gap_closed.CloseUnipathGaps.log'

Tue Jun 03 15:41:02 2014 : make process finished.

Tue Jun 03 15:41:02 2014: Computing runtime statistics.

 e_time(sec)  u_time(sec)  vmrss(MB)  vmsize(MB)   module name
--------------------------------------------------------------------------------
         172          123      21075       21109   ValidateAllPathsInputs
        5995         1461     189945      191084   RemoveDodgyReads
       73893      1856870     284970      315464   FindErrors
       27303       527730     272089      325817   CleanCorrectedReads
       43270       836364     286061      300896   PathReads
        7598       206222     250122      258697   FillFragments
       43565       620914     194746      247269   CommonPather
        1273          965      69714       88086   MakeRcDb
        8996         8286     145553      148669   Unipather
       69954      1366490     218628      236060   CloseUnipathGaps
--------------------------------------------------------------------------------
      282024      5425426     286061      325817   Total/Peak 10 modules

Tue Jun 03 15:41:03 2014: Compiling assembly report.

------------------ FindErrors -> frag_reads_edit.fastb

      775320414    total number of original fragment reads
          150.9    mean length of original fragment reads in bases
           40.7    % gc content of fragment reads
            0.1    % of bases pre-corrected
     2608258109    estimated genome size in bases
           33.0    % genome estimated to be repetitive (at K=25 scale)
             37    estimated genome coverage by fragment reads
           0.28    estimated standard deviation of sequencing bias (at K=25 scale)
           81.0    % of bases confirmed in cycle 0
           0.66    % of bases corrected in cycle 0
           0.05    % of bases with conflicting corrections in cycle 0
           81.8    % of bases confirmed in cycle 1
           0.27    % of bases corrected in cycle 1
           0.04    % of bases with conflicting corrections in cycle 1

------------------ CleanCorrectedReads -> frag_reads_corr.25mer.kspec

            4.0    % of reads removed because of low frequency kmers

------------------ FillFragments -> filled_reads.fastb

          100.2    % of fragment pairs that were filled

------------------ Memory and CPU usage

             64    available cpus
          503.9    GB of total available memory
         9763.0    GB of available disk space
          78.29    hours of total elapsed time
          78.34    hours of total per-module elapsed time
        1507.06    hours of total per-module user time
          19.24    effective parallelization factor
         279.36    GB memory usage peak



Tue Jun 03 15:41:05 2014 : ALLPATHS-LG Pipeline Finished.

Run directory: /mnt/data3/macmanes/allpaths/peer/mydata/peer
Log directory: /mnt/data3/macmanes/allpaths/peer/make_log/mydata/peer/test/2014-05-31T09:20:31

 *** Make encountered an error, see above for error messages. ***

will try `CLOSE_UNIPATH_GAPS=False` if this fails again.

