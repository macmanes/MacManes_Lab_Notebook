


	for i in *xprs
		do F=`basename $i .xprs`; 
		cat $i/results.xprs | sort -k2 | cut -f2 > header
		cat $i/results.xprs | sort -k2 | cut -f8 > $F.txt
	done
	
	paste *txt > soap.out


paste


	

	cat soap.out | awk '{print int($1+0.5) "\t" int($2+0.5) "\t" int($3+0.5) "\t" 	int($4+0.5) "\t" int($5+0.5) "\t" int($6+0.5) "\t" int($7+0.5) "\t" int($8+0.5) "\t" 	int($9+0.5) "\t" int($10+0.5) \
	"\t" int($11+0.5) "\t" int($12+0.5)}' > soap.counts.done
	
	paste header soap.counts.done > soap.counts

	cat soap.counts | sed '1 i\ names HYB_sdE3_rep1 HYB_sdE3_rep2 HYB_wt_rep1 HYB_wt_rep2 ORE_sdE3_rep1 ORE_sdE3_rep2 ORE_wt_rep1 ORE_wt_rep2 SAM_sdE3_rep1 SAM_sdE3_rep2 SAM_wt_rep1 SAM_wt_rep2' > soap.xprs.counts