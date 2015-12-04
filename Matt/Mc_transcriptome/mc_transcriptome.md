Mc_Transcriptome
--

in `$RAID/Mc_transcriptome`

       lighter -t 60 \
    -r Thomas_McOr3_R2.PF.fastq \
    -r Thomas_McOr3_R1.PF.fastq \
    -r Thomas_McOr2_R2.PF.fastq \
    -r Thomas_McOr2_R1.PF.fastq \
    -r Thomas_McOr1_R2.PF.fastq \
    -r Thomas_McOr1_R1.PF.fastq \
    -r Thomas_McBr3_R1.PF.fastq \
    -r Thomas_McBr3_R2.PF.fastq \
    -r Thomas_McBr1_R1.PF.fastq \
    -r Thomas_McBr1_R2.PF.fastq \
    -r Thomas_McBr2_R1.PF.fastq \
    -r Thomas_McBr2_R2.PF.fastq \
    -k 32 600000000 .05
    
trinity

	Trinity --seqType fq --max_memory 50G --inchworm_cpu 10 --trimmomatic \
	--left Thomas_McBr3_R1.PF.cor.fq.gz,\
	Thomas_McOr1_R1.PF.cor.fq.gz,\
	Thomas_McOr2_R1.PF.cor.fq.gz,\
	Thomas_McOr3_R1.PF.cor.fq.gz,\
	Thomas_McBr2_R1.PF.cor.fq.gz,\
	Thomas_McBr1_R1.PF.cor.fq.gz \
	--right Thomas_McBr3_R2.PF.cor.fq.gz,\
	Thomas_McOr1_R2.PF.cor.fq.gz,\
	Thomas_McOr2_R2.PF.cor.fq.gz,\
	Thomas_McOr3_R2.PF.cor.fq.gz,\
	Thomas_McBr2_R2.PF.cor.fq.gz,\
	Thomas_McBr1_R2.PF.cor.fq.gz \
	--CPU 36 --output mc_lighter_trinity --group_pairs_distance 999 --bypass_java_version_check
	
Phylosift

mcbr3


	Trinity --seqType fq --max_memory 20G --inchworm_cpu 10 --trimmomatic \
	--left Thomas_McBr3_R1.PF.cor.fq \
	--right Thomas_McBr3_R2.PF.cor.fq \
	--CPU 16 --output mcbr3_lighter_trinity --group_pairs_distance 999 --bypass_java_version_check

	phylosift all --debug --bayes --besthit --extended --threads 16 --output mcbr3 mcbr3_lighter_trinity/Trinity.fasta


	#McBr2

	Trinity --seqType fq --max_memory 20G --inchworm_cpu 10 --trimmomatic \
	--left Thomas_McBr2_R1.PF.cor.fq \
	--right Thomas_McBr2_R2.PF.cor.fq \
	--CPU 16 --output mcbr2_lighter_trinity --group_pairs_distance 999 --bypass_java_version_check


	phylosift all --debug --bayes --besthit --extended --threads 16 --output mcbr2 mcbr2_lighter_trinity/Trinity.fasta


	#McBr1

	Trinity --seqType fq --max_memory 20G --inchworm_cpu 10 --trimmomatic \
	--left Thomas_McBr1_R1.PF.cor.fq \
	--right Thomas_McBr1_R2.PF.cor.fq \
	--CPU 16 --output mcbr3_lighter_trinity --group_pairs_distance 999 --bypass_java_version_check

	phylosift all --debug --bayes --besthit --extended --threads 16 --output mcbr1 mcbr1_lighter_trinity/Trinity.fasta


	#McOr3

	Trinity --seqType fq --max_memory 20G --inchworm_cpu 10 --trimmomatic \
	--left Thomas_McOr1_R1.PF.cor.fq \
	--right Thomas_McOr1_R2.PF.cor.fq \
	--CPU 16 --output mcor1_lighter_trinity --group_pairs_distance 999 --bypass_java_version_check

	phylosift all --debug --bayes --besthit --extended --threads 16 --output mcor1 mcor1_lighter_trinity/Trinity.fasta



	#McOr2

	Trinity --seqType fq --max_memory 20G --inchworm_cpu 10 --trimmomatic \
	--left Thomas_McOr2_R1.PF.cor.fq \
	--right Thomas_McOr2_R2.PF.cor.fq \
	--CPU 16 --output mcor2_lighter_trinity --group_pairs_distance 999 --bypass_java_version_check

	phylosift all --debug --bayes --besthit --extended --threads 16 --output mcor2 mcor2_lighter_trinity/Trinity.fasta


	#McOr3

	Trinity --seqType fq --max_memory 20G --inchworm_cpu 10 --trimmomatic \
	--left Thomas_McOr3_R1.PF.cor.fq \
	--right Thomas_McOr3_R2.PF.cor.fq \
	--CPU 16 --output mcor3_lighter_trinity --group_pairs_distance 999 --bypass_java_version_check

	phylosift all --debug --bayes --besthit --extended --threads 16 --output mcor3 mcor3_lighter_trinity/Trinity.fasta


phylosift 




AWS Install Stuff
--

	cd
	apt-get update
	
	apt-get -y upgrade
	
	apt-get -y install subversion tmux git curl bowtie libncurses5-dev samtools gcc make g++ python-dev unzip dh-autoreconf default-jre python-pip zlib1g-dev
	
	git clone https://github.com/trinityrnaseq/trinityrnaseq.git
	
	cd trinityrnaseq
	
	make -j8

change in plans: this this after trinity completes
--


	cd /mnt
	wget http://edhar.genomecenter.ucdavis.edu/~koadman/phylosift/phylosift_latest.tar.bz2
	
	tar -jxf phylosift_latest.tar.bz2
	
	PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/home/ubuntu/trinityrnaseq:/mnt/phylosift_20140419

	nano /mnt/phylosift_20140419/lib/Phylosift/pplacer.pm


mod phylosift config file
--

	mkdir /mnt/markers/
	nano /mnt/config
	
contents

	$marker_dir='/mnt/markers/';
	$markers_extended_dir='/mnt/markers/';
	$ncbi_dir = '/mnt/markers/';
	$marker_path='/mnt/markers/';
	$ncbi_path='/mnt/markers/';
	$marker_base_url = 'http://edhar.genomecenter.ucdavis.edu/~koadman/phylosift_markers';
	$ncbi_url = 'http://edhar.genomecenter.ucdavis.edu/~koadman/ncbi.tgz';
	$pplacer_groups = 10;
	$pplacer_verbosity = 1;

