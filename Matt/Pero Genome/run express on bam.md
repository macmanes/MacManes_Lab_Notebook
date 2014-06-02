Run eXpress on STAR bams
-

June 2, 2014

in `/mnt/data3/macmanes/STAR/bam`


	for i in `ls *bam`; do F=`basename $i .bam`; express -p 20 --fr-stranded ../pero.genes.fa $i -o $F.express ; done