`nano ~/Downloads/kallisto`

```
#paste in this stuff

name reads condition cl na
2329 16763373 dry 112 151
2335 98314341 wet 118 147
2336 2370219 dry 118 165
2341 41132907 wet 113 151
2345 5465209 dry 126 170
2346 6217376 dry 116 162
2352 15895311 dry 111 153
2355 71630099 wet 113 147
2925 28349068 wet 105 152
2926 22931311 wet 105 151
335 76453786 wet 112 148
336 72998180 wet 115 156
342 246516 wet 113 148
348 15694891 dry 114 155
350 15102957 dry 118 159
370 17520648 dry 120 160
373 17566491 dry 116 155
376 16642295 dry 112 152
382 10985544 dry 117 158
```


```
mkdir -p /mouse/kallisto  && cd /mouse/kallisto

#DRY

ln -s $RAID/pero_pigeons_ladybugs/2345.1.fastq.gz 2345.1.fastq.gz
ln -s $RAID/pero_pigeons_ladybugs/2345.2.fastq.gz 2345.2.fastq.gz
ln -s /mnt/data3/macmanes/pero_pigeons_ladybugs/2346.1.fastq.gz 2346.1.fastq.gz
ln -s /mnt/data3/macmanes/pero_pigeons_ladybugs/2346.2.fastq.gz 2346.2.fastq.gz
ln -s /mnt/data3/macmanes/pero_pigeons_ladybugs/2336.2.fastq.gz 2336.2.fastq.gz
ln -s /mnt/data3/macmanes/pero_pigeons_ladybugs/2336.1.fastq.gz 2336.1.fastq.gz
ln -s /mnt/data3/macmanes/NYGC_August2015/raw_data/348-Kidney_*_BC6PR5ANXX_L008_001.R1.fastq.gz 348.1.fastq.gz
ln -s /mnt/data3/macmanes/NYGC_August2015/raw_data/348-Kidney_*_BC6PR5ANXX_L008_001.R2.fastq.gz 348.2.fastq.gz
ln -s /mnt/data3/macmanes/NYGC_August2015/raw_data/373-Kidney_*_BC6PR5ANXX_L008_001.R1.fastq.gz 373.1.fastq.gz
ln -s /mnt/data3/macmanes/NYGC_August2015/raw_data/373-Kidney_*_BC6PR5ANXX_L008_001.R2.fastq.gz 373.2.fastq.gz
ln -s /mnt/data3/macmanes/NYGC_August2015/raw_data/350-Kidney_*_BC6PR5ANXX_L008_001.R1.fastq.gz 350.1.fastq.gz
ln -s /mnt/data3/macmanes/NYGC_August2015/raw_data/350-Kidney_*_BC6PR5ANXX_L008_001.R2.fastq.gz 350.2.fastq.gz
ln -s /mnt/data3/macmanes/NYGC_August2015/raw_data/370-Kidney_*_BC6PR5ANXX_L008_001.R1.fastq.gz 370.1.fastq.gz
ln -s /mnt/data3/macmanes/NYGC_August2015/raw_data/370-Kidney_*_BC6PR5ANXX_L008_001.R2.fastq.gz 370.2.fastq.gz
ln -s /mnt/data3/macmanes/NYGC_August2015/raw_data/2329-Kidney_*_BC6PR5ANXX_L008_001.R1.fastq.gz 2329.1.fastq.gz
ln -s /mnt/data3/macmanes/NYGC_August2015/raw_data/2329-Kidney_*_BC6PR5ANXX_L008_001.R2.fastq.gz 2329.2.fastq.gz
ln -s /mnt/data3/macmanes/NYGC_August2015/raw_data/382-Kidney_*_BC6PR5ANXX_L008_001.R1.fastq.gz 382.1.fastq.gz
ln -s /mnt/data3/macmanes/NYGC_August2015/raw_data/382-Kidney_*_BC6PR5ANXX_L008_001.R2.fastq.gz 382.2.fastq.gz
ln -s /mnt/data3/macmanes/NYGC_August2015/raw_data/376A-Kidney_*_BC6PR5ANXX_L008_001.R1.fastq.gz 376.1.fastq.gz
ln -s /mnt/data3/macmanes/NYGC_August2015/raw_data/376A-Kidney_*_BC6PR5ANXX_L008_001.R2.fastq.gz 376.2.fastq.gz
ln -s /mnt/data3/macmanes/NYGC_August2015/raw_data/2352-Kidney_*_BC6PR5ANXX_L008_001.R1.fastq.gz 2352.1.fastq.gz
ln -s /mnt/data3/macmanes/NYGC_August2015/raw_data/2352-Kidney_*_BC6PR5ANXX_L008_001.R2.fastq.gz 2352.2.fastq.gz

```

