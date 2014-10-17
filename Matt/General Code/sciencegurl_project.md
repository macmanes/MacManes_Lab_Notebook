Sciencegurl project
--

downloaded data to `/mnt/data3/macmanes/sciencegurl/`

Selected 1 representative from each group to use in assembly. This individual was selected as it had the most reads. In total, will assembly 85M pe reads. Here are the stats on teh raw reads:

    F8.1.fq:16303993
    M8.1.fq:17295262
    NP1.1.fq:17089215
    P11.1.fq:16626352
    S7.1.fq:17270165

no normalize:

    Trinity --seqType fq \
    --JM 100G --trimmomatic \
    --bflyHeapSpaceMax 10G \
    --inchworm_cpu 10 \
    --SS_lib_type RF \
    --left F8.1.fq M8.1.fq NP1.1.fq P11.1.fq S7.1.fq \
    --right F8.2.fq M8.2.fq NP1.2.fq P11.2.fq S7.2.fq \
    --CPU 25 \
    --output sciencegurl_SS_no_norm \
    --group_pairs_distance 999 \
    --quality_trimming_params "ILLUMINACLIP:/share/trinityrnaseq_r20140717/trinity-plugins/Trimmomatic/adapters/TruSeq3-PE.fa:2:40:15 \
    LEADING:2 TRAILING:2 MINLEN:25" > sciencegurl_SS_no_norm.log

normalized    

    Trinity --seqType fq \
    --JM 100G --trimmomatic \
    --bflyHeapSpaceMax 10G \
    --inchworm_cpu 10 \
    --SS_lib_type RF \
    --normalize_reads \
    --left F8.1.fq M8.1.fq NP1.1.fq P11.1.fq S7.1.fq \
    --right F8.2.fq M8.2.fq NP1.2.fq P11.2.fq S7.2.fq \
    --CPU 32 \
    --output sciencegurl_SS_norm \
    --group_pairs_distance 999 \
    --quality_trimming_params "ILLUMINACLIP:/share/trinityrnaseq_r20140717/trinity-plugins/Trimmomatic/adapters/TruSeq3-PE.fa:2:40:15 \
    LEADING:2 TRAILING:2 MINLEN:25" > sciencegurl_SS_norm.log

Evaluate normalized assembly
--

lets do some mapping using the datasets used in the NORMALIZED assembly

    bwa mem -t20 norm  \
    /mnt/data3/macmanes/sciencegurl/reads/sciencegurl_SS_norm/F8.1.fq.P.qtrim.gz \
    /mnt/data3/macmanes/sciencegurl/reads/sciencegurl_SS_norm/F8.2.fq.P.qtrim.gz | \
    samtools view -@6 -Sub - | samtools sort -n -m3G -@8 - F8

    25638835 + 0 in total (QC-passed reads + QC-failed reads)
    0 + 0 duplicates
    25181692 + 0 mapped (98.22%:-nan%)
    25638835 + 0 paired in sequencing
    12798233 + 0 read1
    12840602 + 0 read2
    23726283 + 0 properly paired (92.54%:-nan%)
    24967396 + 0 with itself and mate mapped
    214296 + 0 singletons (0.84%:-nan%)
    1234043 + 0 with mate mapped to a different chr
    619314 + 0 with mate mapped to a different chr (mapQ>=5)

    bwa mem -t20 norm  \
    /mnt/data3/macmanes/sciencegurl/reads/sciencegurl_SS_norm/NP1.1.fq.P.qtrim.gz \
    /mnt/data3/macmanes/sciencegurl/reads/sciencegurl_SS_norm/NP1.2.fq.P.qtrim.gz | \
    samtools view -@6 -Sub - | samtools sort -n -m3G -@8 - NP1

    26835612 + 0 in total (QC-passed reads + QC-failed reads)
    0 + 0 duplicates
    26392631 + 0 mapped (98.35%:-nan%)
    26835612 + 0 paired in sequencing
    13395785 + 0 read1
    13439827 + 0 read2
    24854238 + 0 properly paired (92.62%:-nan%)
    26171268 + 0 with itself and mate mapped
    221363 + 0 singletons (0.82%:-nan%)
    1249185 + 0 with mate mapped to a different chr
    614821 + 0 with mate mapped to a different chr (mapQ>=5)
    
