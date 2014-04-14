retrain cegma with Maker gff
---------------

this is using the maker derived gff from ~1000 contigs edited.

    ~/maker/bin/maker2zff ../augustus/peer.gff  ../../pero-genome/jelly.out.fasta
 
this gives me a lot of errors like 

	Use of uninitialized value $tag in string eq at /home/macmanes/maker/bin/maker2zff line 130, <GFF> line 725359.` 

Hmmmm
  
    fathom genome.ann genome.dna -categorize 1000
    fathom -export 1000 -plus uni.ann uni.dna
    forge export.ann export.dna
    hmm-assembler.pl jelly.out.fasta . > cegmasnap.hmm
