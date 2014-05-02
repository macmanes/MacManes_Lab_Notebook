
This is the code for running the training module of Augustus

	~/augustus-3.0.2/scripts/autoAug.pl --genome=jelly.out.fasta --pasa --pasapolyAhints -singleCPU --cdna=augustus.complete.cds --species=peer --utr --hints=augustus.gff3 --optrounds=2

	export PASAHOME

	~/augustus-3.0.2/scripts/autoAug.pl --genome jelly.out.fasta --species peer --hints augustus.gff3 --optrounds 2 --trainingset augustus.complete.cds --singleCPU

	macmanes@macmanes:/media/macmanes/hd3/pero-genome/augustus$ ~/augustus-3.0.2/scripts/autoAug.pl --genome jelly.out.fasta --pasa --pasapolyAhints -singleCPU --cdna augustus.complete.cds --species peer --utr --hints augustus.gff3 --optrounds 2
	
This is what I really did: (in `/media/macmanes/hd3/maker/augustus`)

	~/augustus-3.0.2/scripts/autoAug.pl --genome=../../pero-genome/jelly.out.fasta --species=peer \
	--cdna=../augustus.complete.cds --trainingset=../cegma/genome.gff3 --singleCPU -v --useexisting
	
I got an error message: `Number of training genes is with 17 too low (at least 100 genes required)! Training aborted.`

> I'll have to run maker on Blacklight a little *or maybe a lot* longer...


17 Apr 14
--
take 2 (in `/media/macmanes/hd3/maker/pero.genes.maker.output`):

	~/maker/bin/gff3_merge -d pero.genes_master_datastore_index.log
	~/maker/bin/maker2zff pero.gff
	/home/macmanes/maker/exe/snap/fathom genome.ann genome.dna -categorize 1000
	/home/macmanes/maker/exe/snap/zff2gff3.pl genome.ann | perl -plne 's/\t(\S+)$/\t\.\t$1/' > for-augustus.gff3
	