Now some mapping of a few datasets not used for the assembly


    java -Xmx100g -jar /share/trinityrnaseq_r20140717/trinity-plugins/Trimmomatic-0.32/trimmomatic-0.32.jar PE -threads 24 \
    -baseout F12.trim \
    F12.1.fq \
    F12.2.fq  \
    ILLUMINACLIP:/share/trinityrnaseq_r20140717/trinity-plugins/Trimmomatic/adapters/TruSeq3-PE.fa:2:40:15 LEADING:2 TRAILING:2 SLIDINGWINDOW:4:2 MINLEN:25

    bwa mem -t20 norm  \
    /mnt/data3/macmanes/sciencegurl/reads/F12.trim_1P \
    /mnt/data3/macmanes/sciencegurl/reads/F12.trim_2P | \
    samtools view -@6 -Sub - | samtools sort -n -m3G -@16 - F12
    
    19799725 + 0 in total (QC-passed reads + QC-failed reads)
    0 + 0 duplicates
    19452040 + 0 mapped (98.24%:-nan%)
    19799725 + 0 paired in sequencing
    9882751 + 0 read1
    9916974 + 0 read2
    18303504 + 0 properly paired (92.44%:-nan%)
    19295604 + 0 with itself and mate mapped
    156436 + 0 singletons (0.79%:-nan%)
    952650 + 0 with mate mapped to a different chr
    460405 + 0 with mate mapped to a different chr (mapQ>=5)
    
    
    
    java -Xmx100g -jar /share/trinityrnaseq_r20140717/trinity-plugins/Trimmomatic-0.32/trimmomatic-0.32.jar PE -threads 24 \
    -baseout P12.trim \
    P12.1.fq \
    P12.2.fq  \
    ILLUMINACLIP:/share/trinityrnaseq_r20140717/trinity-plugins/Trimmomatic/adapters/TruSeq3-PE.fa:2:40:15 LEADING:2 TRAILING:2 SLIDINGWINDOW:4:2 MINLEN:25

    bwa mem -t20 norm  \
    /mnt/data3/macmanes/sciencegurl/reads/P12.trim_1P \
    /mnt/data3/macmanes/sciencegurl/reads/P12.trim_2P | \
    samtools view -@6 -Sub - | samtools sort -n -m3G -@16 - P12
    
    21973323 + 0 in total (QC-passed reads + QC-failed reads)
    0 + 0 duplicates
    21645431 + 0 mapped (98.51%:-nan%)
    21973323 + 0 paired in sequencing
    10970815 + 0 read1
    11002508 + 0 read2
    20466743 + 0 properly paired (93.14%:-nan%)
    21492708 + 0 with itself and mate mapped
    152723 + 0 singletons (0.70%:-nan%)
    967940 + 0 with mate mapped to a different chr
    465752 + 0 with mate mapped to a different chr (mapQ>=5)
    