run phylosift

	tmux new -s phylosift
	phylosift all --debug --bayes --besthit --threads 16 --output mcor3 mcor3_lighter_trinity/Trinity.fasta
	phylosift all --debug --bayes --besthit --threads 16 --output mcor2 mcor2_lighter_trinity/Trinity.fasta
	phylosift all --debug --bayes --besthit --threads 16 --output mcor1 mcor1_lighter_trinity/Trinity.fasta
	phylosift all --debug --bayes --besthit --threads 16 --output mcbr3 mcbr3_lighter_trinity/Trinity.fasta
	phylosift all --debug --bayes --besthit --threads 16 --output mcbr2 mcbr2_lighter_trinity/Trinity.fasta


bwa
--

	bwa index -p mc mc_lighter_trinity/Trinity.fasta

	bwa mem -t16 mc /mnt/Thomas_McOr3_R1.PF.cor.fq.gz /mnt/Thomas_McOr3_R2.PF.cor.fq.gz | \  
	samtools view -@36 -Sub - > McOr3.bam
	

	bwa mem -t16 mc /mnt/Thomas_McOr2_R1.PF.cor.fq.gz /mnt/Thomas_McOr2_R2.PF.cor.fq.gz | \  
	samtools view -@36 -Sub - > McOr2.bam

	bwa mem -t16 mc /mnt/Thomas_McOr3_R1.PF.cor.fq.gz /mnt/Thomas_McOr1_R2.PF.cor.fq.gz | \  
	samtools view -@36 -Sub - > McOr1.bam

	bwa mem -t16 mc /mnt/Thomas_McBr3_R1.PF.cor.fq.gz /mnt/Thomas_McOr3_R2.PF.cor.fq.gz | \  
	samtools view -@36 -Sub - > McBr3.bam

	bwa mem -t16 mc /mnt/Thomas_McBr2_R1.PF.cor.fq.gz /mnt/Thomas_McOr2_R2.PF.cor.fq.gz | \  
	samtools view -@36 -Sub - > McBr2.bam

	bwa mem -t16 mc /mnt/Thomas_McBr1_R1.PF.cor.fq.gz /mnt/Thomas_McOr1_R2.PF.cor.fq.gz | \  
	samtools view -@36 -Sub - > McBr1.bam


salmon
--

	salmon quant -p 36 --useErrorModel -t mc_lighter_trinity/Trinity.fasta -l SF \
	-a McOr3.bam McOr2.bam McOr1.bam McBr3.bam McBr2.bam McBr1.bam \
	-o salmon_quant
	


cat mcor1/quant.sf | sort -k1 | cut -f1 > 0.txt  
cat mcor1/quant.sf | sort -k1 | cut -f5 > 0a.txt  
cat mcor2/quant.sf | sort -k1 | cut -f5 > 1.txt  
cat mcor3/quant.sf | sort -k1 | cut -f5 > 2.txt  
cat mcbr1/quant.sf | sort -k1 | cut -f5 > 3.txt  
cat mcbr2/quant.sf | sort -k1 | cut -f5 > 4.txt  
cat mcbr3/quant.sf | sort -k1 | cut -f5 > 5.txt  



paste 0.txt 0a.txt 1.txt 2.txt 3.txt 4.txt 5.txt > mc.counts 


edgeR  
--

    source("http://bioconductor.org/biocLite.R")  
    biocLite("edgeR")  
    library(edgeR)  
    x <- read.delim("/Users/macmanes/Box\ Sync/mc_transcriptomr/mc.counts", row.names='name')  
    group <- factor(c(1,1,1,2,2,2))
    y <- DGEList(counts=x, group=group)
    keep <- rowSums(cpm(y) > 6) >= 2
    y <- y[keep,]
    dim(y)
    y <- calcNormFactors(y)
    y <- estimateCommonDisp(y)
    y <- estimateTagwiseDisp(y)  
    et <- exactTest(y)
    summary(de <- decideTestsDGE(et, p=0.05, adjust="BH"))
    topTags(et, n=205)
    
    detags <- rownames(y)[as.logical(de)]  
    plotSmear(et, de.tags=detags)  
    


salmon error
--

    salmon quant -p 16 -t mc_lighter_trinity/Trinity.fasta -l SF -a McOr3.bam McOr2.bam McOr1.bam McBr3.bam McBr2.bam McBr1.bam -o all
    Version Info: This is the most recent version
    
    # salmon (alignment-based) v0.3.0
    # [ program ] => salmon
    # [ command ] => quant
    # [ threads ] => { 16 }
    # [ targets ] => { mc_lighter_trinity/Trinity.fasta }
    # [ libType ] => { SF }
    # [ alignments ] => { McOr3.bam McOr2.bam McOr1.bam McBr3.bam McBr2.bam McBr1.bam }
    # [ output ] => { all }
    Library format { type:single end, relative orientation:none, strandedness:sense }
    Logs will be written to all/logs
    numQuantThreads = 10
    parseThreads = 6
    Checking that provided alignment files have consistent headers . . . done
    Populating targets from aln = "McOr3.bam", fasta = "mc_lighter_trinity/Trinity.fasta" . . .done
    
    
    
    
    processed 43000000 reads in current roundSegmentation fault (core dumped)

