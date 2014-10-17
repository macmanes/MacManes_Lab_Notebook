trimming
--

	ftp://ftp.sra.ebi.ac.uk/vol1/fastq/SRR536/SRR536828/SRR536828.fastq.gz
	ftp://ftp.sra.ebi.ac.uk/vol1/fastq/SRR536/SRR536829/SRR536829.fastq.gz
	wget ftp://ftp.sra.ebi.ac.uk/vol1/fastq/SRR575/SRR575841/SRR575841.fastq.gz
	wget ftp://ftp.sra.ebi.ac.uk/vol1/fastq/SRR656/SRR656612/SRR656612.fastq.gz
	wget ftp://ftp.sra.ebi.ac.uk/vol1/fastq/SRR776/SRR776537/SRR776537.fastq.gz
	wget ftp://ftp.sra.ebi.ac.uk/vol1/fastq/SRR830/SRR830399/SRR830399.fastq.gz
	wget ftp://ftp.sra.ebi.ac.uk/vol1/fastq/SRR867/SRR867201/SRR867201.fastq.gz
	wget ftp://ftp.sra.ebi.ac.uk/vol1/fastq/SRR900/SRR900790/SRR900790.fastq.gz
	wget ftp://ftp.sra.ebi.ac.uk/vol1/fastq/SRR891/SRR891361/SRR891361.fastq.gz
	wget ftp://ftp.sra.ebi.ac.uk/vol1/fastq/SRR776/SRR776566/SRR776566.fastq.gz
	

untrimmed
	
	for i in `ls *fastq`; do
		jellyfish count -m 25 -s 200M -t 12 -C -o $i.jf $i
	done
	
