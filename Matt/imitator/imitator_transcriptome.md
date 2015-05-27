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

