deciphering Cufflinks > transcript

for instance

	genemark-Contig13156-processed-gene-0.8 is in the Cuffdiff sig list.

in teh genemark protien fasta file:


    >genemark-Contig13156-abinit-gene-0.1-mRNA-1 protein
    >genemark-Contig13156-abinit-gene-0.2-mRNA-1 protein
    >genemark-Contig13156-abinit-gene-0.3-mRNA-1 protein
    >genemark-Contig13156-abinit-gene-0.4-mRNA-1 protein
    >genemark-Contig13156-abinit-gene-0.5-mRNA-1 protein
    >genemark-Contig13156-abinit-gene-0.6-mRNA-1 protein
    >genemark-Contig13156-abinit-gene-0.7-mRNA-1 protein
    >genemark-Contig13156-abinit-gene-0.8-mRNA-1 protein
    >genemark-Contig13156-abinit-gene-0.9-mRNA-1 protein
    >genemark-Contig13156-abinit-gene-0.10-mRNA-1 protein
    >genemark-Contig13156-abinit-gene-0.11-mRNA-1 protein
    >genemark-Contig13156-abinit-gene-0.12-mRNA-1 protein
    >genemark-Contig13156-abinit-gene-0.13-mRNA-1 protein
    >genemark-Contig13156-abinit-gene-0.14-mRNA-1 protein
    >genemark-Contig13156-abinit-gene-0.15-mRNA-1 protein
    >genemark-Contig13156-abinit-gene-0.16-mRNA-1 protein
    >genemark-Contig13156-abinit-gene-0.17-mRNA-1 protein
    >genemark-Contig13156-abinit-gene-0.18-mRNA-1 protein
    >genemark-Contig13156-abinit-gene-0.19-mRNA-1 protein
    >genemark-Contig13156-abinit-gene-0.20-mRNA-1 protein
    >genemark-Contig13156-abinit-gene-0.21-mRNA-1 protein
    >genemark-Contig13156-abinit-gene-0.22-mRNA-1 protein
    >genemark-Contig13156-abinit-gene-0.23-mRNA-1 protein
    >genemark-Contig13156-abinit-gene-0.24-mRNA-1 protein
    >genemark-Contig13156-abinit-gene-0.25-mRNA-1 protein
    >genemark-Contig13156-abinit-gene-0.26-mRNA-1 protein
    >genemark-Contig13156-abinit-gene-0.27-mRNA-1 protein
    >genemark-Contig13156-abinit-gene-0.28-mRNA-1 protein	
Which one is the significant one?



	cat sig.cuffdiff | awk '{print $1}' > list
	sed -i 's_processed_abinit_g' list
	for i in `cat list`; do grep --no-group-separator --max-count=1 -A1 $i maker.final.pep >> sig.expression.fasta; done
	makeblastdb -dbtype prot -in protein.fa -out pema_prot
	

	blastp -query sig.expression.fasta -db pema_prot -evalue 1e-06 \
	-num_threads 15 -max_target_seqs 1 \
	-outfmt "6 qseqid evalue stitle" > sig.hist.blast &
	
	

Just 

	cat sig.cuffdiff | awk '0>$10{next}1'  > high.in.dry.cuffdiff
	cat high.in.dry.cuffdiff | awk '{print $1}' > list
	for i in `cat list`; do grep --no-group-separator --max-count=1 -A1 $i maker.final.pep >> sig.high.in.dry.fasta; done