```

Comparison of groups:  2-1 
                        logFC   logCPM       PValue          FDR
TR84415-c10_g1_i1    6.117660 2.608842 1.727679e-18 1.723014e-14
TR85322-c4_g5_i1     5.747839 2.716495 2.214041e-14 1.104032e-10
TR27962-c0_g2_i1    -7.738951 2.141502 1.737576e-13 5.776283e-10
TR42818-c2_g6_i1    -7.834594 2.386907 5.100093e-13 1.271581e-09
TR84045-c0_g1_i1    -9.757449 1.426430 6.779835e-13 1.352306e-09
TR32765-c0_g1_i10    6.830100 1.351175 6.394455e-12 1.062865e-08
TR81796-c17_g5_i4    3.758321 2.591182 3.668463e-11 5.226512e-08
TR85318-c1_g1_i1     4.529822 2.155391 7.678907e-11 9.572717e-08
TR83846-c0_g1_i1    -7.650497 1.512587 4.437005e-10 4.916695e-07
TR53282-c0_g6_i1     4.821640 1.860390 1.075147e-09 1.072244e-06
TR4602-c2_g1_i3     10.722176 2.131712 6.156505e-09 5.581712e-06
TR84406-c0_g1_i1    -4.239428 2.957265 9.510444e-09 7.903972e-06
TR81796-c17_g5_i1    5.577063 3.206451 1.300902e-08 9.979919e-06
TR175304-c0_g1_i1    5.627497 3.018310 1.987550e-08 1.415846e-05
TR60579-c0_g5_i1    -7.561631 2.619259 2.691888e-08 1.789747e-05
TR47584-c0_g1_i2     4.604199 2.512747 7.417330e-08 4.623314e-05
TR77374-c6_g5_i1     5.501759 1.082553 1.096491e-07 6.432531e-10
TR84396-c1_g1_i2    -3.577602 2.065821 1.333359e-07 7.387550e-05
TR15087-c1_g1_i1     3.182268 3.701544 1.772699e-07 8.885773e-05
TR78336-c1_g2_i1     9.430515 1.090855 1.781966e-07 8.885773e-05
TR88584-c0_g1_i2    -4.157209 2.677060 2.159851e-07 1.020794e-04
TR84804-c5_g1_i6     3.706916 1.915113 2.251827e-07 1.020794e-04
TR52830-c2_g1_i4     3.998928 1.341076 2.606658e-07 1.111569e-04
TR85324-c0_g1_i1     9.364339 3.768747 2.682351e-07 1.111569e-04
TR45374-c1_g1_i1    -4.045476 1.888069 2.786445e-07 1.111569e-04
TR24153-c2_g1_i2     6.608468 1.226852 3.007351e-07 1.153551e-04
TR81796-c17_g6_i6    2.877900 2.451096 3.368506e-07 1.244226e-04
TR6478-c0_g1_i1      3.121960 3.703888 3.632986e-07 1.293992e-04
TR10662-c5_g1_i2     3.933377 2.966010 4.699917e-07 1.616285e-04
TR84845-c7_g1_i3     7.722308 1.159144 8.023305e-07 2.667214e-04
TR34135-c0_g1_i1    -8.321686 5.021303 8.485914e-07 2.730001e-04
TR61622-c0_g2_i1   -10.098364 1.736990 9.845368e-07 3.068370e-04
TR34021-c3_g1_i5     5.853690 1.917769 1.099681e-06 3.323369e-04
TR38814-c3_g1_i1    -3.142881 2.407608 1.311933e-06 3.848208e-04
TR6478-c0_g1_i3      3.156381 3.699455 1.481855e-06 4.222440e-04
TR84406-c0_g1_i2    -3.271290 3.002835 1.855350e-06 5.031389e-04
TR82999-c4_g3_i2     3.801288 2.607206 1.866654e-06 5.031389e-04
TR67409-c1_g3_i1     2.789055 3.915378 2.099226e-06 5.419765e-04
TR192043-c0_g1_i1   -6.214366 4.798668 2.142180e-06 5.419765e-04
TR43333-c0_g1_i1     6.511010 1.220902 2.173775e-06 5.419765e-04
TR81796-c17_g6_i8    2.795943 3.469057 2.714580e-06 6.603049e-04
TR61207-c1_g1_i2    -3.744985 2.527549 2.916344e-06 6.924929e-04
TR15033-c0_g1_i1     3.169759 2.738274 3.241119e-06 7.517135e-04
TR47056-c0_g1_i1     8.101227 2.808541 4.323604e-06 9.799843e-04
TR15033-c5_g13_i1    3.488982 3.220113 4.489279e-06 9.949239e-04
TR81796-c17_g6_i1    3.319414 4.263585 5.783182e-06 1.253819e-03
TR44634-c3_g1_i2     2.561662 2.584203 5.910985e-06 1.254261e-03
TR15033-c5_g13_i5    3.550401 3.641190 6.112059e-06 1.269908e-03
TR15033-c5_g13_i11   3.417942 3.331380 7.199304e-06 1.465279e-03
TR81796-c17_g6_i3    2.667794 2.296289 7.952060e-06 1.586118e-03
TR5709-c1_g4_i5     -4.277591 1.923980 8.535127e-06 1.643737e-03
TR19631-c0_g2_i1    -4.215898 2.579153 8.570574e-06 1.643737e-03
TR26936-c0_g1_i1    -3.801002 1.955252 9.262116e-06 1.742851e-03
TR38794-c2_g2_i7     4.898768 3.456922 1.018628e-05 1.881255e-03
TR53725-c0_g1_i1    -6.417935 4.211672 1.040343e-05 1.886425e-03
TR19631-c0_g2_i2    -2.981505 2.545521 1.211182e-05 2.156985e-03
TR63191-c0_g1_i1     2.540183 2.372471 1.290946e-05 2.258702e-03
TR4583-c3_g2_i1      6.774579 5.983387 1.396590e-05 2.382879e-03
TR81796-c17_g6_i2    3.231531 4.343726 1.409705e-05 2.382879e-03
TR15033-c5_g13_i2    3.090775 3.307248 1.609774e-05 2.675713e-03
TR65149-c2_g1_i2    -5.799988 1.282455 1.893222e-05 3.050819e-03
TR10521-c0_g1_i1    -3.854560 2.417029 1.896628e-05 3.050819e-03
TR15033-c5_g2_i1     2.983003 2.573333 1.932508e-05 3.059190e-03
TR15033-c5_g13_i9    2.527844 2.445823 2.199933e-05 3.428114e-03
TR2712-c0_g2_i1      3.306628 5.868281 2.460725e-05 3.775510e-03
TR62711-c1_g2_i6     2.690114 3.962399 2.700254e-05 4.080247e-03
TR15033-c5_g13_i8    3.437053 2.808176 2.822943e-05 4.201971e-03
TR164547-c0_g1_i1    6.081990 6.957542 3.102412e-05 4.550051e-03
TR45449-c0_g1_i1     3.887398 3.269503 3.791229e-05 5.479699e-03
TR194606-c0_g2_i1    6.553863 7.140197 4.493526e-05 6.401991e-03
TR40134-c1_g2_i1     4.147836 2.790054 4.687795e-05 6.584702e-03
TR15033-c5_g13_i4    2.993802 4.235371 5.274136e-05 7.305411e-03
TR38924-c1_g2_i1     4.356838 8.083563 6.238058e-05 8.494312e-03
TR15033-c5_g13_i10   3.066280 4.318281 6.302808e-05 8.494312e-03
TR5709-c1_g4_i2     -3.160486 1.503521 7.045217e-05 9.368260e-03
TR4611-c3_g7_i2      3.386020 2.590773 7.330814e-05 9.619765e-03
TR65146-c2_g1_i3    -3.569522 1.737226 7.815305e-05 1.012234e-02
TR28849-c0_g6_i1    -5.725222 1.144249 8.603723e-05 1.093941e-02
TR39081-c1_g4_i2     3.943298 3.096315 8.756933e-05 1.093941e-02
TR28849-c0_g7_i1    -3.195190 4.857446 8.775222e-05 1.093941e-02
TR72774-c1_g1_i1    -3.306298 1.567039 9.581227e-05 1.179674e-02
TR19631-c0_g2_i3    -3.673913 4.226889 9.722616e-05 1.182484e-02
TR167940-c0_g1_i1    6.264736 1.650127 1.156528e-04 1.389645e-02
TR10521-c0_g1_i2    -3.058613 2.287093 1.251765e-04 1.486173e-02
TR14751-c1_g1_i7     2.623069 3.039509 1.365244e-04 1.598477e-02
TR68106-c6_g10_i4    3.985732 3.257392 1.378412e-04 1.598477e-02
TR28373-c5_g3_i1     4.395108 1.234094 1.683846e-04 1.926199e-02
TR36213-c0_g1_i2     6.165426 2.225268 1.713744e-04 1.926199e-02
TR76162-c1_g1_i1     4.685168 2.953199 1.718958e-04 1.926199e-02
TR5709-c1_g4_i6     -3.124475 1.422849 1.815418e-04 2.011685e-02
TR4604-c8_g2_i2      2.351339 2.620501 1.868042e-04 2.047251e-02
TR68106-c6_g10_i2    4.646490 5.027150 2.157744e-04 2.339042e-02
TR84858-c2_g2_i1     2.215711 4.795918 2.415442e-04 2.590237e-02
TR14771-c2_g1_i1     3.642864 1.626363 2.696826e-04 2.823545e-02
TR40416-c2_g2_i6     1.888002 2.289598 2.696877e-04 2.823545e-02
TR40384-c0_g1_i8     2.275730 2.609893 2.732477e-04 2.823545e-02
TR32808-c1_g1_i1     2.068600 2.655836 2.746253e-04 2.823545e-02
TR8811-c1_g2_i13     2.607997 2.066278 2.816446e-04 2.866165e-02
TR1718-c2_g1_i3      2.293891 2.656183 2.940979e-04 2.962665e-02
TR75072-c2_g1_i3     4.760360 3.154087 3.057268e-04 3.049013e-02
TR31607-c0_g1_i2     6.198198 4.373007 3.149429e-04 3.109827e-02
TR798-c6_g6_i1       5.735792 3.592402 3.338627e-04 3.264326e-02
TR76962-c0_g1_i1     3.505766 3.664750 3.682830e-04 3.551071e-02
TR19806-c0_g1_i2    -2.433509 4.049941 3.703112e-04 3.551071e-02
TR65149-c2_g1_i1    -4.620255 1.712487 3.803883e-04 3.612964e-02
TR82701-c3_g1_i1    -2.280592 3.011137 3.868769e-04 3.639928e-02
TR224210-c0_g1_i1   -2.822143 5.868542 3.958479e-04 3.689524e-02
TR191930-c0_g1_i1    3.381119 5.220499 4.246613e-04 3.921433e-02
TR77507-c0_g1_i2     6.845045 6.342689 4.541639e-04 4.155391e-02
TR68951-c1_g2_i1    -2.002932 2.291400 5.077749e-04 4.603672e-02
TR42818-c2_g5_i1    -2.770217 2.142000 5.667517e-04 5.078928e-02
```