Eval UnNormalized assembly
--
    bwa mem -t20 no_norm  \
    /mnt/data3/macmanes/sciencegurl/reads/sciencegurl_SS_norm/F8.1.fq.P.qtrim.gz \
    /mnt/data3/macmanes/sciencegurl/reads/sciencegurl_SS_norm/F8.2.fq.P.qtrim.gz | \
    samtools view -@6 -Sub - | samtools sort -n -m3G -@16 - F8_no_norm


    25622174 + 0 in total (QC-passed reads + QC-failed reads)
    0 + 0 duplicates
    25309931 + 0 mapped (98.78%:-nan%)
    25622174 + 0 paired in sequencing
    12798605 + 0 read1
    12823569 + 0 read2
    23922693 + 0 properly paired (93.37%:-nan%)
    25133543 + 0 with itself and mate mapped
    176388 + 0 singletons (0.69%:-nan%)
    1194059 + 0 with mate mapped to a different chr
    566923 + 0 with mate mapped to a different chr (mapQ>=5)



    bwa mem -t20 no_norm  \
    /mnt/data3/macmanes/sciencegurl/reads/sciencegurl_SS_norm/NP1.1.fq.P.qtrim.gz \
    /mnt/data3/macmanes/sciencegurl/reads/sciencegurl_SS_norm/NP1.2.fq.P.qtrim.gz | \
    samtools view -@6 -Sub - | samtools sort -n -m3G -@16 - NP1_no_norm


    26810608 + 0 in total (QC-passed reads + QC-failed reads)
    0 +  0 duplicates
    26494311 + 0 mapped (98.82%:-nan%)
    26810608 + 0 paired in sequencing
    13391884 + 0 read1
    13418724 + 0 read2
    25002129 + 0 properly paired (93.25%:-nan%)
    26307641 + 0 with itself and mate mapped
    186670 + 0 singletons (0.70%:-nan%)
    1220585 + 0 with mate mapped to a different chr
    550642 + 0 with mate mapped to a different chr (mapQ>=5)

    bwa mem -t20 no_norm  \
    /mnt/data3/macmanes/sciencegurl/reads/F12.trim_1P \
    /mnt/data3/macmanes/sciencegurl/reads/F12.trim_2P | \
    samtools view -@6 -Sub - | samtools sort -n -m3G -@16 - F12_no_norm

    19789775 + 0 in total (QC-passed reads + QC-failed reads)
    0 + 0 duplicates
    19558229 + 0 mapped (98.83%:-nan%)
    19789775 + 0 paired in sequencing
    9884124 + 0 read1
    9905651 + 0 read2
    18431951 + 0 properly paired (93.14%:-nan%)
    19431082 + 0 with itself and mate mapped
    127147 + 0 singletons (0.64%:-nan%)
    947940 + 0 with mate mapped to a different chr
    430183 + 0 with mate mapped to a different chr (mapQ>=5)



    bwa mem -t20 no_norm  \
    /mnt/data3/macmanes/sciencegurl/reads/P12.trim_1P \
    /mnt/data3/macmanes/sciencegurl/reads/P12.trim_2P | \
    samtools view -@6 -Sub - | samtools sort -n -m3G -@16 - P12_no_norm

    21950071 + 0 in total (QC-passed reads + QC-failed reads)
    0 + 0 duplicates
    21737512 + 0 mapped (99.03%:-nan%)
    21950071 + 0 paired in sequencing
    10964880 + 0 read1
    10985191 + 0 read2
    20579775 + 0 properly paired (93.76%:-nan%)
    21616977 + 0 with itself and mate mapped
    120535 + 0 singletons (0.55%:-nan%)
    956358 + 0 with mate mapped to a different chr
    429010 + 0 with mate mapped to a different chr (mapQ>=5)

let's run Transdecoder
--

UnNormalized Assembly:

    macmanes@davinci:/mnt/data3/macmanes/sciencegurl/assemblies$ abyss-fac sciencegurl_no_norm.Trinity.fasta.transdecoder.pep
    n    n:500	n:N50	min	N80	N50	N20	E-size	max	sum	name
    64554	386	156	500	563	655	902	741	1454	265777	sciencegurl_no_norm.Trinity.fasta.transdecoder.pep
    macmanes@davinci:/mnt/data3/macmanes/sciencegurl/assemblies$ grep -c complete sciencegurl_no_norm.Trinity.fasta.transdecoder.pep
    35971
    macmanes@davinci:/mnt/data3/macmanes/sciencegurl/assemblies$ grep -c 5prime sciencegurl_no_norm.Trinity.fasta.transdecoder.pep
    12011
    macmanes@davinci:/mnt/data3/macmanes/sciencegurl/assemblies$ grep -c 3prime sciencegurl_no_norm.Trinity.fasta.transdecoder.pep
    8497
    macmanes@davinci:/mnt/data3/macmanes/sciencegurl/assemblies$ grep -c internal sciencegurl_no_norm.Trinity.fasta.transdecoder.pep
    8075

