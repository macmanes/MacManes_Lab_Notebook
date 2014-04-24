retrain cegma with Maker gff
---------------

this is using the maker derived gff from ~1000 contigs edited.

    ~/maker/bin/maker2zff ../augustus/peer.gff  
    /home/macmanes/maker/exe/snap/fathom genome.ann genome.dna -categorize 1000
    /home/macmanes/maker/exe/snap/fathom -export 1000 -plus uni.ann uni.dna
    /home/macmanes/maker/exe/snap/forge export.ann export.dna
    /home/macmanes/maker/exe/snap/hmm-assembler.pl ../pero-genome/jelly.out.fasta . > cegmasnap.hmm


this gives me. in `/media/macmanes/hd3/maker/cegma`

`cegmasnap.hmm`