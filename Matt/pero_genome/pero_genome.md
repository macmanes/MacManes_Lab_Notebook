	java -Xmx300g -jar /share/Trimmomatic-0.32/trimmomatic-0.32.jar PE \
	-threads 20 -baseout peroL1 \
	$RAID/macmanes/pero_genome/131008/pero360_L1.1.fq \
	$RAID/macmanes/pero_genome/131008/pero360_L1.2.fq \
	ILLUMINACLIP:/share/Trimmomatic-0.32/barcodes.fa:2:40:15 \
	LEADING:2 TRAILING:2 SLIDINGWINDOW:4:2 MINLEN:75
	
L1
--
Input Read Pairs: 108590493 Both Surviving: 107858557 (99.33%) Forward Only Surviving: 334901 (0.31%) Reverse Only Surviving: 314832 (0.29%) Dropped: 82203 (0.08%)
TrimmomaticPE: Completed successfully

L2
--
Input Read Pairs: 101221019 Both Surviving: 93383010 (92.26%) Forward Only Surviving: 3130088 (3.09%) Reverse Only Surviving: 293458 (0.29%) Dropped: 4414463 (4.36%)
TrimmomaticPE: Completed successfully

L3
--

Input Read Pairs: 155507411 Both Surviving: 154732344 (99.50%) Forward Only Surviving: 701490 (0.45%) Reverse Only Surviving: 6285 (0.00%) Dropped: 67292 (0.04%)
TrimmomaticPE: Completed successfully

L4
--

Input Read Pairs: 142508389 Both Surviving: 141079896 (99.00%) Forward Only Surviving: 1362383 (0.96%) Reverse Only Surviving: 2910 (0.00%) Dropped: 63200 (0.04%)
TrimmomaticPE: Completed successfully

L5
--
Input Read Pairs: 141131119 Both Surviving: 139556787 (98.88%) Forward Only Surviving: 1505745 (1.07%) Reverse Only Surviving: 2789 (0.00%) Dropped: 65798 (0.05%)
TrimmomaticPE: Completed successfully


NextClip
--
3kb - 39% usable reads
--

	nextclip -e -n 50000000 -i peer3kb.1.fq -j peer3kb.2.fq -o 3kb_trim &

--	

	grep -c @HSQ- peer3kb.1.fq
	39391766
	macmanes@davinci:/mnt/data3/macmanes/pero-mate-pair$ grep -c @HSQ- peer3kb.clipped.1.fq
	15297919


7kb
--

Hash:
 unique kmers: 54866588
 Capacity: 104857600
 Occupied: 52.32%
 Pruned: 0 (0.00%)
 Collisions:
	 tries 0: 64801542

Counting duplicates...

100%	[====================================================================================================]

SUMMARY

     Strict match parameters: 34, 18
    Relaxed match parameters: 32, 17
           Minimum read size: 25
                   Trim ends: 19

        Number of read pairs: 64910633
   Number of duplicate pairs: 9934954	15.31 %
Number of pairs containing N: 109091	0.17 %

   R1 Num reads with adaptor: 23336841	35.95 %
   R1 Num with external also: 573443	0.88 %
       R1 long adaptor reads: 16611160	25.59 %
          R1 reads too short: 6725681	10.36 %
     R1 Num reads no adaptor: 41573792	64.05 %
  R1 no adaptor but external: 3640292	5.61 %

   R2 Num reads with adaptor: 22915535	35.30 %
   R2 Num with external also: 408423	0.63 %
       R2 long adaptor reads: 16528574	25.46 %
          R2 reads too short: 6386961	9.84 %
     R2 Num reads no adaptor: 41995098	64.70 %
  R2 no adaptor but external: 291498	0.45 %

   Total pairs in category A: 3190598	4.92 %
         A pairs long enough: 2456480	3.78 %
           A pairs too short: 734118	1.13 %
A external clip in 1 or both: 14818	0.02 %

   Total pairs in category B: 19707696	30.36 %
         B pairs long enough: 13582568	20.93 %
           B pairs too short: 6125128	9.44 %
B external clip in 1 or both: 135835	0.21 %

   Total pairs in category C: 20120173	31.00 %
         C pairs long enough: 13783929	21.24 %
           C pairs too short: 6336244	9.76 %
C external clip in 1 or both: 151640	0.23 %

   Total pairs in category D: 21848855	33.66 %
         D pairs long enough: 18351068	28.27 %
           D pairs too short: 3497787	5.39 %
D external clip in 1 or both: 3563681	5.49 %

   Total pairs in category E: 43311	0.07 %
         E pairs long enough: 29733	0.05 %
           E pairs too short: 13578	0.02 %
E external clip in 1 or both: 5603	0.01 %

          Total usable pairs: 29852710	45.99 %
             All long enough: 48203778	74.26 %
    All categories too short: 16706855	25.74 %
      Duplicates not written: 0	0.00 %

         Category B became E: 17241	0.03 %
         Category C became E: 26070	0.04 %
          Overall GC content: 42.33 %