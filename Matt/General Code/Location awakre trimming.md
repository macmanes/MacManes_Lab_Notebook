Location aware trimming paper
--

Running `trimming.mk` for 10M dataset

>this runs the location aware kmer trimming, trinity assembly, pslx and TransDecoder analysis.

>One important issue is that the versions for many of these thinges (e..g TRinity) has ahcnged substantially

This is the code for generating the error plot in Fig 1 in Frontiers paper.

	for i in `ls *pslx`;do echo $i; cat $i | sed 1,5d | awk '{print $1 "\t" $2 "\t" $10 	"\t" $14 "\t" (1-(($11-$1)/$11))}' | sort -rnk5 | awk '.9>$5{next}1'  | awk '{sumnt	+=$1; sum+=$2} END { print "Sum = ",sum; print "align. size = ",sumnt/1000000;print 	"Num. error per Mb aligned = ",sum/(sumnt/1000000)}'; done