trim

	for i in `ls *fastq`; do
		java -Xmx30g -jar /share/trinityrnaseq_r20140717/trinity-plugins/Trimmomatic-0.32/trimmomatic-0.32.jar SE \
		-threads 12 \
		$i \
		$i.Phred20.fq \
		ILLUMINACLIP:/share/trinityrnaseq_r20140717/trinity-plugins/Trimmomatic/adapters/TruSeq3-PE.fa:2:30:10 \
		SLIDINGWINDOW:4:20 \
		LEADING:20 \
		TRAILING:20 \
		MINLEN:25
	done


    TrimmomaticSE: Started with arguments: -threads 12 SRR536828.fastq SRR536828.fastq.Phred20.fq ILLUMINACLIP:/share/trinityrnaseq_r20140717/trinity-plugins/Trimmomatic/adapters/TruSeq3-PE.fa:2:30:10 SLIDINGWINDOW:4:20 LEADING:20 TRAILING:20 MINLEN:25
    Using PrefixPair: 'TACACTCTTTCCCTACACGACGCTCTTCCGATCT' and 'GTGACTGGAGTTCAGACGTGTGCTCTTCCGATCT'
    ILLUMINACLIP: Using 1 prefix pairs, 0 forward/reverse sequences, 0 forward only sequences, 0 reverse only sequences
    Quality encoding detected as phred64
    Input Reads: 22369924 Surviving: 20916999 (93.51%) Dropped: 1452925 (6.49%)
    TrimmomaticSE: Completed successfully
    
    TrimmomaticSE: Started with arguments: -threads 12 SRR536829.fastq SRR536829.fastq.Phred20.fq ILLUMINACLIP:/share/trinityrnaseq_r20140717/trinity-plugins/Trimmomatic/adapters/TruSeq3-PE.fa:2:30:10 SLIDINGWINDOW:4:20 LEADING:20 TRAILING:20 MINLEN:25
    Using PrefixPair: 'TACACTCTTTCCCTACACGACGCTCTTCCGATCT' and 'GTGACTGGAGTTCAGACGTGTGCTCTTCCGATCT'
    ILLUMINACLIP: Using 1 prefix pairs, 0 forward/reverse sequences, 0 forward only sequences, 0 reverse only sequences
    Quality encoding detected as phred64
    Input Reads: 26170444 Surviving: 24395261 (93.22%) Dropped: 1775183 (6.78%)
    TrimmomaticSE: Completed successfully
    
    TrimmomaticSE: Started with arguments: -threads 12 SRR575726.fastq SRR575726.fastq.Phred20.fq ILLUMINACLIP:/share/trinityrnaseq_r20140717/trinity-plugins/Trimmomatic/adapters/TruSeq3-PE.fa:2:30:10 SLIDINGWINDOW:4:20 LEADING:20 TRAILING:20 MINLEN:25
    Using PrefixPair: 'TACACTCTTTCCCTACACGACGCTCTTCCGATCT' and 'GTGACTGGAGTTCAGACGTGTGCTCTTCCGATCT'
    ILLUMINACLIP: Using 1 prefix pairs, 0 forward/reverse sequences, 0 forward only sequences, 0 reverse only sequences
    Quality encoding detected as phred33
    Input Reads: 4000000 Surviving: 3662813 (91.57%) Dropped: 337187 (8.43%)
    TrimmomaticSE: Completed successfully
    
    TrimmomaticSE: Started with arguments: -threads 12 SRR575841.fastq SRR575841.fastq.Phred20.fq ILLUMINACLIP:/share/trinityrnaseq_r20140717/trinity-plugins/Trimmomatic/adapters/TruSeq3-PE.fa:2:30:10 SLIDINGWINDOW:4:20 LEADING:20 TRAILING:20 MINLEN:25
    Using PrefixPair: 'TACACTCTTTCCCTACACGACGCTCTTCCGATCT' and 'GTGACTGGAGTTCAGACGTGTGCTCTTCCGATCT'
    ILLUMINACLIP: Using 1 prefix pairs, 0 forward/reverse sequences, 0 forward only sequences, 0 reverse only sequences
    Quality encoding detected as phred33
    Input Reads: 4000000 Surviving: 3712049 (92.80%) Dropped: 287951 (7.20%)
    TrimmomaticSE: Completed successfully
    
    TrimmomaticSE: Started with arguments: -threads 12 SRR656612.fastq SRR656612.fastq.Phred20.fq ILLUMINACLIP:/share/trinityrnaseq_r20140717/trinity-plugins/Trimmomatic/adapters/TruSeq3-PE.fa:2:30:10 SLIDINGWINDOW:4:20 LEADING:20 TRAILING:20 MINLEN:25
    Using PrefixPair: 'TACACTCTTTCCCTACACGACGCTCTTCCGATCT' and 'GTGACTGGAGTTCAGACGTGTGCTCTTCCGATCT'
    ILLUMINACLIP: Using 1 prefix pairs, 0 forward/reverse sequences, 0 forward only sequences, 0 reverse only sequences
    Quality encoding detected as phred64
    Input Reads: 29112785 Surviving: 28437192 (97.68%) Dropped: 675593 (2.32%)
    TrimmomaticSE: Completed successfully
    
    TrimmomaticSE: Started with arguments: -threads 12 SRR776537.fastq SRR776537.fastq.Phred20.fq ILLUMINACLIP:/share/trinityrnaseq_r20140717/trinity-plugins/Trimmomatic/adapters/TruSeq3-PE.fa:2:30:10 SLIDINGWINDOW:4:20 LEADING:20 TRAILING:20 MINLEN:25
    Using PrefixPair: 'TACACTCTTTCCCTACACGACGCTCTTCCGATCT' and 'GTGACTGGAGTTCAGACGTGTGCTCTTCCGATCT'
    ILLUMINACLIP: Using 1 prefix pairs, 0 forward/reverse sequences, 0 forward only sequences, 0 reverse only sequences
    Quality encoding detected as phred64
    Input Reads: 31036922 Surviving: 30380536 (97.89%) Dropped: 656386 (2.11%)
    TrimmomaticSE: Completed successfully
    
    TrimmomaticSE: Started with arguments: -threads 12 SRR776566.fastq SRR776566.fastq.Phred20.fq ILLUMINACLIP:/share/trinityrnaseq_r20140717/trinity-plugins/Trimmomatic/adapters/TruSeq3-PE.fa:2:30:10 SLIDINGWINDOW:4:20 LEADING:20 TRAILING:20 MINLEN:25
    Using PrefixPair: 'TACACTCTTTCCCTACACGACGCTCTTCCGATCT' and 'GTGACTGGAGTTCAGACGTGTGCTCTTCCGATCT'
    ILLUMINACLIP: Using 1 prefix pairs, 0 forward/reverse sequences, 0 forward only sequences, 0 reverse only sequences
    Quality encoding detected as phred64
    Input Reads: 19655692 Surviving: 19363295 (98.51%) Dropped: 292397 (1.49%)
    TrimmomaticSE: Completed successfully
    
    TrimmomaticSE: Started with arguments: -threads 12 SRR830399.fastq SRR830399.fastq.Phred20.fq ILLUMINACLIP:/share/trinityrnaseq_r20140717/trinity-plugins/Trimmomatic/adapters/TruSeq3-PE.fa:2:30:10 SLIDINGWINDOW:4:20 LEADING:20 TRAILING:20 MINLEN:25
    Using PrefixPair: 'TACACTCTTTCCCTACACGACGCTCTTCCGATCT' and 'GTGACTGGAGTTCAGACGTGTGCTCTTCCGATCT'
    ILLUMINACLIP: Using 1 prefix pairs, 0 forward/reverse sequences, 0 forward only sequences, 0 reverse only sequences
    Quality encoding detected as phred33
    Input Reads: 44442202 Surviving: 43162774 (97.12%) Dropped: 1279428 (2.88%)
    TrimmomaticSE: Completed successfully
    
    TrimmomaticSE: Started with arguments: -threads 12 SRR867201.fastq SRR867201.fastq.Phred20.fq ILLUMINACLIP:/share/trinityrnaseq_r20140717/trinity-plugins/Trimmomatic/adapters/TruSeq3-PE.fa:2:30:10 SLIDINGWINDOW:4:20 LEADING:20 TRAILING:20 MINLEN:25
    Using PrefixPair: 'TACACTCTTTCCCTACACGACGCTCTTCCGATCT' and 'GTGACTGGAGTTCAGACGTGTGCTCTTCCGATCT'
    ILLUMINACLIP: Using 1 prefix pairs, 0 forward/reverse sequences, 0 forward only sequences, 0 reverse only sequences
    Quality encoding detected as phred64
    Input Reads: 27015370 Surviving: 26728529 (98.94%) Dropped: 286841 (1.06%)
    TrimmomaticSE: Completed successfully
    
    TrimmomaticSE: Started with arguments: -threads 12 SRR891361.fastq SRR891361.fastq.Phred20.fq ILLUMINACLIP:/share/trinityrnaseq_r20140717/trinity-plugins/Trimmomatic/adapters/TruSeq3-PE.fa:2:30:10 SLIDINGWINDOW:4:20 LEADING:20 TRAILING:20 MINLEN:25
    Using PrefixPair: 'TACACTCTTTCCCTACACGACGCTCTTCCGATCT' and 'GTGACTGGAGTTCAGACGTGTGCTCTTCCGATCT'
    ILLUMINACLIP: Using 1 prefix pairs, 0 forward/reverse sequences, 0 forward only sequences, 0 reverse only sequences
    Quality encoding detected as phred33
    Input Reads: 12066318 Surviving: 11968917 (99.19%) Dropped: 97401 (0.81%)
    TrimmomaticSE: Completed successfully


    TrimmomaticSE: Started with arguments: -threads 12 SRR900790.fastq SRR900790.fastq.Phred20.fq ILLUMINACLIP:/share/trinityrnaseq_r20140717/trinity-plugins/Trimmomatic/adapters/TruSeq3-PE.fa:2:30:10 SLIDINGWINDOW:4:20 LEADING:20 TRAILING:20 MINLEN:25
    Using PrefixPair: 'TACACTCTTTCCCTACACGACGCTCTTCCGATCT' and 'GTGACTGGAGTTCAGACGTGTGCTCTTCCGATCT'
    ILLUMINACLIP: Using 1 prefix pairs, 0 forward/reverse sequences, 0 forward only sequences, 0 reverse only sequences
    Quality encoding detected as phred64
    Input Reads: 32129837 Surviving: 22770944 (70.87%) Dropped: 9358893 (29.13%)
    TrimmomaticSE: Completed successfully





