MaSuRCA
--


in `/mouse/masurca`

    DATA
    PE= aa 550 50 /mnt/data3/macmanes/pero_genome/raw_reasd/Pero360_550bp.P20_1P.gz /mnt/data3/macmanes/pero_genome/raw_reasd/Pero360_550bp.P20_2P.gz
	PE= ab 300 40 /mnt/data3/macmanes/pero_genome/raw_reasd/Pero360_300bp.P20_1P.gz /mnt/data3/macmanes/pero_genome/raw_reasd/Pero360_300bp.P20_2P.gz
	JUMP= aa 5000 400 /mnt/data3/macmanes/pero_genome/raw_reasd/peer5kb.clipped.1.fq /mnt/data3/macmanes/pero_genome/raw_reasd/peer5kb.clipped.2.fq  
	JUMP= ab 7000 600 /mnt/data3/macmanes/pero_genome/raw_reasd/peer8kb.clipped.1.fq /mnt/data3/macmanes/pero_genome/raw_reasd/peer8kb.clipped.2.fq
	JUMP= ac 6000 600 /mnt/data3/macmanes/pero_genome/raw_reasd/peer7kb.clipped.1.fq /mnt/data3/macmanes/pero_genome/raw_reasd/peer7kb.clipped.2.fq
	JUMP= ad 3500 300 /mnt/data3/macmanes/pero_genome/raw_reasd/peer3kb.clipped.1.fq /mnt/data3/macmanes/pero_genome/raw_reasd/peer3kb.clipped.2.fq
    OTHER=/mnt/data3/macmanes/pacbio/temppacbio/pacbio.frg
    END
    
    PARAMETERS
    GRAPH_KMER_SIZE = auto
    USE_LINKING_MATES = 1
    LIMIT_JUMP_COVERAGE = 300
    CA_PARAMETERS = cgwErrorRate=0.15 ovlMemory=4GB
    KMER_COUNT_THRESHOLD = 1    
    NUM_THREADS = 50
    JF_SIZE = 16244928491
    DO_HOMOPOLYMER_TRIM = 0
    END

to run

	./assemble.sh

_started assembly 3/20/15 at 0619._


killed

_started assembly 4/16/15 at 0929._

in `/mouse/masurca`

    DATA
    PE= aa 550 50 /mnt/data3/macmanes/pero_genome/raw_reasd/Pero360_550bp.P20_1P.fq.gz /mnt/data3/macmanes/pero_genome/raw_reasd/Pero360_550bp.P20_2P.fq.gz
    PE= ab 300 40 /mnt/data3/macmanes/pero_genome/raw_reasd/Pero360_300bp.P20_1P.fq.gz /mnt/data3/macmanes/pero_genome/raw_reasd/Pero360_300bp.P20_2P.fq.gz
    JUMP= ae 5000 400 /mnt/data3/macmanes/pero_genome/raw_reasd/peer5kb.clipped.1.fq /mnt/data3/macmanes/pero_genome/raw_reasd/peer5kb.clipped.2.fq
    JUMP= af 7000 600 /mnt/data3/macmanes/pero_genome/raw_reasd/peer8kb.clipped.1.fq /mnt/data3/macmanes/pero_genome/raw_reasd/peer8kb.clipped.2.fq
    JUMP= ac 6000 600 /mnt/data3/macmanes/pero_genome/raw_reasd/peer7kb.clipped.1.fq /mnt/data3/macmanes/pero_genome/raw_reasd/peer7kb.clipped.2.fq
    JUMP= ad 3500 300 /mnt/data3/macmanes/pero_genome/raw_reasd/peer3kb.clipped.1.fq /mnt/data3/macmanes/pero_genome/raw_reasd/peer3kb.clipped.2.fq
    OTHER=pacbio.frg
    END
    
    PARAMETERS
    GRAPH_KMER_SIZE = auto
    USE_LINKING_MATES = 1
    LIMIT_JUMP_COVERAGE = 300
    CA_PARAMETERS = cgwErrorRate=0.15 ovlMemory=8GB doFragmentCorrection=0
    KMER_COUNT_THRESHOLD = 2
    NUM_THREADS = 50
    JF_SIZE = 16244928491
    DO_HOMOPOLYMER_TRIM = 0
    END
    