GFP
--
```
gi|16508124|gb|AY056460.1|      97.91   0.0     TR75761-c4_g1_i1
gi|15425964|gb|AF406766.1|      97.44   0.0     TR27784-c2_g1_i4
gi|15298095|gb|AF384683.2|      86.74   0.0     TR27784-c2_g1_i8
gi|37287362|gb|AY362545.1|      92.71   0.0     TR27784-c2_g1_i5
gi|21303777|gb|AY037768.1|      97.13   0.0     TR27784-c2_g1_i4
gi|154814327|gb|EU035536.1|     89.77   0.0     TR27784-c2_g1_i4
gi|154814325|gb|EU035535.1|     95.82   0.0     TR27784-c2_g1_i8
gi|154814323|gb|EU035534.1|     91.99   0.0     TR27784-c2_g1_i4
gi|154814321|gb|EU035533.1|     97.04   0.0     TR27784-c2_g1_i8
gi|154814319|gb|EU035532.1|     94.77   0.0     TR27784-c2_g1_i8
gi|154814317|gb|EU035531.1|     90.42   0.0     TR27784-c2_g1_i4
gi|154814315|gb|EU035530.1|     88.73   0.0     TR27784-c2_g1_i5
gi|154814313|gb|EU035529.1|     97.91   0.0     TR27784-c2_g1_i4
gi|154814311|gb|EU035528.1|     90.20   0.0     TR27784-c2_g1_i4
gi|154814309|gb|EU035527.1|     97.93   0.0     TR75761-c4_g1_i1

```



```
name	mcor1	mcor2	mcor3	mcbr1	mcbr2	mcbr3
TR75761-c4_g1_i1 (cyan fluorescent protein )	41.1507	91	276	34	7	4
TR27784-c2_g1_i4 (green fluorescent protein)	43	886.024	76	185.383	110	66
TR27784-c2_g1_i8 (isolate 9 green fluorescent protein)	104.796	255.059	198.076	310.571 101.009 130.581
TR27784-c2_g1_i5 (photoconvertible fluorescent protein)	112.911	538	240.557	231.361	58 105

```


Mc blast


    blastx -db uniprot -max_target_seqs 1 -query loose.up.in.orange.fasta \
    -outfmt '6 qseqid evalue stitle' -evalue 1e-10 -num_threads 20 -out loose.up.in.orange.uniprot.blastx
    
    blastx -db uniprot -max_target_seqs 1 -query loose.up.in.brown.fasta \
    -outfmt '6 qseqid evalue stitle' -evalue 1e-10 -num_threads 20 -out loose.up.in.brown.uniprot.blastx

Phycoer

```
name	evalue	ID	mcor1	mcor2	mcor3	mcbr1	mcbr2	mcbr3
TR162043-c0_g1_i1	2e-75	phycoerythrin-alpha-chain	3	0	6	16	4	1
TR43136-c0_g1_i1	5e-11	phycoerythrin-class-2-subunit-gamma-linker-polypeptide 0	0	0	0	3	0
TR115666-c0_g1_i1	1e-78	phycoerythrin-beta-subunit		0	0	4	5	2	0
TR81874-c3_g1_i16	1.3	phycoerythrin-lyase-subunit		19	8	23	3	12	9.97835
TR182201-c0_g1_i1	1e-48	Glutaredoxin-like-domain-fused-to-phycoerythrin-related-domain		7	26	15	1	28	9
TR115666-c0_g1_i1	2e-64	Phycoerythrin-class-III-beta-chain-CpeB		0	0	4	5	2	0

```

