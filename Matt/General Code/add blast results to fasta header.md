Add blast output to fasta header:
---

in `/media/macmanes/hd3/matching`

> do blast: tabular blast output

	nohup blastn -query pero.transdecoder.cds -db nt -evalue 1e-06 \
	-num_threads 15 -max_target_seqs 1 \
	-outfmt "6 qseqid stitle" > pero.transd.blast &

-

>create formatted blast results
	
	sed -i 's_PREDICTED: __g' pero.transd.blast
	sed -i 's_Mus musculus_Mmu_g' pero.transd.blast
	sed -i 's_Microtus ochrogaster_Mior_g' pero.transd.blast
	sed -i 's_Cricetulus griseus_Crgr_g' pero.transd.blast
	sed -i 's_ _-_g' pero.transd.blast
	sed -i 's_;__g' pero.transd.blast
	sed -i 's_)__g' pero.transd.blast
	sed -i 's_(__g' pero.transd.blast
	sed -i 's_,__g' pero.transd.blast
	awk -F "\t" '{print $1 "\t" "gene="$2}' pero.transd.blast > formatted.blast
	awk '{print $1}' formatted.blast > list

>do formatting

	for i in `cat list`; do 
	var1=$(grep -w --max-count=1 ^$i formatted.blast); 
	var2=$(grep -w --max-count=1 $i pero.transdecoder.cds);
	grep -A1 -w --max-count=1 $i pero.transdecoder.cds > tmp;
	if [ ! -z "$var1" ]; then 
		sed "s_${var2}_>${var1}_g" tmp >> output1.fa
	else
		cat tmp >> output1.fa
fi
wait 
done

> maybe need -h and -w options
	