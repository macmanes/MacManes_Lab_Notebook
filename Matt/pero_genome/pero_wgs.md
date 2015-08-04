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
    

new spec file
--

```
nsErrorRate = 0.25
gridEngineSyncOption = -sync y
merSize = 16
frgMinLen = 200
gridOptionsScript = -pe threads 1
shell = /bin/bash
cgwErrorRate = 0.25
doUnitigSplitting = 0
gridEngineTaskID = SGE_TASK_ID
utgGraphErrorLimit = 0
gridEngineArrayName = ARRAY_NAME
gridOptions =
gridEngineSubmitCommand = qsub
gridEngineHoldOption = -hold_jid "WAIT_TAG"
gridEngineOutputOption = -j y -o
useGrid = 0
gridOptionsOverlap = -pe threads 16 -l mem=2GB
doFragmentCorrection = 1
gridEngineArrayOption = -t ARRAY_JOBS
unitigger = bogart
ovlErrorRate = 0.25
doOverlapBasedTrimming = 0
utgErrorRate = 0.25
utgMergeErrorLimit = 0
gridEngineJobID = JOB_ID
cnsMinFrags = 1000
utgMergeErrorRate = 0.05
utgErrorLimit = 6.5
scriptOnGrid = 0
ovlHashBlockLength = 180000000
gridEngineArraySubmitID = $TASK_ID
gridEngineNameOption = -cwd -N
gridEnginePropagateCommand = qalter -hold_jid "WAIT_TAG"
ovlRefBlockSize = 1000000
batOptions = -RS -NS -CS
utgGraphErrorRate = 0.05
gridOptionsConsensus = -pe threads 16
gridEngineNameToJobIDCommand =
merSize = 16
merylThreads = 32
merylMemory = 32000
frgCorrBatchSize = 100000
ovlHashBlockLength = 180000000
ovlCorrConcurrency = 10
ovlConcurrency = 30
ovlHashBits = 25
ovlHashBlockLength = 180000000
ovlThreads = 1
ovlRefBlockSize = 1000000
ovlCorrBatchSize = 100000
ovlStoreMemory = 219362
mbtConcurrency = 2
frgCorrThreads = 20
frgCorrConcurrency = 1
cnsConcurrency = 45
batThreads = 40
batMemory = 250
utgGraphErrorRate = 0.05
utgMergeErrorRate = 0.05
frgMinLen = 200
```


```
/share/wgs-assembler/Linux-amd64/bin/runCA -s /mouse/Mya/pbcr//tempMya_v1/Mya_v1.spec \
-p Peer -d Peer_v1 useGrid=0 scriptOnGrid=0 unitigger=bogart \
ovlErrorRate=0.1 utgErrorRate=0.06 cgwErrorRate=0.1 cnsErrorRate=0.1 utgGraphErrorLimit=0 utgGraphErrorRate=0.05 \
utgMergeErrorLimit=0 utgMergeErrorRate=0.05 frgCorrBatchSize=100000 doOverlapBasedTrimming=1 obtErrorRate=0.08 obtErrorLimit=4.5 frgMinLen=500 \
ovlMinLen=100 "batOptions=-RS -NS -CS" consensus=pbutgcns merSize=22 cnsMaxCoverage=1 cnsReuseUnitigs=1 superReadSequences_shr.frg pero.pacbio.frg

```