edgeR Hacking
--
    source("http://bioconductor.org/biocLite.R")  
    biocLite("edgeR")  
    library(edgeR)  
    x <- read.delim("/Users/macmanes/Box\ Sync/mc_transcriptomr/mc.counts", row.names='name')  
    group <- factor(c(1,1,1,2,2,2))
    y <- DGEList(counts=x, group=group)
    keep <- rowSums(cpm(y) > 4) >= 3
    #keep <- rowSums(cpm(y) > 1) >= 3 #382 diff expression
    y <- y[keep,]
    dim(y)
    y <- calcNormFactors(y)
    y <- estimateCommonDisp(y)
    y <- estimateTagwiseDisp(y)  
    et <- exactTest(y)
    summary(de <- decideTestsDGE(et, p=0.05, adjust="BH"))
    topTags(et, n=80)



```
for i in $(ls *fasta); do
   F=`basename $i .fasta`;
   python3 ~/BUSCO_v1.1b1/BUSCO_v1.1b1.py -g $i -m Trans --cpu 32 -o $F -l metazoa;
done
```

trinity 
--

```
Trinity --seqType fq --max_memory 30G --inchworm_cpu 10 --trimmomatic \
--left ../reads/Thomas_McBr3_R1.PF.cor.fq.gz,\
../reads/Thomas_McOr1_R1.PF.cor.fq.gz \
--right ../reads/Thomas_McBr3_R2.PF.cor.fq.gz,\
../reads/Thomas_McOr1_R2.PF.cor.fq.gz \
--CPU 32 --output mc_lighter_BR3OR1_trinity --group_pairs_distance 999 --full_cleanup
```

BUSCO for existing assemblies, which were done individually and ask per above;
-

```
::::::::::::::
run_mcbr1.Trinity/short_summary_mcbr1.Trinity
::::::::::::::
#Summarized BUSCO benchmarking for file: mcbr1.Trinity.fasta
#BUSCO was run in mode: genome

Summarized benchmarks in BUSCO notation:
	C:5.1%[D:1.3%],F:9.7%,M:85%,n:843

Representing:
	43	Complete Single-Copy BUSCOs
	11	Complete Duplicated BUSCOs
	82	Fragmented BUSCOs
	718	Missing BUSCOs
	843	Total BUSCO groups searched
::::::::::::::
run_mcbr2.Trinity/short_summary_mcbr2.Trinity
::::::::::::::
#Summarized BUSCO benchmarking for file: mcbr2.Trinity.fasta
#BUSCO was run in mode: genome

Summarized benchmarks in BUSCO notation:
	C:13%[D:4.5%],F:16%,M:69%,n:843

Representing:
	117	Complete Single-Copy BUSCOs
	38	Complete Duplicated BUSCOs
	141	Fragmented BUSCOs
	585	Missing BUSCOs
	843	Total BUSCO groups searched
::::::::::::::
run_mcbr3.Trinity/short_summary_mcbr3.Trinity
::::::::::::::
#Summarized BUSCO benchmarking for file: mcbr3.Trinity.fasta
#BUSCO was run in mode: genome

Summarized benchmarks in BUSCO notation:
	C:43%[D:16%],F:19%,M:36%,n:843

Representing:
	366	Complete Single-Copy BUSCOs
	143	Complete Duplicated BUSCOs
	168	Fragmented BUSCOs
	309	Missing BUSCOs
	843	Total BUSCO groups searched
::::::::::::::
run_mcor1.Trinity/short_summary_mcor1.Trinity
::::::::::::::
#Summarized BUSCO benchmarking for file: mcor1.Trinity.fasta
#BUSCO was run in mode: genome

Summarized benchmarks in BUSCO notation:
	C:48%[D:13%],F:21%,M:30%,n:843

Representing:
	410	Complete Single-Copy BUSCOs
	117	Complete Duplicated BUSCOs
	180	Fragmented BUSCOs
	253	Missing BUSCOs
	843	Total BUSCO groups searched
::::::::::::::
run_mcor2.Trinity/short_summary_mcor2.Trinity
::::::::::::::
#Summarized BUSCO benchmarking for file: mcor2.Trinity.fasta
#BUSCO was run in mode: genome

Summarized benchmarks in BUSCO notation:
	C:46%[D:18%],F:22%,M:30%,n:843

Representing:
	394	Complete Single-Copy BUSCOs
	152	Complete Duplicated BUSCOs
	190	Fragmented BUSCOs
	259	Missing BUSCOs
	843	Total BUSCO groups searched
::::::::::::::
run_mcor3.Trinity/short_summary_mcor3.Trinity
::::::::::::::
#Summarized BUSCO benchmarking for file: mcor3.Trinity.fasta
#BUSCO was run in mode: genome

Summarized benchmarks in BUSCO notation:
	C:44%[D:17%],F:20%,M:34%,n:843

Representing:
	375	Complete Single-Copy BUSCOs
	144	Complete Duplicated BUSCOs
	177	Fragmented BUSCOs
	291	Missing BUSCOs
	843	Total BUSCO groups searched
::::::::::::::
run_Trinity/short_summary_Trinity
::::::::::::::
#Summarized BUSCO benchmarking for file: Trinity.fasta
#BUSCO was run in mode: genome

Summarized benchmarks in BUSCO notation:
	C:83%[D:53%],F:9.9%,M:6.8%,n:843

Representing:
	701	Complete Single-Copy BUSCOs
	449	Complete Duplicated BUSCOs
	84	Fragmented BUSCOs
	58	Missing BUSCOs
	843	Total BUSCO groups searched
```

transrate
--

```
transrate -a ../assembly/Trinity.fasta -t 6 -o mc_firstjoint_assembly \
-l ../reads/Thomas_McBr3_R1.PF.cor.fq.gz,../reads/Thomas_McOr1_R1.PF.cor.fq.gz \
-r ../reads/Thomas_McBr3_R2.PF.cor.fq.gz,../reads/Thomas_McOr1_R2.PF.cor.fq.gz
```





TMP calc final assembly

