runCA

```
runCA \
-s Peer_v3.config \
-p Peer \
-d Peer_v3 pero.pacbio.frg superReadSequences_shr.frg | tee Peer_v3.out
```

Peer_v3

```
cnsErrorRate = 0.25
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
ovlThreads = 5
ovlRefBlockSize = 1000000
ovlCorrBatchSize = 100000
ovlStoreMemory = 219362
mbtConcurrency = 2
frgCorrThreads = 20
frgCorrConcurrency = 5
cnsConcurrency = 45
batThreads = 40
batMemory = 250
utgGraphErrorRate = 0.05
utgMergeErrorRate = 0.05
frgMinLen = 200
```