#WET

```
ln -s /mnt/data3/macmanes/pero_annotation/Pero2926.1.fastq.gz 2926.1.fastq.gz
ln -s /mnt/data3/macmanes/pero_annotation/Pero2926.2.fastq.gz 2926.2.fastq.gz
ln -s /mnt/data3/macmanes/pero_annotation/Pero2925.1.fastq.gz 2925.1.fastq.gz
ln -s /mnt/data3/macmanes/pero_annotation/Pero2925.2.fastq.gz 2925.2.fastq.gz
ln -s $RAID/NYGC_pero/2355K.R1.fastq.gz 2355.1.fastq.gz
ln -s $RAID/NYGC_pero/2355K.R2.fastq.gz 2355.2.fastq.gz
ln -s $RAID/NYGC_pero/2341K.R1.fastq.gz 2341.1.fastq.gz
ln -s $RAID/NYGC_pero/2341K.R2.fastq.gz 2341.2.fastq.gz
ln -s $RAID/NYGC_pero/2335K.R1.fastq.gz 2335.1.fastq.gz
ln -s $RAID/NYGC_pero/2335K.R2.fastq.gz 2335.2.fastq.gz
ln -s $RAID/NYGC_pero/342K.R1.fastq.gz 342.1.fastq.gz
ln -s $RAID/NYGC_pero/342K.R2.fastq.gz 342.2.fastq.gz
ln -s $RAID/NYGC_pero/336K.R1.fastq.gz 336.1.fastq.gz
ln -s $RAID/NYGC_pero/336K.R2.fastq.gz 336.2.fastq.gz
ln -s $RAID/NYGC_pero/335K.R1.fastq.gz 335.1.fastq.gz
ln -s $RAID/NYGC_pero/335K.R2.fastq.gz 335.2.fastq.gz

```

```

#these are not testes
#ln -s $RAID/NYGC_pero/334L.R2.fastq.gz .
#n -s $RAID/NYGC_August2015/raw_data/381-testes_ATTCCT_BC6PR5ANXX_L008_001.R{1,2}.fastq.gz .
#ln -s $RAID/NYGC_August2015/raw_data/366-testes_GTGGCC_BC6PR5ANXX_L008_001.R{1,2}.fastq.gz .
#ln -s $RAID/NYGC_August2015/raw_data/349-testes_ACTGAT_BC6PR5ANXX_L008_001.R{1,2}.fastq.gz .
#ln -s $RAID/NYGC_August2015/raw_data/3333-testes_GTTTCG_BC6PR5ANXX_L008_001.R{1,2}.fastq.gz .

```
KALLISTO

```
samples[1]=2345
samples[2]=2346
samples[3]=2336
samples[4]=348
samples[5]=373
samples[6]=350
samples[7]=370
samples[8]=2329
samples[9]=382
samples[10]=376
samples[11]=2352
samples[13]=2926
samples[14]=2925
samples[15]=2355
samples[16]=2341
samples[17]=2335
samples[18]=342
samples[19]=336
samples[12]=335




#Make the kallisto index
kallisto index -i peer_kidney kidney.final.fasta

#Now we can actually do the mapping
for i in 1 2 3 4 5 6 7 8 9 10 11 12 13 14 15 16 17 18 19
do
    sample=${samples[${i}]}
    mkdir -p results/${sample}/kallisto
    kallisto quant -i peer_kidney --threads=20 --bootstrap-samples=100 \
    --output-dir=results/${sample}/kallisto \
    ${sample}.1.fastq.gz ${sample}.2.fastq.gz
done
```
SALMON

```
samples[1]=2345
samples[2]=2346
samples[3]=2336
samples[4]=348
samples[5]=373
samples[6]=350
samples[7]=370
samples[8]=2329
samples[9]=382
samples[10]=376
samples[11]=2352
samples[13]=2926
samples[14]=2925
samples[15]=2355
samples[16]=2341
samples[17]=2335
samples[18]=342
samples[19]=336
samples[12]=335




#Make the kallisto index
salmon index --index salmon_kidney --transcripts /mnt/data3/macmanes/reference_assemblies/eremicus/transcriptome/Pero.BLTK.fasta --type quasi --threads 20

#Now we can actually do the mapping
for i in 1 2 3 4 5 6 7 8 9 10 11 12 13 14 15 16 17 18 19
do
    sample=${samples[${i}]}
    mkdir -p results/${sample}/salmon
    salmon quant -i salmon_kidney --threads 20  \
    --libType ISR -o results/${sample}/salmon \
    -1 <(gzip -cd ../${sample}.1.fastq.gz) -2 <(gzip -cd ../${sample}.2.fastq.gz)
done

```

