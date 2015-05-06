Run eXpress on STAR bams
-

June 2, 2014

in `/mnt/data3/macmanes/STAR/bam`


	for i in `ls *bam`; do F=`basename $i .bam`; express -p 20 --rf-stranded /mnt/data3/macmanes/pero_trans_assembly/pero.final.fa $i -o $F.express ; done