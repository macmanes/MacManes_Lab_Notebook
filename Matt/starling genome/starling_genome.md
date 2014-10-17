Starling Genome
--

In `/mnt/data3/macmanes/starling/` is the pacbio and Illumina data

I used Nextclip version 1.3 for the mp data (see `/mnt/data3/macmanes/starling/illumina/Starling_nextclip.ipynb`)

    nextclip -i Liver-0151585355-4-5kb-MatePair_CGATGT_AC41ALANXX_L004_001.R1.fastq \
    -j Liver-0151585355-4-5kb-MatePair_CGATGT_AC41ALANXX_L004_001.R2.fastq \
    -o starling5kb -e -n 50000000

I cancatenated the A B C files from 5kb MP and 10kb MP into left and right files: `/mnt/data3/macmanes/starling/illumina/mate_pair/starling10kb_1.fq.gz` for instance

The D files I think I can use as single end files - will place them in `/mnt/data3/macmanes/starling/illumina/single_end`

In `/mnt/data3/macmanes/starling/illumina/paired_end` I am correcting the Liver500 and Lib300 libs using bless version 0.17

I started bless on Friday 8/29
--

    bless -read1 Liver_500bp_1.fq -read2 Liver_500bp_2.fq -prefix Liver500_corr -kmerlength 25 -verify -notrim -load Liver500_corr.bf.data
    bless -read1 Liver_300bp_1.fq -read2 Liver_300bp_2.fq -prefix Liver300_corr -kmerlength 25 -verify -notrim -load Liver300_corr.bf.data
    
This finished on Wednesday.

300bp lib:

    Correcting errors in reads
     Number of corrected errors: 142,384,872
     Number of trimmed bases   : 233,602,369
     Number of corrected reads : 57,735,419
     Correcting errors in reads: done
     
500bp lib

    Correcting errors in reads
     Number of corrected errors: 62,312,642
     Number of trimmed bases   : 83,216,983
     Number of corrected reads : 24,684,081
     Correcting errors in reads: done

     
Trimmomatic
--

    java -Xmx50g -jar /share/trinityrnaseq_r20140717/trinity-plugins/Trimmomatic-0.32/trimmomatic-0.32.jar PE \
    -threads 48 -baseout Liver500.corr.trim.fq.gz \
    Liver500_corr.1.corrected.fastq.gz \
    Liver500_corr.2.corrected.fastq.gz  \
    ILLUMINACLIP:/share/trinityrnaseq_r20140717/trinity-plugins/Trimmomatic/adapters/TruSeq3-PE.fa:2:40:15 \
    LEADING:2 TRAILING:2 SLIDINGWINDOW:4:2 MINLEN:25


Input Read Pairs: 176216527 Both Surviving: 176080427 (99.92%) Forward Only Surviving: 122356 (0.07%) Reverse Only Surviving: 2081 (0.00%) Dropped: 11663 (0.01%)

and

    java -Xmx50g -jar /share/trinityrnaseq_r20140717/trinity-plugins/Trimmomatic-0.32/trimmomatic-0.32.jar PE \
    -threads 48 -baseout Liver300.corr.trim.fq.gz \
    Liver300_corr.1.corrected.fastq.gz \
    Liver300_corr.2.corrected.fastq.gz  \
    ILLUMINACLIP:/share/trinityrnaseq_r20140717/trinity-plugins/Trimmomatic/adapters/TruSeq3-PE.fa:2:40:15 \
    LEADING:2 TRAILING:2 SLIDINGWINDOW:4:2 MINLEN:25


Input Read Pairs: 243753879 Both Surviving: 242129622 (99.33%) Forward Only Surviving: 1609832 (0.66%) Reverse Only Surviving: 966 (0.00%) Dropped: 13459 (0.01%)

I'm going to gzip the resultant error corrected files together, then error correct the pacbio data
--

Started 9/4/14 at 0615

    lordec-correct -threads 48 /mnt/data3/macmanes/starling/illumina/paired_end/illumina.for.lordec.fq.gz 21 2 \
    /mnt/data3/macmanes/starling/pacbio/pacbio_fastq/pacbio.starling.fq.gz \
    /mnt/data3/macmanes/starling/pacbio/pacbio_fastq_corr/pacbio.corr.starling.fq.gz 
    
