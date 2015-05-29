imitator
--

tadpole sequences in `/mnt/data3/macmanes/131011_HS1A_tadpole`

	tadpole_10_1.fq.gz
	tadpole_10_2.fq.gz
	tadpole_14_1.fq.gz
	tadpole_14_2.fq.gz	
	tadpole_15_1.fq.gz
	tadpole_15_2.fq.gz
	tadpole16_1.fq.gz
	tadpole16_2.fq.gz
	tadpole1_1.fq.gz
	tadpole1_2.fq.gz	
	tadpole2_1.fq.gz
	tadpole2_2.fq.gz
	tadpole3_1.fq.gz
	tadpole3_2.fq.gz
	tadpole4_1.fq.gz
	tadpole4_2.fq.gz
	tadpole8_1.fq.gz
	tadpole8_2.fq.gz
	tadpole9_1.fq.gz
	tadpole9_2.fq.gz

skin patches in `/mnt/data3/macmanes/121201_HS3B_imitator`

	frog.1.fq.gz
	frog.2.fq.gz
	
cat in `$RAID/imitator/May2015`

	cat /mnt/data3/macmanes/121201_HS3B_imitator/frog.1.fq.gz $RAID/131011_HS1A_tadpole/*1.fq.gz > imitator.1.fq
	cat /mnt/data3/macmanes/121201_HS3B_imitator/frog.2.fq.gz $RAID/131011_HS1A_tadpole/*2.fq.gz > imitator.2.fq
	
SEECER version .13. 430Gb RAM

	gzip -d *gz
	run_seecer.sh -t . -k 31 imitator.1.fq imitator.2.fq
	
trimmomatic Q=5 threshold

	Input Read Pairs: 452798245 Both Surviving: 399574128 (88.25%) Forward Only Surviving: 19697549 (4.35%) Reverse Only Surviving: 15097734 (3.33%) Dropped: 18428834 (4.07%)

Trinity v 2.0.6

    Trinity --seqType fq --max_memory 150G --inchworm_cpu 10 \
    --trimmomatic \
    --left imitator.1.fq \
    --right imitator.2.fq \
    --CPU 30 --output seecer_trinity --group_pairs_distance 999 \
    --bypass_java_version_check

TRANSRATE

    /share/transrate-1.0.0.beta3-linux-x86_64/transrate \
    -a ../seecer_trinity/Trinity.fa \
    -r Xenopus_tropicalis.JGI_4.2.pep.all.fa \
    -l  ../seecer_trinity/imitator.1.trim.fq \
    -i  ../seecer_trinity/imitator.2.trim.fq \
    -o seecer_trin_transrate -t 30


KALLISTO

	kallisto quant -i imitator -o CH1_week5 --plaintext \
	/mnt/data3/macmanes/131011_HS1A_tadpole/tadpole_10_1.fq.gz \
	/mnt/data3/macmanes/131011_HS1A_tadpole/tadpole_10_2.fq.gz
	
	kallisto quant -i imitator -o CH3_week2 --plaintext \
	/mnt/data3/macmanes/131011_HS1A_tadpole/tadpole_14_1.fq.gz \
	/mnt/data3/macmanes/131011_HS1A_tadpole/tadpole_14_2.fq.gz
	
	kallisto quant -i imitator -o CH3_week4 --plaintext \
	/mnt/data3/macmanes/131011_HS1A_tadpole/tadpole_15_1.fq.gz \
	/mnt/data3/macmanes/131011_HS1A_tadpole/tadpole_15_2.fq.gz
	
	kallisto quant -i imitator -o CH3_week5 --plaintext \
	/mnt/data3/macmanes/131011_HS1A_tadpole/tadpole16_1.fq.gz \
	/mnt/data3/macmanes/131011_HS1A_tadpole/tadpole16_2.fq.gz
	
	kallisto quant -i imitator -o CH2_week1 --plaintext \
	/mnt/data3/macmanes/131011_HS1A_tadpole/tadpole1_1.fq.gz \
	/mnt/data3/macmanes/131011_HS1A_tadpole/tadpole1_2.fq.gz
	
	kallisto quant -i imitator -o CH2_week2 --plaintext \
	/mnt/data3/macmanes/131011_HS1A_tadpole/tadpole2_1.fq.gz \
	/mnt/data3/macmanes/131011_HS1A_tadpole/tadpole2_2.fq.gz
	
	kallisto quant -i imitator -o CH2_week4 --plaintext \
	/mnt/data3/macmanes/131011_HS1A_tadpole/tadpole3_1.fq.gz \
	/mnt/data3/macmanes/131011_HS1A_tadpole/tadpole3_2.fq.gz
	
	kallisto quant -i imitator -o CH2_week5 --plaintext \
	/mnt/data3/macmanes/131011_HS1A_tadpole/tadpole4_1.fq.gz \
	/mnt/data3/macmanes/131011_HS1A_tadpole/tadpole4_2.fq.gz
	
	kallisto quant -i imitator -o CH1_week2 --plaintext \
	/mnt/data3/macmanes/131011_HS1A_tadpole/tadpole8_1.fq.gz \
	/mnt/data3/macmanes/131011_HS1A_tadpole/tadpole8_2.fq.gz
	
	kallisto quant -i imitator -o CH1_week4 --plaintext \
	/mnt/data3/macmanes/131011_HS1A_tadpole/tadpole9_1.fq.gz \
	/mnt/data3/macmanes/131011_HS1A_tadpole/tadpole9_2.fq.gz
	
	kallisto quant -i imitator -o rear_legs --plaintext \
	/mnt/data3/macmanes/121201_HS3B_imitator/MBE-MDM-89_T4.1.fq.gz \
	/mnt/data3/macmanes/121201_HS3B_imitator/MBE-MDM-89_T4.2.fq.gz
	
	kallisto quant -i imitator -o chin --plaintext \
	/mnt/data3/macmanes/121201_HS3B_imitator/MBE-MDM-89_T1.1.fq.gz \
	/mnt/data3/macmanes/121201_HS3B_imitator/MBE-MDM-89_T1.2.fq.gz
	
	kallisto quant -i imitator -o nape --plaintext \
	/mnt/data3/macmanes/121201_HS3B_imitator/MBE-MDM-89_T2.1.fq.gz \
	/mnt/data3/macmanes/121201_HS3B_imitator/MBE-MDM-89_T2.2.fq.gz
	
	kallisto quant -i imitator -o dorsal_post --plaintext \
	/mnt/data3/macmanes/121201_HS3B_imitator/MBE-MDM-89_T3.1.fq.gz \
	/mnt/data3/macmanes/121201_HS3B_imitator/MBE-MDM-89_T3.2.fq.gz
	
	kallisto quant -i imitator -o brain --plaintext \
	/mnt/data3/macmanes/121201_HS3B_imitator/MBE-MDM-89_T5.1.fq.gz \
	/mnt/data3/macmanes/121201_HS3B_imitator/MBE-MDM-89_T5.2.fq.gz

sort


    cat CH1_week2/abundance.txt | sort -k1 | cut -f1 > 0.txt  
    cat CH1_week2/abundance.txt | sort -k1 | cut -f4 > 1.txt  
    cat CH1_week4/abundance.txt | sort -k1 | cut -f4 > 2.txt  
    cat CH2_week1/abundance.txt | sort -k1 | cut -f4 > 3.txt  
    cat CH2_week2/abundance.txt | sort -k1 | cut -f4 > 4.txt  
    cat CH2_week4/abundance.txt | sort -k1 | cut -f4 > 5.txt  
    cat CH2_week5/abundance.txt | sort -k1 | cut -f4 > 6.txt  
    cat CH3_week2/abundance.txt | sort -k1 | cut -f4 > 8.txt  
    cat CH3_week4/abundance.txt | sort -k1 | cut -f4 > 9.txt  
    cat CH3_week5/abundance.txt | sort -k1 | cut -f4 > 10.txt  
    cat brain/abundance.txt | sort -k1 | cut -f4 > 11.txt  
    cat nape/abundance.txt | sort -k1 | cut -f4 > 12.txt  
    cat chin/abundance.txt | sort -k1 | cut -f4 > 13.txt  
    cat rear_legs/abundance.txt | sort -k1 | cut -f4 > 14.txt  
    cat dorsal_post/abundance.txt | sort -k1 | cut -f4 > 15.txt  


   
	paste 0.txt 1.txt 2.txt 3.txt 4.txt 5.txt \
	6.txt 8.txt 9.txt 10.txt 11.txt 12.txt 13.txt 14.txt 15.txt > imi.counts.txt
	
	sed -i '1d' imi.counts.txt
    
    cat imi.counts.txt | awk '{print $1 "\t" int($2+0.5) "\t" int($3+0.5) "\t" int($4+0.5) "\t" int($5+0.5) "\t" int($6+0.5) "\t" int($7+0.5) "\t" int($8+0.5) "\t" int($9+0.5) "\t" int($10+0.5) "\t" int($11+0.5) "\t" int($12+0.5) "\t" int($13+0.5) "\t" int($14+0.5) "\t" int($15+0.5)} ' > imi.effcounts.txt   
    
    
    
    sed -i '1 i\names \t CH1_week2 \t CH1_week4 \t CH2_week1 \t CH2_week2 \t CH2_week4 \t CH2_week5 \t \t CH3_week2 \t CH3_week4 \t CH3_week5 \t brain \t nape \t chin \t rear_legs \t dorsal_post' imi.counts.txt
































