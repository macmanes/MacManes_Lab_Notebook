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
	
SEECER

	gzip -d *gz
	run_seecer.sh -t . -k 31 imitator.1.fq imitator.2.fq