jf trim

	
	for i in `ls *fq`; do
		jellyfish count -m 25 -s 200M -t 12 -C -o $i.jf $i
	done
	

make histograms

	for i in `ls *jf`; do
		jellyfish histo $i -o $i.histo
	done

paste things

    paste <(head -100 SRR900790.fastq.jf.histo | awk '{print $2}') \
    <(head -100 SRR891361.fastq.jf.histo | awk '{print $2}') \
    <(head -100 SRR867201.fastq.jf.histo | awk '{print $2}') \
    <(head -100 SRR830399.fastq.jf.histo | awk '{print $2}') \
    <(head -100 SRR776566.fastq.jf.histo | awk '{print $2}') \
    <(head -100 SRR776537.fastq.jf.histo | awk '{print $2}') \
    <(head -100 SRR656612.fastq.jf.histo | awk '{print $2}') \
    <(head -100 SRR575841.fastq.jf.histo | awk '{print $2}') \
    <(head -100 SRR575726.fastq.jf.histo | awk '{print $2}') \
    <(head -100 SRR536829.fastq.jf.histo | awk '{print $2}') \
    <(head -100 SRR536828.fastq.jf.histo | awk '{print $2}') \
    <(head -100 SRR900790.fastq.Phred20.fq.jf.histo | awk '{print $2}') \
    <(head -100 SRR891361.fastq.Phred20.fq.jf.histo | awk '{print $2}') \
    <(head -100 SRR867201.fastq.Phred20.fq.jf.histo | awk '{print $2}') \
    <(head -100 SRR830399.fastq.Phred20.fq.jf.histo | awk '{print $2}') \
    <(head -100 SRR776566.fastq.Phred20.fq.jf.histo | awk '{print $2}') \
    <(head -100 SRR776537.fastq.Phred20.fq.jf.histo | awk '{print $2}') \
    <(head -100 SRR656612.fastq.Phred20.fq.jf.histo | awk '{print $2}') \
    <(head -100 SRR575841.fastq.Phred20.fq.jf.histo | awk '{print $2}') \
    <(head -100 SRR575726.fastq.Phred20.fq.jf.histo | awk '{print $2}') \
    <(head -100 SRR536829.fastq.Phred20.fq.jf.histo | awk '{print $2}') \
    <(head -100 SRR536828.fastq.Phred20.fq.jf.histo | awk '{print $2}') > histo.txt
    
