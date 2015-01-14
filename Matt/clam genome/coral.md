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

see: https://github.com/macmanes-lab/general/blob/master/crb_genes.sh


	cd nos
	~/coral/crb_genes.sh -t 8 -f nos.fasta -n nos
	cd ../atm
	~/coral/crb_genes.sh -t 8 -f atm.fasta -n atm
	cd ../gpx
	~/coral/crb_genes.sh -t 8 -f gpx.fasta -n gpx
	cd ../sod
	~/coral/crb_genes.sh -t 8 -f sod.fasta -n sod
	cd ../Caspase_9
	~/coral/crb_genes.sh -t 8 -f caspase9.fasta -n caspase9
	cd ../p53
	~/coral/crb_genes.sh -t 8 -f p53.fasta -n p53
	cd ../mortalin
	~/coral/crb_genes.sh -t 16 -f mortalin.fasta -n mortalin
	cd ../BIRC5
	~/coral/crb_genes.sh -t 8 -f birc5.fasta -n BIRC5
	cd ../NOXA
	~/coral/crb_genes.sh -t 8 -f noxa.fasta -n NOXA
	cd ../bcl2
	~/coral/crb_genes.sh -t 16 -f bcl2.fasta -n bcl2
	cd ../fas
	~/coral/crb_genes.sh -t 16 -f fas.fasta -n FAS
	cd ../Caspase_3
	~/coral/crb_genes.sh -t 12 -f caspase3.fasta -n caspase3
	cd ../BAX
	~/coral/crb_genes.sh -t 12 -f BAX.fasta -n BAX
	cd ../e2f1
	~/coral/crb_genes.sh -t 12 -f e2f1.fasta -n e2f1
	cd ../bclxl
	~/coral/crb_genes.sh -t 12 -f bclxl.fasta -n bclxl
	cd ../apaf1
	~/coral/crb_genes.sh -t 12 -f apaf1.fasta -n apaf1
	cd ../pig8
	~/coral/crb_genes.sh -t 12 -f pig8.fasta -n pig8
	cd ../traf6
	~/coral/crb_genes.sh -t 12 -f traf6.fasta -n traf6
	cd ../sumo2
	~/coral/crb_genes.sh -t 12 -f sumo2.fasta -n sumo2
	cd ../jab1
	~/coral/crb_genes.sh -t 12 -f jab1.fasta -n jab1
	cd ../crm1
	~/coral/crb_genes.sh -t 12 -f crm1.fasta -n crm1
	cd ../pig3
	~/coral/crb_genes.sh -t 12 -f pig3.fasta -n pig3
	cd ../cul7
	~/coral/crb_genes.sh -t 12 -f cul7.fasta -n cul7
	cd ../ddb2
	~/coral/crb_genes.sh -t 12 -f ddb2.fasta -n ddb2
	cd ../trim22
	~/coral/crb_genes.sh -t 12 -f trim22.fasta -n trim22
	cd ../ddit4
	~/coral/crb_genes.sh -t 12 -f ddit4.fasta -n ddit4
	cd ../topo2
	~/coral/crb_genes.sh -t 12 -f topo2.fasta -n topo2
	cd ../pcna
	~/coral/crb_genes.sh -t 12 -f pcna.fasta -n pcna
	cd ../mdm2
	~/coral/crb_genes.sh -t 12 -f mdm2.fasta -n mdm2
	cd ../cip1
	~/coral/crb_genes.sh -t 12 -f cip1.fasta -n cip1
	cd ../cdc25c
	~/coral/crb_genes.sh -t 12 -f cdc25c.fasta -n cdc25c

new list:

	






































