this is running wgs 8.3 after MaSuRCA generated 'super-reads'

had to change `ulimit -n 8000` because of a crash in meryl

Started 5/4 in the PM in `/mouse/masurca`

	runCA \
	-s CA_4May14.txt \
	-p peer_genome \
	-d CA_4May14 1> runCA_4May15a.out 2>&1


spec file

    gkpFixInsertSizes=0
    cgwErrorRate=0.15
    ovlHashBits=25
    ovlHashBlockLength=180000000
    ovlCorrConcurrency=50
    ovlConcurrency=50
    ovlThreads=1
    ovlRefBlockSize=46896261
    ovlCorrBatchSize=4689626
    doFragmentCorrection=1
    utgErrorRate=0.03
    merylMemory=8192
    bogBreakAtIntersections=0
    unitigger=bogart
    bogBadMateDepth=1000000
    merylThreads=50
    mbtConcurrency=10
    frgCorrThreads=1
    frgCorrConcurrency=50
    cnsConcurrency=13
    doOverlapBasedTrimming=1
    doExtendClearRanges=1
    ovlMerSize=22
    
    /mouse/masurca/superReadSequences_shr.frg
    /mouse/masurca/pacbio.frg
    /mouse/masurca/ac.cor.clean.frg
    /mouse/masurca/ad.cor.clean.frg
    /mouse/masurca/ae.cor.clean.frg
    /mouse/masurca/af.cor.clean.frg