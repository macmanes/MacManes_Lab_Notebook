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
	
Stuff

	grep -i "exch\|sol\|pot\|cal\|solu\|sod\|chlo\|atp\|mg\|transp" sig.in.dry.blast |  awk '{print $1}' | sort | uniq | wc -l
	35 out of 369 associated with transport in wet.
	
	30 in 225 in dry.
	
These are the genes in wet

maker-Contig10768-exonerate_est2genome-gene-0.1-mRNA-1	0.0	gi|589952299|ref|XP_006988794.1| PREDICTED: 26S proteasome non-ATPase regulatory subunit 5 [Peromyscus maniculatus bairdii]
maker-Contig11790-snap-gene-0.35-mRNA-1	7e-152	gi|589924865|ref|XP_006975306.1| PREDICTED: solute carrier family 25 member 33 [Peromyscus maniculatus bairdii]
maker-Contig12339-snap-gene-0.24-mRNA-1	3e-152	gi|589938605|ref|XP_006982052.1| PREDICTED: 26S proteasome non-ATPase regulatory subunit 8 [Peromyscus maniculatus bairdii]
maker-Contig125132-snap-gene-0.7-mRNA-1	1e-93	gi|589957086|ref|XP_006991145.1| PREDICTED: excitatory amino acid transporter 3 isoform X2 [Peromyscus maniculatus bairdii]
maker-Contig14835-snap-gene-0.49-mRNA-1	0.0	gi|589928357|ref|XP_006977001.1| PREDICTED: putative pre-mRNA-splicing factor ATP-dependent RNA helicase DHX32 isoform X1 [Peromyscus maniculatus bairdii]
maker-Contig14878-exonerate_est2genome-gene-0.1-mRNA-1	9e-128	gi|589928762|ref|XP_006977199.1| PREDICTED: magnesium transporter MRS2 homolog, mitochondrial [Peromyscus maniculatus bairdii]
maker-Contig14953-snap-gene-0.16-mRNA-1	0.0	gi|589922999|ref|XP_006974397.1| PREDICTED: sodium-coupled neutral amino acid transporter 2 [Peromyscus maniculatus bairdii]
maker-Contig14953-snap-gene-0.16-mRNA-1	3e-28	gi|589922999|ref|XP_006974397.1| PREDICTED: sodium-coupled neutral amino acid transporter 2 [Peromyscus maniculatus bairdii]
maker-Contig15896-exonerate_protein2genome-gene-0.27-mRNA-1	2e-53	gi|589932263|ref|XP_006978931.1| PREDICTED: V-type proton ATPase subunit e 1 [Peromyscus maniculatus bairdii]
maker-Contig16426-snap-gene-0.39-mRNA-1	0.0	gi|589924560|ref|XP_006975157.1| PREDICTED: sodium bicarbonate cotransporter 3 isoform X1 [Peromyscus maniculatus bairdii]
maker-Contig17155-snap-gene-0.17-mRNA-1	1e-118	gi|589923021|ref|XP_006974408.1| PREDICTED: rap guanine nucleotide exchange factor 3 [Peromyscus maniculatus bairdii]
maker-Contig17155-snap-gene-0.17-mRNA-1	3e-55	gi|589923021|ref|XP_006974408.1| PREDICTED: rap guanine nucleotide exchange factor 3 [Peromyscus maniculatus bairdii]
maker-Contig17442-exonerate_est2genome-gene-0.0-mRNA-1	0.0	gi|589955524|ref|XP_006990381.1| PREDICTED: activator of 90 kDa heat shock protein ATPase homolog 1 [Peromyscus maniculatus bairdii]
maker-Contig18342-snap-gene-0.26-mRNA-1	2e-129	gi|589917153|ref|XP_006971891.1| PREDICTED: 26S proteasome non-ATPase regulatory subunit 3 [Peromyscus maniculatus bairdii]
maker-Contig19223-snap-gene-0.23-mRNA-1	2e-23	gi|589996783|ref|XP_006998863.1| PREDICTED: ATP synthase-coupling factor 6, mitochondrial-like, partial [Peromyscus maniculatus bairdii]
maker-Contig20050-exonerate_est2genome-gene-0.0-mRNA-1	0.0	gi|589969436|ref|XP_006997201.1| PREDICTED: sodium- and chloride-dependent glycine transporter 1 [Peromyscus maniculatus bairdii]
maker-Contig22396-snap-gene-0.21-mRNA-1	4e-153	gi|589936214|ref|XP_006980876.1| PREDICTED: sodium-coupled monocarboxylate transporter 2 [Peromyscus maniculatus bairdii]
maker-Contig22396-snap-gene-0.21-mRNA-1	1e-66	gi|589936214|ref|XP_006980876.1| PREDICTED: sodium-coupled monocarboxylate transporter 2 [Peromyscus maniculatus bairdii]
maker-Contig29903-exonerate_protein2genome-gene-0.16-mRNA-1	3e-77	gi|589939472|ref|XP_006982479.1| PREDICTED: V-type proton ATPase subunit G 3 [Peromyscus maniculatus bairdii]
maker-Contig30159-snap-gene-0.26-mRNA-1	0.0	gi|589932699|ref|XP_006979142.1| PREDICTED: gamma-glutamyltranspeptidase 1 [Peromyscus maniculatus bairdii]
maker-Contig30159-snap-gene-0.26-mRNA-1	4e-53	gi|589932699|ref|XP_006979142.1| PREDICTED: gamma-glutamyltranspeptidase 1 [Peromyscus maniculatus bairdii]
maker-Contig34873-exonerate_est2genome-gene-0.0-mRNA-1	9e-147	gi|589941802|ref|XP_006983621.1| PREDICTED: ATP synthase subunit O, mitochondrial [Peromyscus maniculatus bairdii]
maker-Contig35841-snap-gene-0.24-mRNA-1	0.0	gi|589943621|ref|XP_006984511.1| PREDICTED: katanin p60 ATPase-containing subunit A1 [Peromyscus maniculatus bairdii]
maker-Contig40578-exonerate_protein2genome-gene-0.16-mRNA-1	4e-91	gi|589917318|ref|XP_006971973.1| PREDICTED: ATP synthase F(0) complex subunit C1, mitochondrial isoform X2 [Peromyscus maniculatus bairdii]
maker-Contig40847-snap-gene-0.11-mRNA-1	6e-109	gi|589927692|ref|XP_006976673.1| PREDICTED: hippocalcin-like protein 1 [Peromyscus maniculatus bairdii]
maker-Contig57686-snap-gene-0.23-mRNA-1	0.0	gi|589948000|ref|XP_006986667.1| PREDICTED: EF-hand calcium-binding domain-containing protein 14 [Peromyscus maniculatus bairdii]
maker-Contig65048-snap-gene-0.8-mRNA-1	9e-109	gi|589943543|ref|XP_006984472.1| PREDICTED: ATP synthase subunit gamma, mitochondrial isoform X2 [Peromyscus maniculatus bairdii]
maker-Contig6685-exonerate_est2genome-gene-0.1-mRNA-1	1e-75	gi|589958124|ref|XP_006991658.1| PREDICTED: sodium- and chloride-dependent GABA transporter 2 [Peromyscus maniculatus bairdii]
maker-Contig70873-snap-gene-0.7-mRNA-1	1e-62	gi|589953998|ref|XP_006989631.1| PREDICTED: V-type proton ATPase subunit B, brain isoform [Peromyscus maniculatus bairdii]
maker-Contig72897-snap-gene-0.7-mRNA-1	7e-45	gi|589915799|ref|XP_006971228.1| PREDICTED: solute carrier family 2, facilitated glucose transporter member 2 [Peromyscus maniculatus bairdii]
maker-Contig7490-exonerate_est2genome-gene-0.0-mRNA-1	0.0	gi|589941639|ref|XP_006983541.1| PREDICTED: calcium-binding mitochondrial carrier protein SCaMC-2 [Peromyscus maniculatus bairdii]
maker-Contig77093-snap-gene-0.9-mRNA-1	4e-127	gi|589953998|ref|XP_006989631.1| PREDICTED: V-type proton ATPase subunit B, brain isoform [Peromyscus maniculatus bairdii]
maker-Contig82364-snap-gene-0.9-mRNA-1	6e-128	gi|589958124|ref|XP_006991658.1| PREDICTED: sodium- and chloride-dependent GABA transporter 2 [Peromyscus maniculatus bairdii]
maker-Contig82364-snap-gene-0.9-mRNA-1	2e-19	gi|589958124|ref|XP_006991658.1| PREDICTED: sodium- and chloride-dependent GABA transporter 2 [Peromyscus maniculatus bairdii]
maker-Contig8631-snap-gene-0.78-mRNA-1	1e-43	gi|589916805|ref|XP_006971721.1| PREDICTED: hematological and neurological expressed 1-like protein [Peromyscus maniculatus bairdii]
maker-Contig9249-exonerate_protein2genome-gene-0.63-mRNA-1	8e-71	gi|589933333|ref|XP_006979454.1| PREDICTED: V-type proton ATPase subunit F [Peromyscus maniculatus bairdii]
maker-Contig9353-exonerate_protein2genome-gene-0.55-mRNA-1	1e-120	gi|589920644|ref|XP_006973384.1| PREDICTED: mitochondrial inner membrane protease ATP23 homolog isoform X1 [Peromyscus maniculatus bairdii]
maker-Contig94553-snap-gene-0.11-mRNA-1	0.0	gi|589965263|ref|XP_006995166.1| PREDICTED: ATP-binding cassette sub-family A member 1 [Peromyscus maniculatus bairdii]
maker-Contig94553-snap-gene-0.11-mRNA-1	0.0	gi|589965263|ref|XP_006995166.1| PREDICTED: ATP-binding cassette sub-family A member 1 [Peromyscus maniculatus bairdii]
maker-Contig94553-snap-gene-0.11-mRNA-1	8e-18	gi|589965263|ref|XP_006995166.1| PREDICTED: ATP-binding cassette sub-family A member 1 [Peromyscus maniculatus bairdii]
snap_masked-Contig357048-processed-gene-0.3-mRNA-1	5e-49	gi|589913556|ref|XP_006970122.1| PREDICTED: collagen and calcium-binding EGF domain-containing protein 1 [Peromyscus maniculatus bairdii]
snap_masked-Contig39484-processed-gene-0.9-mRNA-1	3e-62	gi|589936767|ref|XP_006981150.1| PREDICTED: rap guanine nucleotide exchange factor 2 [Peromyscus maniculatus bairdii]
snap_masked-Contig39484-processed-gene-0.9-mRNA-1	5e-54	gi|589936767|ref|XP_006981150.1| PREDICTED: rap guanine nucleotide exchange factor 2 [Peromyscus maniculatus bairdii]
snap_masked-Contig39484-processed-gene-0.9-mRNA-1	2e-14	gi|589936767|ref|XP_006981150.1| PREDICTED: rap guanine nucleotide exchange factor 2 [Peromyscus maniculatus bairdii]