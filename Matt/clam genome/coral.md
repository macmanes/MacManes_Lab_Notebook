**CORAL WORK**
--

On BEEMO

in `/home/macmanes/coral`

downloading db
    
    wget http://comparative.reefgenomics.org/faa/Coral/Seriatopora_sp_peptides_100.final.clstr.faa
    wget http://comparative.reefgenomics.org/faa/Coral/Stylophora_pistillata_peptides_100.final.clstr.faa
    wget http://comparative.reefgenomics.org/faa/Placozoa/Trichoplax_adherens_peptides_100.final.clstr.faa
    wget http://comparative.reefgenomics.org/faa/Coral/Acropora_millepora_peptides_100.final.clstr.faa
    wget http://comparative.reefgenomics.org/faa/Cnidaria/Nematostella_vectensis_peptides_100.final.clstr.faa
    wget http://comparative.reefgenomics.org/faa/Choanozoa/Monosiga_brevicollis_peptides_100.final.clstr.faa
    wget http://comparative.reefgenomics.org/faa/Sponge/Amphimedon_queenslandica_peptides_100.final.clstr.faa
	...


install Pfam and blast 2.2.30


format faa files

	for i in $(ls *faa); do F=$(basename $i _peptides_100.final.clstr.faa); fasta_formatter -i $i -o $F.prot; done

makeblastdb

in `~/coral/blastdb`
	
make individual databases

	for i in $(ls ../prot_data/*prot); do F=$(basename $i .prot); makeblastdb -in $i -dbtype prot -title $F -out $F; done
	


CRB blast individually

	
	for i in $(ls ../../prot_data/*prot); do F=$(basename $i .prot); \
	crb-blast --query p53.fasta --target $i --threads 12 --output $F.crb; done

	old:
	#for i in $(ls ../../blastdb/*pin); do F=$(basename $i .pin); \
	#blastp -db ../../blastdb/$F -query mya.p53.aa -outfmt 6 -evalue 1e-2 -num_threads 12 \
	#-max_target_seqs 1 >> p55.blastp ; done
	

extract seqs

	for i in $(ls *crb); do awk '{print $2}' $i >> list; done
	

	for i in $(ls ../../prot_data/*prot); do grep -A1 --max-count=1 -w -f list $i >> p53.prot; done	

