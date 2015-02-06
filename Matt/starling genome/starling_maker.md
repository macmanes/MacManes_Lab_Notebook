INSTALL Maker


/usr/lib/openmpi/include/mpi.h
/usr/bin/mpicc

2.31.8

Ran CEGMA on AWS, downloaded results to `/mouse/Starling/cegma`

	cegma2zff output.cegma.gff ../genome/Starling_MacManes_AllPathsLG.fasta
	fathom genome.ann genome.dna -categorize 1000
	fathom -export 1000 -plus uni.ann uni.dna  
	forge export.ann export.dna  
	hmm-assembler.pl jelly.out.fasta . > cegmasnap.hmm
	
Barrnap 0.4.2

	barrnap --kingdom euk --threads 10 ../genome/Starling_MacManes_AllPathsLG.fasta
	
maker

	mpirun -np 40 maker -fix_nucleotides
	
    #-----Genome (these are always required)
    genome=/mouse/starling/genome/Starling_MacManes_AllPathsLG.fasta
    organism_type=eukaryotic
    
    #-----Re-annotation Using MAKER Derived GFF3
    maker_gff= #MAKER derived GFF3 file
    est_pass=1 #use ESTs in maker_gff: 1 = yes, 0 = no
    altest_pass=0 #use alternate organism ESTs in maker_gff: 1 = yes, 0 = no
    protein_pass=1 #use protein alignments in maker_gff: 1 = yes, 0 = no
    rm_pass=0 #use repeats in maker_gff: 1 = yes, 0 = no
    model_pass=0 #use gene models in maker_gff: 1 = yes, 0 = no
    pred_pass=0 #use ab-initio predictions in maker_gff: 1 = yes, 0 = no
    other_pass=1 #passthrough anyything else in maker_gff: 1 = yes, 0 = no
    
    #-----EST Evidence (for best results provide a file for at least one)
    est=/mouse/starling/TransDecoder/starling.est #set of ESTs or assembled mRNA-seq in fasta format
    
    #-----Protein Homology Evidence (for best results provide a file for at least one)
    protein=/mouse/starling/other_prot/bird.prot  #protein sequence file in fasta format (i.e. from mutiple oransisms)
    
    #-----Repeat Masking (leave values blank to skip repeat masking)
    model_org=all #select a model organism for RepBase masking in RepeatMasker
    repeat_protein= #provide a fasta file of transposable element proteins for RepeatRunner
    rm_gff= #pre-identified repeat elements from an external GFF3 file
    prok_rm=0 #forces MAKER to repeatmask prokaryotes (no reason to change this), 1 = yes, 0 = no
    softmask=1 #use soft-masking rather than hard-masking in BLAST (i.e. seg and dust filtering)
    
    #-----Gene Prediction
    snaphmm=/mouse/starling/cegma/cegmasnap.hmm
    gmhmm= #GeneMark HMM file
    augustus_species= #Augustus gene prediction species model
    fgenesh_par_file= #FGENESH parameter file
    pred_gff= #ab-initio predictions from an external GFF3 file
    model_gff= #annotated gene models from an external GFF3 file (annotation pass-through)
    est2genome=0 #infer gene predictions directly from ESTs, 1 = yes, 0 = no
    protein2genome=0 #infer predictions from protein homology, 1 = yes, 0 = no
    trna=1 #find tRNAs with tRNAscan, 1 = yes, 0 = no
    snoscan_rrna= #rRNA file to have Snoscan find snoRNAs
    unmask=0 #also run ab-initio prediction programs on unmasked sequence, 1 = yes, 0 = no
    
    #-----Other Annotation Feature Types (features MAKER doesn't recognize)
    other_gff=/mouse/starling/barrnap/barrnap.gff
    
    #-----External Application Behavior Options
    alt_peptide=C #amino acid used to replace non-standard amino acids in BLAST databases
    cpus=1 #max number of cpus to use in BLAST and RepeatMasker (not for MPI, leave 1 when using MPI)
    
    #-----MAKER Behavior Options
    max_dna_len=700000 #length for dividing up contigs into chunks (increases/decreases memory usage)
    min_contig=10000 #skip genome contigs below this length (under 10kb are often useless)
    
    pred_flank=200 #flank for extending evidence clusters sent to gene predictors
    pred_stats=0 #report AED and QI statistics for all predictions as well as models
    AED_threshold=1 #Maximum Annotation Edit Distance allowed (bound by 0 and 1)
    min_protein=0 #require at least this many amino acids in predicted proteins
    alt_splice=0 #Take extra steps to try and find alternative splicing, 1 = yes, 0 = no
    always_complete=0 #extra steps to force start and stop codons, 1 = yes, 0 = no
    map_forward=0 #map names and attributes forward from old GFF3 genes, 1 = yes, 0 = no
    keep_preds=0 #Concordance threshold to add unsupported gene prediction (bound by 0 and 1)
    
    split_hit=50000 #length for the splitting of hits (expected max intron size for evidence alignments)
    single_exon=0 #consider single exon EST evidence when generating annotations, 1 = yes, 0 = no
    single_length=250 #min length required for single exon ESTs if 'single_exon is enabled'
    correct_est_fusion=0 #limits use of ESTs in annotation to avoid fusion genes
    
    tries=2 #number of times to try a contig if there is a failure for some reason
    clean_try=0 #remove all data from previous run before retrying, 1 = yes, 0 = no
    clean_up=0 #removes theVoid directory with individual analysis files, 1 = yes, 0 = no
    TMP=/home/macmanes/maker_tmp
    

make `maker_2` folder.

add maker gff file
--

	maker_gff=/mouse/starling/maker/Starling_MacManes_AllPathsLG.maker.output/starling.gff
	
retrain snap
--

    maker2zff /mouse/starling/maker/Starling_MacManes_AllPathsLG.maker.output/starling.gff
    fathom -categorize 1000 genome.ann genome.dna
    fathom -export 1000 -plus uni.ann uni.dna
    forge export.ann export.dna
    hmm-assembler.pl pyu . > maker2.hmm
    
use new snap hmm
--

train augustus

    /share/augustus-3.0.3/scripts/autoAug.pl \
    -g /mouse/starling/genome/Starling_MacManes_AllPathsLG.fasta \
    -t /mouse/starling/cegma/output.cegma.gff --species=starling \
    --cdna=/mouse/starling/TransDecoder/starling.simple.est -v  --singleCPU --useexisting