in R

	boxplot(
	as.numeric(1-(histo[2,12:22] / histo[2,1:11])), 
	as.numeric(1-(histo[3,12:22] / histo[3,1:11])),
	as.numeric(1-(histo[4,12:22] / histo[4,1:11])),
	as.numeric(1-(histo[5,12:22] / histo[5,1:11])),
	as.numeric(1-(histo[6,12:22] / histo[6,1:11])),
	as.numeric(1-(histo[7,12:22] / histo[7,1:11])),
	as.numeric(1-(histo[8,12:22] / histo[8,1:11])),
	as.numeric(1-(histo[9,12:22] / histo[9,1:11])),
	as.numeric(1-(histo[10,12:22] / histo[10,1:11])),
	as.numeric(1-(histo[11,12:22] / histo[11,1:11])),
	as.numeric(1-(histo[12,12:22] / histo[12,1:11])),
	as.numeric(1-(histo[13,12:22] / histo[13,1:11])),
	as.numeric(1-(histo[14,12:22] / histo[14,1:11])),
	as.numeric(1-(histo[15,12:22] / histo[15,1:11])),
	as.numeric(1-(histo[16,12:22] / histo[16,1:11])),
	as.numeric(1-(histo[17,12:22] / histo[17,1:11])),
	as.numeric(1-(histo[18,12:22] / histo[18,1:11])),
	as.numeric(1-(histo[19,12:22] / histo[19,1:11])),
	as.numeric(1-(histo[20,12:22] / histo[20,1:11])),
	col='light blue', frame.plot=F, xaxt='n',
	main='Percent loss of non-unique kmers \n No qual. trim versus trimming at Phred=20') 
	
	axis(1, at=c(1,2,3,4,5,6,7,8,9,10,11,12,13,14,15,16,17,18,19),
	labels=c('kmer_freq=2',
	"kmer_freq=3",
	"kmer_freq=4",
	"kmer_freq=5",
	"kmer_freq=6",
	"kmer_freq=7",
	"kmer_freq=8",
	"kmer_freq=9",
	"kmer_freq=10",
	"kmer_freq=11",
	"kmer_freq=12",
	"kmer_freq=13",
	"kmer_freq=14",
	"kmer_freq=15",
	"kmer_freq=16",
	"kmer_freq=17",
	"kmer_freq=18",
	"kmer_freq=19",
	"kmer_freq=20"), 
	las=2
	)
































