nof for the actual training (in .

	~/augustus-3.0.2/scripts/autoAug.pl --genome=../../pero-genome/jelly.out.fasta --species=peer \
	--cdna=../augustus.complete.cds --trainingset=for-augustus.gff3 --singleCPU -v --useexisting


25 Apr 14
--

I killed the last run, remade the `for-augustus.gff` file, and started with slightly different command. Specifically, I lost the --singleCPU command in hopes that this will run faster. 

	nohup ~/augustus-3.0.2/scripts/autoAug.pl --genome=../../pero-genome/jelly.out.fasta --species=peer \
	--cdna=../augustus.complete.cds --trainingset=for-augustus.gff3 --noninteractive --useexisting --optrounds=1 &
	

28 Apr 14
--

Augustus was killed, something about the `noninteractive` command. It is expecting some SGE type integration with that.  RESTARTED:

	nohup ~/augustus-3.0.2/scripts/autoAug.pl --genome=../../pero-genome/jelly.out.fasta --species=peer --cdna=../augustus.complete.cds --trainingset=for-augustus.gff3 --useexisting --optrounds=1 &
	--
	~/augustus-3.0.2/scripts/autoAug.pl --species=peer --genome=/media/macmanes/hd3/maker/pero.genes.maker.output/autoAug/seq/genome_clean.fa --useexisting --hints=/media/macmanes/hd3/maker/pero.genes.maker.output/autoAug/hints/hints.E.gff  -v -v  --index=1
	--
	~/augustus-3.0.2/scripts/autoAug.pl --species=peer --genome=/media/macmanes/hd3/maker/pero.genes.maker.output/autoAug/seq/genome_clean.fa --useexisting --hints=/media/macmanes/hd3/maker/pero.genes.maker.output/autoAug/hints/hints.E.gff --estali=your.cdna.psl -v -v -v  --index=2
	--
	2 The shell scripts for cluster have been prepared under /media/macmanes/hd3/maker/pero.genes.maker.output/autoAug/autoAugPred_hints/shells
	Please start the augustus jobs /media/macmanes/hd3/maker/pero.genes.maker.output/autoAug/autoAugPred_hints/shells/aug* manually now.
	Either by running them sequentially on a single PC or by submitting these jobs to a compute cluster. When the jobs are done, simply rerun your original 	command with --useexisting

_____
	/home/macmanes/augustus-3.0.2/config//../src/augustus --UTR=off --hintsfile=../../hints/hints.gff \
	--extrinsicCfgFile=/home/macmanes/augustus-3.0.2/config/extrinsic/extrinsic.E.cfg \
	--AUGUSTUS_CONFIG_PATH=/home/macmanes/augustus-3.0.2/config/ --exonnames=on --species=peer \
	/media/macmanes/hd3/maker/pero.genes.maker.output/autoAug/seq/split/genome_clean.split.1.fa \
	> /media/macmanes/hd3/maker/pero.genes.maker.output/autoAug/autoAugPred_hints/shells/aug1.out &
	
_______________________

	/home/macmanes/augustus-3.0.2/config//../src/augustus --UTR=off --hintsfile=../../hints/hints.gff \
	--extrinsicCfgFile=/home/macmanes/augustus-3.0.2/config/extrinsic/extrinsic.E.cfg \
	--AUGUSTUS_CONFIG_PATH=/home/macmanes/augustus-3.0.2/config/ --exonnames=on --species=peer \
	/media/macmanes/hd3/maker/pero.genes.maker.output/autoAug/seq/split/genome_clean.split.2.fa > \
	/media/macmanes/hd3/maker/pero.genes.maker.output/autoAug/autoAugPred_hints/shells/aug2.out &

_______________________

	/home/macmanes/augustus-3.0.2/config//../src/augustus --UTR=off --hintsfile=../../hints/hints.gff \
	--extrinsicCfgFile=/home/macmanes/augustus-3.0.2/config/extrinsic/extrinsic.E.cfg \
	--AUGUSTUS_CONFIG_PATH=/home/macmanes/augustus-3.0.2/config/ --exonnames=on --species=peer \
	/media/macmanes/hd3/maker/pero.genes.maker.output/autoAug/seq/split/genome_clean.split.3.fa > \
	/media/macmanes/hd3/maker/pero.genes.maker.output/autoAug/autoAugPred_hints/shells/aug3.out &


_______________________

	/home/macmanes/augustus-3.0.2/config//../src/augustus --UTR=off --hintsfile=../../hints/hints.gff \
	--extrinsicCfgFile=/home/macmanes/augustus-3.0.2/config/extrinsic/extrinsic.E.cfg \
	--AUGUSTUS_CONFIG_PATH=/home/macmanes/augustus-3.0.2/config/ --exonnames=on --species=peer \
	/media/macmanes/hd3/maker/pero.genes.maker.output/autoAug/seq/split/genome_clean.split.4.fa > \
	/media/macmanes/hd3/maker/pero.genes.maker.output/autoAug/autoAugPred_hints/shells/aug4.out &

_______________________

	/home/macmanes/augustus-3.0.2/config//../src/augustus --UTR=off --hintsfile=../../hints/hints.gff \
	--extrinsicCfgFile=/home/macmanes/augustus-3.0.2/config/extrinsic/extrinsic.E.cfg \
	--AUGUSTUS_CONFIG_PATH=/home/macmanes/augustus-3.0.2/config/ --exonnames=on --species=peer \
	/media/macmanes/hd3/maker/pero.genes.maker.output/autoAug/seq/split/genome_clean.split.5.fa > \
	/media/macmanes/hd3/maker/pero.genes.maker.output/autoAug/autoAugPred_hints/shells/aug5.out &

_______________________

	/home/macmanes/augustus-3.0.2/config//../src/augustus --UTR=off --hintsfile=../../hints/hints.gff \
	--extrinsicCfgFile=/home/macmanes/augustus-3.0.2/config/extrinsic/extrinsic.E.cfg \
	--AUGUSTUS_CONFIG_PATH=/home/macmanes/augustus-3.0.2/config/ --exonnames=on --species=peer \
	/media/macmanes/hd3/maker/pero.genes.maker.output/autoAug/seq/split/genome_clean.split.6.fa > \
	/media/macmanes/hd3/maker/pero.genes.maker.output/autoAug/autoAugPred_hints/shells/aug6.out &


_______________________

	/home/macmanes/augustus-3.0.2/config//../src/augustus --UTR=off --hintsfile=../../hints/hints.gff \
	--extrinsicCfgFile=/home/macmanes/augustus-3.0.2/config/extrinsic/extrinsic.E.cfg \
	--AUGUSTUS_CONFIG_PATH=/home/macmanes/augustus-3.0.2/config/ --exonnames=on --species=peer \
	/media/macmanes/hd3/maker/pero.genes.maker.output/autoAug/seq/split/genome_clean.split.7.fa > \
	/media/macmanes/hd3/maker/pero.genes.maker.output/autoAug/autoAugPred_hints/shells/aug7.out &

these 4 above might be suspect..
--

_______________________

	/home/macmanes/augustus-3.0.2/config//../src/augustus --UTR=off --hintsfile=../../hints/hints.gff \
	--extrinsicCfgFile=/home/macmanes/augustus-3.0.2/config/extrinsic/extrinsic.E.cfg \
	--AUGUSTUS_CONFIG_PATH=/home/macmanes/augustus-3.0.2/config/ --exonnames=on --species=peer \
	/media/macmanes/hd3/maker/pero.genes.maker.output/autoAug/seq/split/genome_clean.split.8.fa > \
	/media/macmanes/hd3/maker/pero.genes.maker.output/autoAug/autoAugPred_hints/shells/aug8.out &

_______________________

	/home/macmanes/augustus-3.0.2/config//../src/augustus --UTR=off --hintsfile=../../hints/hints.gff \
	--extrinsicCfgFile=/home/macmanes/augustus-3.0.2/config/extrinsic/extrinsic.E.cfg \
	--AUGUSTUS_CONFIG_PATH=/home/macmanes/augustus-3.0.2/config/ --exonnames=on --species=peer \
	/media/macmanes/hd3/maker/pero.genes.maker.output/autoAug/seq/split/genome_clean.split.9.fa > \
	/media/macmanes/hd3/maker/pero.genes.maker.output/autoAug/autoAugPred_hints/shells/aug9.out &


_______________________

	/home/macmanes/augustus-3.0.2/config//../src/augustus --UTR=off --hintsfile=../../hints/hints.gff \
	--extrinsicCfgFile=/home/macmanes/augustus-3.0.2/config/extrinsic/extrinsic.E.cfg \
	--AUGUSTUS_CONFIG_PATH=/home/macmanes/augustus-3.0.2/config/ --exonnames=on --species=peer \
	/media/macmanes/hd3/maker/pero.genes.maker.output/autoAug/seq/split/genome_clean.split.10.fa > \
	/media/macmanes/hd3/maker/pero.genes.maker.output/autoAug/autoAugPred_hints/shells/aug10.out &


_______________________

	/home/macmanes/augustus-3.0.2/config//../src/augustus --UTR=off --hintsfile=../../hints/hints.gff \
	--extrinsicCfgFile=/home/macmanes/augustus-3.0.2/config/extrinsic/extrinsic.E.cfg \
	--AUGUSTUS_CONFIG_PATH=/home/macmanes/augustus-3.0.2/config/ --exonnames=on --species=peer \
	/media/macmanes/hd3/maker/pero.genes.maker.output/autoAug/seq/split/genome_clean.split.11.fa > \
	/media/macmanes/hd3/maker/pero.genes.maker.output/autoAug/autoAugPred_hints/shells/aug11.out &

_______________________

	/home/macmanes/augustus-3.0.2/config//../src/augustus --UTR=off --hintsfile=../../hints/hints.gff \
	--extrinsicCfgFile=/home/macmanes/augustus-3.0.2/config/extrinsic/extrinsic.E.cfg \
	--AUGUSTUS_CONFIG_PATH=/home/macmanes/augustus-3.0.2/config/ --exonnames=on --species=peer \
	/media/macmanes/hd3/maker/pero.genes.maker.output/autoAug/seq/split/genome_clean.split.12.fa > \
	/media/macmanes/hd3/maker/pero.genes.maker.output/autoAug/autoAugPred_hints/shells/aug12.out &

_______________________

	/home/macmanes/augustus-3.0.2/config//../src/augustus --UTR=off --hintsfile=../../hints/hints.gff \
	--extrinsicCfgFile=/home/macmanes/augustus-3.0.2/config/extrinsic/extrinsic.E.cfg \
	--AUGUSTUS_CONFIG_PATH=/home/macmanes/augustus-3.0.2/config/ --exonnames=on --species=peer \
	/media/macmanes/hd3/maker/pero.genes.maker.output/autoAug/seq/split/genome_clean.split.13.fa > \
	/media/macmanes/hd3/maker/pero.genes.maker.output/autoAug/autoAugPred_hints/shells/aug13.out &

_______________________

	/home/macmanes/augustus-3.0.2/config//../src/augustus --UTR=off --hintsfile=../../hints/hints.gff \
	--extrinsicCfgFile=/home/macmanes/augustus-3.0.2/config/extrinsic/extrinsic.E.cfg \
	--AUGUSTUS_CONFIG_PATH=/home/macmanes/augustus-3.0.2/config/ --exonnames=on --species=peer \
	/media/macmanes/hd3/maker/pero.genes.maker.output/autoAug/seq/split/genome_clean.split.14.fa > \
	/media/macmanes/hd3/maker/pero.genes.maker.output/autoAug/autoAugPred_hints/shells/aug14.out &

_______________________

	/home/macmanes/augustus-3.0.2/config//../src/augustus --UTR=off --hintsfile=../../hints/hints.gff \
	--extrinsicCfgFile=/home/macmanes/augustus-3.0.2/config/extrinsic/extrinsic.E.cfg \
	--AUGUSTUS_CONFIG_PATH=/home/macmanes/augustus-3.0.2/config/ --exonnames=on --species=peer \
	/media/macmanes/hd3/maker/pero.genes.maker.output/autoAug/seq/split/genome_clean.split.15.fa > \
	/media/macmanes/hd3/maker/pero.genes.maker.output/autoAug/autoAugPred_hints/shells/aug15.out &



done to here
--

_______________________

_______________________

	/home/macmanes/augustus-3.0.2/config//../src/augustus --UTR=off --hintsfile=../../hints/hints.gff \
	--extrinsicCfgFile=/home/macmanes/augustus-3.0.2/config/extrinsic/extrinsic.E.cfg \
	--AUGUSTUS_CONFIG_PATH=/home/macmanes/augustus-3.0.2/config/ --exonnames=on --species=peer \
	/media/macmanes/hd3/maker/pero.genes.maker.output/autoAug/seq/split/genome_clean.split.16.fa > \
	/media/macmanes/hd3/maker/pero.genes.maker.output/autoAug/autoAugPred_hints/shells/aug16.out &

_______________________

	/home/macmanes/augustus-3.0.2/config//../src/augustus --UTR=off --hintsfile=../../hints/hints.gff \
	--extrinsicCfgFile=/home/macmanes/augustus-3.0.2/config/extrinsic/extrinsic.E.cfg \
	--AUGUSTUS_CONFIG_PATH=/home/macmanes/augustus-3.0.2/config/ --exonnames=on --species=peer \
	/media/macmanes/hd3/maker/pero.genes.maker.output/autoAug/seq/split/genome_clean.split.17.fa > \
	/media/macmanes/hd3/maker/pero.genes.maker.output/autoAug/autoAugPred_hints/shells/aug17.out &


_______________________

	/home/macmanes/augustus-3.0.2/config//../src/augustus --UTR=off --hintsfile=../../hints/hints.gff \
	--extrinsicCfgFile=/home/macmanes/augustus-3.0.2/config/extrinsic/extrinsic.E.cfg \
	--AUGUSTUS_CONFIG_PATH=/home/macmanes/augustus-3.0.2/config/ --exonnames=on --species=peer \
	/media/macmanes/hd3/maker/pero.genes.maker.output/autoAug/seq/split/genome_clean.split.18.fa > \
	/media/macmanes/hd3/maker/pero.genes.maker.output/autoAug/autoAugPred_hints/shells/aug18.out &


_______________________

	/home/macmanes/augustus-3.0.2/config//../src/augustus --UTR=off --hintsfile=../../hints/hints.gff \
	--extrinsicCfgFile=/home/macmanes/augustus-3.0.2/config/extrinsic/extrinsic.E.cfg \
	--AUGUSTUS_CONFIG_PATH=/home/macmanes/augustus-3.0.2/config/ --exonnames=on --species=peer \
	/media/macmanes/hd3/maker/pero.genes.maker.output/autoAug/seq/split/genome_clean.split.19.fa > \
	/media/macmanes/hd3/maker/pero.genes.maker.output/autoAug/autoAugPred_hints/shells/aug19.out &

_______________________

	/home/macmanes/augustus-3.0.2/config//../src/augustus --UTR=off --hintsfile=../../hints/hints.gff \
	--extrinsicCfgFile=/home/macmanes/augustus-3.0.2/config/extrinsic/extrinsic.E.cfg \
	--AUGUSTUS_CONFIG_PATH=/home/macmanes/augustus-3.0.2/config/ --exonnames=on --species=peer \
	/media/macmanes/hd3/maker/pero.genes.maker.output/autoAug/seq/split/genome_clean.split.20.fa > \
	/media/macmanes/hd3/maker/pero.genes.maker.output/autoAug/autoAugPred_hints/shells/aug20.out &






