```

kallisto index -i transcripts2.idx ../assembly/Montastrea.trinity.fasta
~/salmon-0.5.1/bin/salmon index -t ../assembly/Montastrea.trinity.fasta -i transcripts2_index --type quasi -k 31





kallisto quant -t 32 -i transcripts2.idx -o kallisto_McBr1 -b 100 \
../reads/Thomas_McBr1_R1.PF.cor.fq.gz \
../reads/Thomas_McBr1_R2.PF.cor.fq.gz

kallisto quant -t 32 -i transcripts2.idx -o kallisto_McBr2 -b 100 \
../reads/Thomas_McBr2_R1.PF.cor.fq.gz \
../reads/Thomas_McBr2_R2.PF.cor.fq.gz

kallisto quant -t 32 -i transcripts2.idx -o kallisto_McBr3 -b 100 \
../reads/Thomas_McBr3_R1.PF.cor.fq.gz \
../reads/Thomas_McBr3_R2.PF.cor.fq.gz


~/salmon-0.5.1/bin/salmon quant -p 32 -i transcripts2_index -l MSR \
-1 <(gzip -cd ../reads/Thomas_McBr3_R1.PF.cor.fq.gz) \
-2 <(gzip -cd ../reads/Thomas_McBr3_R2.PF.cor.fq.gz) -o salmon_McBr3

~/salmon-0.5.1/bin/salmon quant -p 32 -i transcripts2_index -l MSR \
-1 <(gzip -cd ../reads/Thomas_McBr1_R1.PF.cor.fq.gz) \
-2 <(gzip -cd ../reads/Thomas_McBr1_R2.PF.cor.fq.gz) -o salmon_McBr1

~/salmon-0.5.1/bin/salmon quant -p 32 -i transcripts2_index -l MSR \
-1 <(gzip -cd ../reads/Thomas_McBr2_R1.PF.cor.fq.gz) \
-2 <(gzip -cd ../reads/Thomas_McBr2_R2.PF.cor.fq.gz) -o salmon_McBr2



kallisto quant -t 32 -i transcripts2.idx -o kallisto_McOr1 -b 100 \
../reads/Thomas_McOr1_R1.PF.cor.fq.gz \
../reads/Thomas_McOr1_R2.PF.cor.fq.gz

kallisto quant -t 32 -i transcripts2.idx -o kallisto_McOr2 -b 100 \
../reads/Thomas_McOr2_R1.PF.cor.fq.gz \
../reads/Thomas_McOr2_R2.PF.cor.fq.gz

kallisto quant -t 32 -i transcripts2.idx -o kallisto_McOr3 -b 100 \
../reads/Thomas_McOr3_R1.PF.cor.fq.gz \
../reads/Thomas_McOr3_R2.PF.cor.fq.gz

~/salmon-0.5.1/bin/salmon quant -p 32 -i transcripts2_index -l MSR \
-1 <(gzip -cd ../reads/Thomas_McOr3_R1.PF.cor.fq.gz) \
-2 <(gzip -cd ../reads/Thomas_McOr3_R2.PF.cor.fq.gz) -o salmon_McOr3

~/salmon-0.5.1/bin/salmon quant -p 32 -i transcripts2_index -l MSR \
-1 <(gzip -cd ../reads/Thomas_McOr2_R1.PF.cor.fq.gz) \
-2 <(gzip -cd ../reads/Thomas_McOr2_R2.PF.cor.fq.gz) -o salmon_McOr2

~/salmon-0.5.1/bin/salmon quant -p 32 -i transcripts2_index -l MSR \
-1 <(gzip -cd ../reads/Thomas_McOr1_R1.PF.cor.fq.gz) \
-2 <(gzip -cd ../reads/Thomas_McOr1_R2.PF.cor.fq.gz) -o salmon_McOr1


```

filter

```

awk '1>$5{next}1' kallisto_McOr1/abundance.tsv | awk '{print $1}' | sed  '1d' > kallisto.McOr1.list
awk '1>$5{next}1' kallisto_McOr2/abundance.tsv | awk '{print $1}' | sed  '1d' > kallisto.McOr2.list
awk '1>$5{next}1' kallisto_McOr3/abundance.tsv | awk '{print $1}' | sed  '1d' > kallisto.McOr3.list
awk '1>$3{next}1' salmon_McOr3/quant.sf | awk '{print $1}' | sed  '1d' > salmon.McOr3.list
awk '1>$3{next}1' salmon_McOr2/quant.sf | awk '{print $1}' | sed  '1d' > salmon.McOr2.list
awk '1>$3{next}1' salmon_McOr1/quant.sf | awk '{print $1}' | sed  '1d' > salmon.McOr1.list

awk '1>$3{next}1' salmon_McBr3/quant.sf | awk '{print $1}' | sed  '1d' > salmon.McBr3.list
awk '1>$3{next}1' salmon_McBr2/quant.sf | awk '{print $1}' | sed  '1d' > salmon.McBr2.list
awk '1>$3{next}1' salmon_McBr1/quant.sf | awk '{print $1}' | sed  '1d' > salmon.McBr1.list
awk '1>$5{next}1' kallisto_McBr1/abundance.tsv | awk '{print $1}' | sed  '1d' > kallisto.McBr1.list
awk '1>$5{next}1' kallisto_McBr2/abundance.tsv | awk '{print $1}' | sed  '1d' > kallisto.McBr2.list
awk '1>$5{next}1' kallisto_McBr3/abundance.tsv | awk '{print $1}' | sed  '1d' > kallisto.McBr3.list
cat *list | sort | uniq | wc -l

cat *list | sort | uniq > highexp

```