SLEUTH
```


#to Launch into RStudio
source("http://bioconductor.org/biocLite.R")
biocLite("rhdf5")
biocLite("biomaRt")
install.packages('devtools')
devtools::install_github('pachterlab/sleuth')
library("sleuth")

#Change project dir in R

base_dir <- "/Users/macmanes/Desktop/kallisto"
sample_id <- dir(file.path(base_dir,"results"))
kal_dirs <- sapply(sample_id, function(id) file.path(base_dir, "results", id, "kallisto"))
s2c <- read.table(file.path(base_dir,"3info"), header = TRUE, stringsAsFactors=FALSE)
s2c <- dplyr::select(s2c, sample = name, reads, condition, cl, na)
s2c <- dplyr::mutate(s2c, path = kal_dirs)
so <- sleuth_prep(s2c, ~ condition)


so <- sleuth_fit(so)
so <- sleuth_wt(so, 'conditionwet')


mart <- biomaRt::useMart(biomart = "ensembl", dataset = "dmelanogaster_gene_ensembl")
t2g <- biomaRt::getBM(attributes = c("ensembl_transcript_id", "ensembl_gene_id",
    "external_gene_name"), mart = mart)
t2g <- dplyr::rename(t2g, target_id = ensembl_transcript_id,
     ens_gene = ensembl_gene_id, ext_gene = external_gene_name)
so <- sleuth_prep(kal_dirs, s2c, ~ wt, target_mapping = t2g)
so <- sleuth_fit(so)
so <- sleuth_test(so, which_beta = 'wtyes')
sleuth_live(so)

```


```
source("http://bioconductor.org/biocLite.R")  
biocLite("edgeR")  
library(edgeR)  
library("edgeR")


base_dir <- "/Users/macmanes/Desktop/salmon"

files <- c("/Users/macmanes/Desktop/salmon/2329.counts",
           "/Users/macmanes/Desktop/salmon/2336.counts",
           "/Users/macmanes/Desktop/salmon/2345.counts",
           "/Users/macmanes/Desktop/salmon/2346.counts",
           "/Users/macmanes/Desktop/salmon/2352.counts",
           "/Users/macmanes/Desktop/salmon/348.counts",
           "/Users/macmanes/Desktop/salmon/350.counts",
           "/Users/macmanes/Desktop/salmon/370.counts",
           "/Users/macmanes/Desktop/salmon/373.counts",
           "/Users/macmanes/Desktop/salmon/376.counts",
           "/Users/macmanes/Desktop/salmon/382.counts",    
           "/Users/macmanes/Desktop/salmon/2341.counts",
           "/Users/macmanes/Desktop/salmon/2335.counts",           
           "/Users/macmanes/Desktop/salmon/2925.counts",
           "/Users/macmanes/Desktop/salmon/2355.counts",
           "/Users/macmanes/Desktop/salmon/336.counts",
           "/Users/macmanes/Desktop/salmon/335.counts",
           "/Users/macmanes/Desktop/salmon/2926.counts"
)

labels=c("2329","2336","2345","2346","2952","348","350","370","373","376","382",
          "2341","2335","2925","2355","336","335","2926")


data <- readDGE(files)

print(data)
head(data$counts)

###

group <- c(rep("dry",11), rep("wet",7))

dge = DGEList(counts=data, group=group)
dge <- estimateCommonDisp(dge)
dge <- estimateTagwiseDisp(dge)

# make an MA-plot of 0 vs 6 hour

et <- exactTest(dge, pair=c("wet", "dry"))
summary(dge <- decideTestsDGE(et, p=0.05, adjust="BH"))
etp <- topTags(et, n=100000)
etp$table$logFC = -etp$table$logFC

plot(
  etp$table$logCPM,
  etp$table$logFC,
  xlim=c(-3, 20), ylim=c(-12, 12), pch=20, cex=.3,
  col = ifelse( etp$table$FDR < .2, "red", "black" ) )

# plot MDS
plotMDS(dge, labels=labels)

# output CSV for 0-6 hr
write.csv(etp$table, "nema-edgeR-0v6.csv")
```
































