1st run failed after 1 hour with 

    kmer_len: 21 solid_kmer_thr: 3
    max_trials: 5 max_error_rate: 0.4 max_branch: 200
    Cannot access the graph file for reference reads: /mnt/data3/macmanes/starling/illumina/paired_end/illumina.for.lordec.fq.gz.h5
    bRefGraph: 0
    bRefSeq: 1
    creating the graph from file: /mnt/data3/macmanes/starling/illumina/paired_end/illumina.for.lordec.fq.gz
    [Bank: fasta to binary                  ]  105    %     elapsed:     40 min 52    sec      estimated remaining:      0 min 0     sec
    [DSK: Pass 2/434, Step 1: partitioning    ]  0.224  %     elapsed:      1 min 41    sec      estimated remaining:    749 min 41    sec
    
    terminate called after throwing an instance of 'gatb::core::system::Exception'
    
Looks like lordec is going to run - corrected 5.1G of sequence, failed because a read was too long - reset parameter in lordec-corect.cpp to 70000.

ABySS k81
--
I will run abyss now:

    #Break up PE reads into a bunch of files to speed up load time.
    time /usr/bin/mpirun -np 44 ABYSS-P -k81 -q3 \
    --coverage-hist=coverage.hist -s starling81-bubbles.fa \
    -o starling81-1.fa /mnt/data3/macmanes/starling/illumina/paired_end/*fastq
    
Then full run.
    
    time abyss-pe np=32 k=81 name=starling81 lib='pe1 pe2' mp='mp1 mp2' long=long1 v=-v \
    pe1='/mnt/data3/macmanes/starling/illumina/paired_end/Liver300.corr.trim_1P.fq.gz /mnt/data3/macmanes/starling/illumina/paired_end/Liver300.corr.trim_2P.fq.gz' \
    pe2='/mnt/data3/macmanes/starling/illumina/paired_end/Liver500.corr.trim_1P.fq.gz /mnt/data3/macmanes/starling/illumina/paired_end/Liver500.corr.trim_2P.fq.gz' \
    mp1='/mnt/data3/macmanes/starling/illumina/mate_pair/starling5kb_1.fq.gz /mnt/data3/macmanes/starling/illumina/mate_pair/starling5kb_2.fq.gz' \
    mp2='/mnt/data3/macmanes/starling/illumina/mate_pair/starling10kb_1.fq.gz /mnt/data3/macmanes/starling/illumina/mate_pair/starling10kb_2.fq.gz' \
    long1='/mnt/data3/macmanes/starling/pacbio/pacbio_fastq_corr/pacbio.corr.starling.fasta'

took ~16 hours. 

    n       n:500   n:N50   min     N80     N50     N20     E-size  max     sum     name
    1291317 127214  14762   500     7193    19196   41048   25968   194214  1.021e9 starling81-unitigs.fa
    981489  71647   4680    500     20042   64622   155991  99088   746519  1.188e9 starling81-contigs.fa
    966358  57078   2642    500     32115   112226  280728  175273  1474592 1.187e9 starling81-scaffolds.fa
    956888  52265   2602    500     34584   115908  281370  177510  1474592 1.187e9 starling81-long-scaffs.fa

with trimmed PacBio reads, N50 increases by 1kb, but in general the assembly was VERY similar. 

ABySS k91
--

    time /usr/bin/mpirun -np 36 ABYSS-P -k91 -q3 --no-chastity \
    --coverage-hist=coverage.hist -s starling91-bubbles.fa \
    -o starling91-1.fa /mnt/data3/macmanes/starling/illumina/paired_end/*fastq
    
Then full run.
    
    time abyss-pe np=32 k=91 name=starling91 lib='pe1 pe2' mp='mp1 mp2' long=long1 v=-v n=5 \
    pe1='/mnt/data3/macmanes/starling/illumina/paired_end/Liver300.corr.trim_1P.fq.gz /mnt/data3/macmanes/starling/illumina/paired_end/Liver300.corr.trim_2P.fq.gz' \
    pe2='/mnt/data3/macmanes/starling/illumina/paired_end/Liver500.corr.trim_1P.fq.gz /mnt/data3/macmanes/starling/illumina/paired_end/Liver500.corr.trim_2P.fq.gz' \
    mp1='/mnt/data3/macmanes/starling/illumina/mate_pair/starling5kb_1.fq.gz /mnt/data3/macmanes/starling/illumina/mate_pair/starling5kb_2.fq.gz' \
    mp2='/mnt/data3/macmanes/starling/illumina/mate_pair/starling10kb_1.fq.gz /mnt/data3/macmanes/starling/illumina/mate_pair/starling10kb_2.fq.gz' \
    long1='/mnt/data3/macmanes/starling/pacbio/pacbio_fastq_corr/pacbio.corr.starling.fa'
    
    
    n       n:200   n:N50   min     N80     N50     N20     E-size  max     sum     name
    1168062 287094  15935   200     6050    18254   40333   25045   195175  1.071e9 starling91-3.fa
    
    

SPADES
--

    spades.py -t 30 -m 500  --careful \
    --pe1-1 /mnt/data3/macmanes/starling/illumina/paired_end/Liver300.corr.trim_1P.fq.gz \
    --pe1-2 /mnt/data3/macmanes/starling/illumina/paired_end/Liver300.corr.trim_2P.fq.gz \
    --pe2-1 /mnt/data3/macmanes/starling/illumina/paired_end/Liver500.corr.trim_1P.fq.gz \
    --pe2-2 /mnt/data3/macmanes/starling/illumina/paired_end/Liver500.corr.trim_2P.fq.gz \
    --mp1-1 /mnt/data3/macmanes/starling/illumina/mate_pair/starling5kb_1.fq.gz \
    --mp1-2 /mnt/data3/macmanes/starling/illumina/mate_pair/starling5kb_2.fq.gz  \
    --mp2-1 /mnt/data3/macmanes/starling/illumina/mate_pair/starling10kb_1.fq.gz \
    --mp2-2 /mnt/data3/macmanes/starling/illumina/mate_pair/starling10kb_2.fq.gz \
     --pacbio /mnt/data3/macmanes/starling/pacbio/pacbio_fastq/pacbio.starling.fq.gz \
    -o spades_output
    
   
AllPaths
--

    PrepareAllPathsInputs.pl \
    DATA_DIR=/mouse/starling/assembly/allpaths/assembo \
    GENOME_SIZE=1100000000 OVERWRITE=True PLOIDY=2 \
    FRAG_COVERAGE=50 HOSTS=40 \
    TMP_DIR=/mouse \
    JAVA_MEM_GB=100
    

run

    RunAllPathsLG THREADS=40 FIX_ASSEMBLY_BASE_ERRORS=TRUE \
    PRE=/mouse/starling/assembly/allpaths/ \
    DATA_SUBDIR=assembo \
    RUN=starling \
    REFERENCE_NAME=st \
    TARGETS=standard \
    CONNECT_SCAFFOLDS=TRUE HAPLOIDIFY=TRUE

------------------ LibCoverage -> library_coverage.report

LibCoverage table:

LEGEND
   n_reads:  number of reads in input
   %_used:   % of reads assembled
   scov:     sequence coverage
   n_pairs:  number of valid pairs assembled
   pcov:     physical coverage

type  lib_name           lib_stats      n_reads  %_used  scov      n_pairs   pcov

frag  L300              -73 +/- 50  484,259,244    91.3  54.0  222,684,467   39.4
frag  L500              140 +/- 50  352,160,854    92.7  39.9  159,290,960   68.0
frag  === total ===                 836,420,098    91.9  93.9  381,975,427  107.5

jump  10kb           4300 +/- 2129  133,255,004     7.7   0.8    3,470,620   17.4
jump  5kb             3254 +/- 842  161,984,044    55.7   7.2   38,306,547  141.9
jump  === total ===                 295,239,048    34.1   8.0   41,777,167  159.4


------------------ Memory and CPU usage

             64    available cpus
          503.9    GB of total available memory
         2811.8    GB of available disk space
         111.41    hours of total elapsed time
         111.43    hours of total per-module elapsed time
        2139.63    hours of total per-module user time
          19.20    effective parallelization factor
         310.46    GB memory usage peak
         

------------------ AllPathsReport -> assembly_stats.report

           1000    contig minimum size for reporting
          27683    number of contigs
           25.9    number of contigs per Mb
           2869    number of scaffolds
     1022452874    total contig length
     1066841368    total scaffold length, with gaps
          123.7    N50 contig size in kb
           4625    N50 scaffold size in kb
           4390    N50 scaffold size in kb, with gaps
           2.69    number of scaffolds per Mb
            365    median size of gaps in scaffolds
            161    median dev of gaps in scaffolds
           4.16    % of bases in captured gaps
           0.04    % of bases in negative gaps (after 5 devs)
          32.03    %% of ambiguous bases
          12.00    ambiguities per 10,000 bases
          
          
----------Thu Oct 02 07:52:55 2014: Computing runtime statistics.

    e_time(sec)  u_time(sec)  vmrss(MB)  vmsize(MB)   module name
          87           62      22628       22769   ValidateAllPathsInputs
        9161         1642     174384      180333   RemoveDodgyReads
       47151      2046150     285133      312972   FindErrors
       19698       463740     240431      280031   CleanCorrectedReads
       21119       920438     105715      115877   PathReads
        4289       209053      88342       98725   FillFragments
       38592       290866     197661      256498   CommonPather
         611          471      24718       32888   MakeRcDb
        1153          808      59977       60051   Unipather    
        12418       152001     216391      233910   CloseUnipathGaps                                                                                                                                        
        6672        62366     109855      150412   ShaveUnipathGraph
          71            2       6785        6815   ReplacePairsStats
         873          560      47869       58301   RemoveDodgyReads
         270          243      15624       20724   SamplePairedReadStats
       16424        60143     317908      341726   UnipathPatcher
       37665       318937     239208      333199   CommonPather
          13           10        532         563   MakeRcDb
         118           99       2888        3004   Unipather
        1244          734      27745       30972   FilterPrunedReads
         733          675      33525       34857   CreateLookupTab
        2100        83550      36865       47152   ErrorCorrectJump
          99           66       2529        2613   SplitUnibases
         230          139       3042        6182   MergeReadSets
         734          558      25866       32757   MakeRcDb
       13580       145487     165913      224584   UnibaseCopyNumber3
        1083         8169      45676       64033   UnipathLocsLG
         179          274       7355       16239   SamplePairedReadDistributions
        1027          870      51636       51670   BuildUnipathLinkGraphsLG
         576         1446      57229       66880   SelectSeeds
       42671      1042450     125030      133482   LocalizeReadsLG
        5326        51601      89547      126331   MergeNeighborhoods1
        1071        23285      10179       28425   MergeNeighborhoods2
         681          667      21702       33421   MergeNeighborhoods3
        2628        19521      54476       85980   RecoverUnipaths
         627          612       4857        4889   FlattenHKP
         326         2955     134138      143709   AlignPairsToFasta
        3567        32438      91771      138136   RemoveHighCNAligns
        1499         3655      52729       62318   MakeScaffoldsLG
        3344         8528      47891       60308   CleanAssembly
        2582       102194      75612       85180   RemodelGaps
        6007         3636     129089      138667   PostPatcher
        1214         1174       8463        8555   ApplyGapPatches
        5943       176922     139044      168992   AlignReads
         916          877       3077        3134   ConnectScaffolds
        6462       175984     139284      168936   AlignReads
        1493         1366      17548       23294   TagCircularScaffolds
         449         2810     126950      139960   FixPrecompute
        5382       107270     145217      319022   FixAssemblyBaseErrors
        2849        86765     115473      122534   FixSomeIndels
         284          243       7745        8038   ApplyAssemblyEdits
        6037       175477     139155      168868   AlignReads
       29986       876163     266272      554363   FixLocal
        4288         8699     103535      113665   KPatch
       26900        26767       9589        9664   RebuildAssemblyFiles
          35           32       1052        1101   AllPathsReport
         580         1004      15495       24154   LibCoverage
--------------------------------------------------------------------------------
      401137      7702675     317908      554363   Total/Peak 56 modules   
    
-----library Stats

    LEGEND
   n_reads:  number of reads in input
   %_used:   % of reads assembled
   scov:     sequence coverage
   n_pairs:  number of valid pairs assembled
   pcov:     physical coverage

    type  lib_name           lib_stats      n_reads  %_used  scov      n_pairs   pcov

    frag  L300              -73 +/- 50  484,259,244    91.3  54.0  222,684,467   39.4
    frag  L500              140 +/- 50  352,160,854    92.7  39.9  159,290,960   68.0
    frag  === total ===                 836,420,098    91.9  93.9  381,975,427  107.5

    jump  10kb           4300 +/- 2129  133,255,004     7.7   0.8    3,470,620   17.4
    jump  5kb             3254 +/- 842  161,984,044    55.7   7.2   38,306,547  141.9
    jump  === total ===                 295,239,048    34.1   8.0   41,777,167  159.4    
    
    
PBJelly
---

in `/mouse/starling/assembly/pbjelly`

    Jelly.py setup Protocol.xml
    Jelly.py mapping Protocol.xml
    Jelly.py support Protocol.xml
    Jelly.py extraction Protocol.xml
    Jelly.py assembly Protocol.xml -x "-n 30"
    

CEGMA
--

    WARNING executed HMMER version has not been tested !!!

    #      Statistics of the completeness of the genome based on 248 CEGs      #

              #Prots  %Completeness  -  #Total  Average  %Ortho

      Complete      202       81.45      -   233     1.15     12.38

      Group 1       51       77.27      -    56     1.10      7.84
      Group 2       51       91.07      -    56     1.10      9.80
    Group 3       47       77.05      -    56     1.19     17.02
       Group 4       53       81.54      -    65     1.23     15.09

    Partial      221       89.11      -   279     1.26     20.81

    Group 1       56       84.85      -    67     1.20     17.86
       Group 2       54       96.43      -    66     1.22     18.52
       Group 3       55       90.16      -    70     1.27     21.82
       Group 4       56       86.15      -    76     1.36     25.00


    
    
    
    