Normalized data
--

    n       n:500   n:N50   min     N80     N50     N20     E-size  max     sum     name
    71955   374     152     500     559     662     901     727     1434    255990  sciencegurl_norm.Trinity.fasta.transdecoder.pep
    root@davinci:/mnt/data3/macmanes/sciencegurl/assemblies# grep -c complete sciencegurl_norm.Trinity.fasta.transdecoder.pep
    39759
    root@davinci:/mnt/data3/macmanes/sciencegurl/assemblies# grep -c 5prime sciencegurl_norm.Trinity.fasta.transdecoder.pep
    14088
    root@davinci:/mnt/data3/macmanes/sciencegurl/assemblies# grep -c 3prime sciencegurl_norm.Trinity.fasta.transdecoder.pep
    9882
    root@davinci:/mnt/data3/macmanes/sciencegurl/assemblies# grep -c internal sciencegurl_norm.Trinity.fasta.transdecoder.pep
    8226

It seems like normalized assembly is better (same mapping, more complete CDS's)
--

Will do blast to identify things that are likely 'real' 

    blastn -query sciencegurl_norm.Trinity.fasta  -db fish -evalue 1e-3 -num_threads 25 -outfmt "6 qseqid sacc pident length evalue"  > fish.blast
    cat fish.blast | sort -k1 | awk '{print $1}' | uniq | wc -l
    74638
    
    sed ':begin;$!N;/[ACTGNn-]\n[ACTGNn-]/s/\n//;tbegin;P;D' sciencegurl_norm.Trinity.fasta > sciencegurl_norm.Trinity.fa
    cat fish.blast | sort -k1 | awk '{print $1}' | uniq > list2
    cat ../assemblies/sciencegurl_norm.Trinity.fasta.transdecoder.pep | grep '>' | awk -F ">" '{print $2}' | awk -F "|" '{print $1}' >> list2
    for i in `cat list2`; do  grep --max-count=1 -A1 -w $i sciencegurl_norm.Trinity.fa >> sciencegurl.reduced.fa; done &

cd-hit
--

    cd-hit-est -M 5000 -T 24 -c .97 -i sciencegurl.reduced.fa -o sciencegurl.cdhit.fa

Map to new reference to make sure we didn't lose too much

    bwa index -p cdhit sciencegurl.cdhit.fa
    
    bwa mem -t20 cdhit  \
    /mnt/data3/macmanes/sciencegurl/reads/P12.trim_1P \
    /mnt/data3/macmanes/sciencegurl/reads/P12.trim_2P | \
    samtools view -@6 -Sub - | samtools sort -n -m3G -@16 - P12_cdhit

    21871355 + 0 in total (QC-passed reads + QC-failed reads)
    0 + 0 duplicates
    20185553 + 0 mapped (92.29%:-nan%)
    21871355 + 0 paired in sequencing
    10922242 + 0 read1
    10949113 + 0 read2
    19352443 + 0 properly paired (88.48%:-nan%)
    19959608 + 0 with itself and mate mapped
    225945 + 0 singletons (1.03%:-nan%)
    541164 + 0 with mate mapped to a different chr
    261023 + 0 with mate mapped to a different chr (mapQ>=5)


    bwa mem -t20 cdhit  \
    /mnt/data3/macmanes/sciencegurl/reads/sciencegurl_SS_norm/NP1.1.fq.P.qtrim.gz \
    /mnt/data3/macmanes/sciencegurl/reads/sciencegurl_SS_norm/NP1.2.fq.P.qtrim.gz | \
    samtools view -@6 -Sub - | samtools sort -n -m3G -@16 - NP1_cdhit
    
    
    26715324 + 0 in total (QC-passed reads + QC-failed reads)
    0 + 0 duplicates
    24440539 + 0 mapped (91.49%:-nan%)
    26715324 + 0 paired in sequencing
    13339770 + 0 read1
    13375554 + 0 read2
    23311897 + 0 properly paired (87.26%:-nan%)
    24122080 + 0 with itself and mate mapped
    318459 + 0 singletons (1.19%:-nan%)
    737237 + 0 with mate mapped to a different chr
    366323 + 0 with mate mapped to a different chr (mapQ>=5)
    
    
so we lose some mapped reads, <5%, but this is not surprising and is within the realm of expected. 
--

I sent the *.pep *cds and *.fa file. 