```
split -l 6000 highexp
for i in `cat xaa`; do grep --no-group-separator --max-count=1 -A1 -w $i ../assembly/Montastrea.trinity.fasta >> xaa.fa; done &
for i in `cat xab`; do grep --no-group-separator --max-count=1 -A1 -w $i ../assembly/Montastrea.trinity.fasta >> xab.fa; done &
for i in `cat xac`; do grep --no-group-separator --max-count=1 -A1 -w $i ../assembly/Montastrea.trinity.fasta >> xac.fa; done &
for i in `cat xad`; do grep --no-group-separator --max-count=1 -A1 -w $i ../assembly/Montastrea.trinity.fasta >> xad.fa; done &
for i in `cat xae`; do grep --no-group-separator --max-count=1 -A1 -w $i ../assembly/Montastrea.trinity.fasta >> xae.fa; done &
for i in `cat xaf`; do grep --no-group-separator --max-count=1 -A1 -w $i ../assembly/Montastrea.trinity.fasta >> xaf.fa; done &
for i in `cat xag`; do grep --no-group-separator --max-count=1 -A1 -w $i ../assembly/Montastrea.trinity.fasta >> xag.fa; done &
for i in `cat xah`; do grep --no-group-separator --max-count=1 -A1 -w $i ../assembly/Montastrea.trinity.fasta >> xah.fa; done &
for i in `cat xai`; do grep --no-group-separator --max-count=1 -A1 -w $i ../assembly/Montastrea.trinity.fasta >> xai.fa; done &
for i in `cat xaj`; do grep --no-group-separator --max-count=1 -A1 -w $i ../assembly/Montastrea.trinity.fasta >> xaj.fa; done &
for i in `cat xak`; do grep --no-group-separator --max-count=1 -A1 -w $i ../assembly/Montastrea.trinity.fasta >> xak.fa; done &
for i in `cat xal`; do grep --no-group-separator --max-count=1 -A1 -w $i ../assembly/Montastrea.trinity.fasta >> xal.fa; done &
for i in `cat xam`; do grep --no-group-separator --max-count=1 -A1 -w $i ../assembly/Montastrea.trinity.fasta >> xam.fa; done &
for i in `cat xan`; do grep --no-group-separator --max-count=1 -A1 -w $i ../assembly/Montastrea.trinity.fasta >> xan.fa; done &
for i in `cat xao`; do grep --no-group-separator --max-count=1 -A1 -w $i ../assembly/Montastrea.trinity.fasta >> xao.fa; done &
for i in `cat xap`; do grep --no-group-separator --max-count=1 -A1 -w $i ../assembly/Montastrea.trinity.fasta >> xap.fa; done &
for i in `cat xaq`; do grep --no-group-separator --max-count=1 -A1 -w $i ../assembly/Montastrea.trinity.fasta >> xaq.fa; done &
for i in `cat xar`; do grep --no-group-separator --max-count=1 -A1 -w $i ../assembly/Montastrea.trinity.fasta >> xar.fa; done &
for i in `cat xas`; do grep --no-group-separator --max-count=1 -A1 -w $i ../assembly/Montastrea.trinity.fasta >> xas.fa; done &
for i in `cat xat`; do grep --no-group-separator --max-count=1 -A1 -w $i ../assembly/Montastrea.trinity.fasta >> xat.fa; done &
for i in `cat xau`; do grep --no-group-separator --max-count=1 -A1 -w $i ../assembly/Montastrea.trinity.fasta >> xau.fa; done &
for i in `cat xav`; do grep --no-group-separator --max-count=1 -A1 -w $i ../assembly/Montastrea.trinity.fasta >> xav.fa; done &
for i in `cat xaw`; do grep --no-group-separator --max-count=1 -A1 -w $i ../assembly/Montastrea.trinity.fasta >> xaw.fa; done &
for i in `cat xax`; do grep --no-group-separator --max-count=1 -A1 -w $i ../assembly/Montastrea.trinity.fasta >> xax.fa; done &
for i in `cat xay`; do grep --no-group-separator --max-count=1 -A1 -w $i ../assembly/Montastrea.trinity.fasta >> xay.fa; done &
for i in `cat xaz`; do grep --no-group-separator --max-count=1 -A1 -w $i ../assembly/Montastrea.trinity.fasta >> xaz.fa; done &
for i in `cat xba`; do grep --no-group-separator --max-count=1 -A1 -w $i ../assembly/Montastrea.trinity.fasta >> xba.fa; done &
for i in `cat xbb`; do grep --no-group-separator --max-count=1 -A1 -w $i ../assembly/Montastrea.trinity.fasta >> xbb.fa; done &
for i in `cat xbc`; do grep --no-group-separator --max-count=1 -A1 -w $i ../assembly/Montastrea.trinity.fasta >> xbc.fa; done &
for i in `cat xbd`; do grep --no-group-separator --max-count=1 -A1 -w $i ../assembly/Montastrea.trinity.fasta >> xbd.fa; done &

cat *fa > ../assembly/Montastrea.trinity.v2.fasta


transrate -a /mnt/mc/assembly/Montastrea.trinity.v2.fasta \
-t 12 -o Montastrea.trinity.v2 \
-l ../reads/Thomas_McBr3_R1.PF.cor.fq.gz,../reads/Thomas_McBr2_R1.PF.cor.fq.gz,../reads/Thomas_McOr1_R1.PF.cor.fq.gz,../reads/Thomas_McOr3_R1.PF.cor.fq.gz \
-r ../reads/Thomas_McBr3_R2.PF.cor.fq.gz,../reads/Thomas_McBr2_R2.PF.cor.fq.gz,../reads/Thomas_McOr1_R2.PF.cor.fq.gz,../reads/Thomas_McOr3_R2.PF.cor.fq.gz


python3 ~/BUSCO_v1.1b1/BUSCO_v1.1b1.py -g /mnt/mc/assembly/Montastrea.trinity.v2.fasta \
-m Trans --cpu 22 -o Montastrea.trinity.v2 -l metazoa

```
BUSCO results
--

```
ubuntu@ip-172-31-56-29:/mnt/mc/busco$ more run_Montastrea.trinity.v2/short_summary_Montastrea.trinity.v2
#Summarized BUSCO benchmarking for file: /mnt/mc/assembly/Montastrea.trinity.v2.fasta
#BUSCO was run in mode: genome

Summarized benchmarks in BUSCO notation:
        C:82%[D:43%],F:8.5%,M:9.0%,n:843

Representing:
        695     Complete Single-Copy BUSCOs
        369     Complete Duplicated BUSCOs
        72      Fragmented BUSCOs
        76      Missing BUSCOs
        843     Total BUSCO groups searched
```

dammit
--

in `/mnt/mc/dammit`

```
dammit annotate /mnt/mc/assembly/Montastrea.trinity.v2.fasta --busco-group metazoa --n_threads 36 --database-dir /mnt/dammit/
```

blast
--

