harmonia
--

```
kallisto index -i transcripts2.idx ../Harmonia.v1.0.1.fasta.dammit.fasta

kallisto quant -t 32 -i transcripts2.idx -o kallisto_adult -b 100 \
../harmonia_adult.R1.fastq.gz \
../harmonia_adult.R2.fastq.gz

kallisto quant -t 32 -i transcripts2.idx -o kallisto_larva -b 100 \
../harmonia_larva.R1.fastq.gz \
../harmonia_larvae.R2.fastq.gz


salmon index -t ../Harmonia.v1.0.1.fasta.dammit.fasta -i transcripts2_index --type quasi -k 31

salmon quant -p 32 -i transcripts2_index -l MSR \
-1 <(gzip -cd ../harmonia_adult.R1.fastq.gz) \
-2 <(gzip -cd ../harmonia_adult.R2.fastq.gz) -o salmon_adult

salmon quant -p 32 -i transcripts2_index -l MSR \
-1 <(gzip -cd ../harmonia_larva.R1.fastq.gz) \
-2 <(gzip -cd ../harmonia_larvae.R2.fastq.gz) -o salmon_larva
```

pull out unique
--

```
paste salmon_adult/quant.sf salmon_larva/quant.sf | awk '{print $1 "\t" $3 "\t" $7}' > salmon.adultlarva.venn.list

cat salmon.adultlarva.venn.list | awk '$2 != 0' | awk '$3 != 0' | wc -l
expressed in both = 104273

cat salmon.adultlarva.venn.list | awk '$2 != 0' | awk '$3 == 0' | wc -l
expressed just in gill=55527

cat salmon.adultlarva.venn.list | awk '$2 == 0' | awk '$3 != 0' | wc -l
expressed just in muscle=6957
```