```
mkdir /mnt/mc/blast && cd /mnt/mc/blast
ln -s /mnt/blast/uniprot* .
split -l 11000  /mnt/mc/assembly/Montastrea.trinity.v2.fasta

blastx -db uniprot_sprot.fasta -max_target_seqs 1 -evalue 1e-10 -num_threads 1 -outfmt 6 \
-query xaa > xaa.blastx &
blastx -db uniprot_sprot.fasta -max_target_seqs 1 -evalue 1e-10 -num_threads 1 -outfmt 6 \
-query xab > xab.blastx &
blastx -db uniprot_sprot.fasta -max_target_seqs 1 -evalue 1e-10 -num_threads 1 -outfmt 6 \
-query xac > xac.blastx &
blastx -db uniprot_sprot.fasta -max_target_seqs 1 -evalue 1e-10 -num_threads 1 -outfmt 6 \
-query xad > xad.blastx &
blastx -db uniprot_sprot.fasta -max_target_seqs 1 -evalue 1e-10 -num_threads 1 -outfmt 6 \
-query xae > xae.blastx &
blastx -db uniprot_sprot.fasta -max_target_seqs 1 -evalue 1e-10 -num_threads 1 -outfmt 6 \
-query xaf > xaf.blastx &
blastx -db uniprot_sprot.fasta -max_target_seqs 1 -evalue 1e-10 -num_threads 1 -outfmt 6 \
-query xag > xag.blastx &
blastx -db uniprot_sprot.fasta -max_target_seqs 1 -evalue 1e-10 -num_threads 1 -outfmt 6 \
-query xah > xah.blastx &
blastx -db uniprot_sprot.fasta -max_target_seqs 1 -evalue 1e-10 -num_threads 1 -outfmt 6 \
-query xai > xai.blastx &
blastx -db uniprot_sprot.fasta -max_target_seqs 1 -evalue 1e-10 -num_threads 1 -outfmt 6 \
-query xaj > xaj.blastx &
blastx -db uniprot_sprot.fasta -max_target_seqs 1 -evalue 1e-10 -num_threads 1 -outfmt 6 \
-query xak > xak.blastx &
blastx -db uniprot_sprot.fasta -max_target_seqs 1 -evalue 1e-10 -num_threads 1 -outfmt 6 \
-query xal > xal.blastx &
blastx -db uniprot_sprot.fasta -max_target_seqs 1 -evalue 1e-10 -num_threads 1 -outfmt 6 \
-query xam > xam.blastx &
blastx -db uniprot_sprot.fasta -max_target_seqs 1 -evalue 1e-10 -num_threads 1 -outfmt 6 \
-query xan > xan.blastx &
blastx -db uniprot_sprot.fasta -max_target_seqs 1 -evalue 1e-10 -num_threads 1 -outfmt 6 \
-query xao > xao.blastx &
blastx -db uniprot_sprot.fasta -max_target_seqs 1 -evalue 1e-10 -num_threads 1 -outfmt 6 \
-query xap > xap.blastx &
blastx -db uniprot_sprot.fasta -max_target_seqs 1 -evalue 1e-10 -num_threads 1 -outfmt 6 \
-query xaq > xaq.blastx &
blastx -db uniprot_sprot.fasta -max_target_seqs 1 -evalue 1e-10 -num_threads 1 -outfmt 6 \
-query xar > xar.blastx &
blastx -db uniprot_sprot.fasta -max_target_seqs 1 -evalue 1e-10 -num_threads 1 -outfmt 6 \
-query xas > xas.blastx &
blastx -db uniprot_sprot.fasta -max_target_seqs 1 -evalue 1e-10 -num_threads 1 -outfmt 6 \
-query xat > xat.blastx &
blastx -db uniprot_sprot.fasta -max_target_seqs 1 -evalue 1e-10 -num_threads 1 -outfmt 6 \
-query xau > xau.blastx &
blastx -db uniprot_sprot.fasta -max_target_seqs 1 -evalue 1e-10 -num_threads 1 -outfmt 6 \
-query xav > xav.blastx &


blastx -db uniprot_sprot.fasta -max_target_seqs 1 -evalue 1e-10 -num_threads 1 -outfmt 6 \
-query xaw > xaw.blastx &
blastx -db uniprot_sprot.fasta -max_target_seqs 1 -evalue 1e-10 -num_threads 1 -outfmt 6 \
-query xax > xax.blastx &
blastx -db uniprot_sprot.fasta -max_target_seqs 1 -evalue 1e-10 -num_threads 1 -outfmt 6 \
-query xay > xay.blastx &
blastx -db uniprot_sprot.fasta -max_target_seqs 1 -evalue 1e-10 -num_threads 1 -outfmt 6 \
-query xaz > xaz.blastx &
blastx -db uniprot_sprot.fasta -max_target_seqs 1 -evalue 1e-10 -num_threads 1 -outfmt 6 \
-query xba > xba.blastx &
blastx -db uniprot_sprot.fasta -max_target_seqs 1 -evalue 1e-10 -num_threads 1 -outfmt 6 \
-query xbb > xbb.blastx &
blastx -db uniprot_sprot.fasta -max_target_seqs 1 -evalue 1e-10 -num_threads 1 -outfmt 6 \
-query xbc > xbc.blastx &
blastx -db uniprot_sprot.fasta -max_target_seqs 1 -evalue 1e-10 -num_threads 1 -outfmt 6 \
-query xbd > xbd.blastx &
blastx -db uniprot_sprot.fasta -max_target_seqs 1 -evalue 1e-10 -num_threads 1 -outfmt 6 \
-query xbe > xbe.blastx &
blastx -db uniprot_sprot.fasta -max_target_seqs 1 -evalue 1e-10 -num_threads 1 -outfmt 6 \
-query xbf > xbf.blastx &
blastx -db uniprot_sprot.fasta -max_target_seqs 1 -evalue 1e-10 -num_threads 1 -outfmt 6 \
-query xbg > xbg.blastx &

cat x*blastx > Montastrea.trinity.v2.blastx

```

venn diagram
--

```

cd /mnt/mc/quant/

~/salmon-0.5.1/bin/salmon index -t /mnt/mc/assembly/Montastrea.trinity.v2.fasta -i transcripts_index --type quasi -k 31

~/salmon-0.5.1/bin/salmon quant -p 4 -i transcripts_index -l MSR \
-1 <(gzip -cd ../reads/Thomas_McOr*_R1.PF.cor.fq.gz) \
-2 <(gzip -cd ../reads/Thomas_McOr*_R2.PF.cor.fq.gz) -o salmon_McOr

~/salmon-0.5.1/bin/salmon quant -p 4 -i transcripts_index -l MSR \
-1 <(gzip -cd ../reads/Thomas_McBr*_R1.PF.cor.fq.gz) \
-2 <(gzip -cd ../reads/Thomas_McBr*_R2.PF.cor.fq.gz) -o salmon_McBr


paste salmon_McBr/quant.sf salmon_McOr/quant.sf | awk '{print $1 "\t" $3 "\t" $7}' > salmon.McBr.McOr.venn.list

cat salmon.McBr.McOr.venn.list | awk '$2 != 0' | awk '$3 != 0' | wc -l
expressed in both = 169519

cat salmon.McBr.McOr.venn.list | awk '$2 != 0' | awk '$3 == 0' | wc -l
expressed just in orange=3559

cat salmon.McBr.McOr.venn.list | awk '$2 == 0' | awk '$3 != 0' | wc -l
expressed just in brown=4857

cat salmon.McBr.McOr.venn.list | awk '$2 != 0' | awk '$3 != 0' | awk '{print $1}' | sed 1d > expressed.in.BROR.list
cat salmon.McBr.McOr.venn.list | awk '$2 != 0' | awk '$3 == 0' | awk '{print $1}' | sed 1d > expressed.in.justOR.list
cat salmon.McBr.McOr.venn.list | awk '$2 == 0' | awk '$3 != 0' | awk '{print $1}' | sed 1d > expressed.in.justOR.list


```































