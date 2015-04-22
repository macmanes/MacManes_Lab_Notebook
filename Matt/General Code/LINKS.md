LINKS
--

    for k in 500 1000 2000 3000 4000 5000 6000 7000 8000; do  
		LINKS -d $k -f abyss113-8.fa -s all.long.harmonia.fasta -b iter$k;  
    done 
    

	ARRAY=( 1 2 3 )

    for m in "${arrayname[@]}"; do
    	echo ${ARRAY[0]};
    done
    


    LINKS -l 1 -d 500 -f harm.fa -s all.long.harmonia.fasta -b iter500
    LINKS -l 1 -d 600 -f iter500.scaffolds.fa -s all.long.harmonia.fasta -b iter600
    LINKS -l 1 -d 700 -f iter600.scaffolds.fa -s all.long.harmonia.fasta -b iter700
    LINKS -l 1 -d 800 -f iter700.scaffolds.fa -s all.long.harmonia.fasta -b iter800
    LINKS -l 1 -d 900 -f iter800.scaffolds.fa -s all.long.harmonia.fasta -b iter900   
    LINKS -l 1 -d 1000 -f iter900.scaffolds.fa -s all.long.harmonia.fasta -b iter1000   
    LINKS -l 1 -d 1500 -f iter1000.scaffolds.fa -s all.long.harmonia.fasta -b iter1500   
    LINKS -l 1 -d 2000 -f iter1500.scaffolds.fa -s all.long.harmonia.fasta -b iter2000
    LINKS -l 1 -d 2500 -f iter2000.scaffolds.fa -s all.long.harmonia.fasta -b iter2500
    LINKS -l 1 -d 3000 -f iter2500.scaffolds.fa -s all.long.harmonia.fasta -b iter3000
    LINKS -l 1 -d 3500 -f iter3000.scaffolds.fa -s all.long.harmonia.fasta -b iter3500
    LINKS -l 1 -d 4000 -f iter3500.scaffolds.fa -s all.long.harmonia.fasta -b iter4000
    LINKS -l 1 -d 4500 -f iter4000.scaffolds.fa -s all.long.harmonia.fasta -b iter4500
    LINKS -l 1 -d 5000 -f iter4500.scaffolds.fa -s all.long.harmonia.fasta -b iter5000
    LINKS -l 1 -d 5500 -f iter5000.scaffolds.fa -s all.long.harmonia.fasta -b iter5500
    LINKS -l 1 -d 6000 -f iter5500.scaffolds.fa -s all.long.harmonia.fasta -b iter6000
    LINKS -l 1 -d 7000 -f iter6000.scaffolds.fa -s all.long.harmonia.fasta -b iter7000
    LINKS -l 1 -d 8000 -f iter7000.scaffolds.fa -s all.long.harmonia.fasta -b iter8000
    LINKS -l 1 -d 9000 -f iter8000.scaffolds.fa -s all.long.harmonia.fasta -b iter9000
    LINKS -l 1 -d 10000 -f iter9000.scaffolds.fa -s all.long.harmonia.fasta -b iter10000
    LINKS -l 1 -d 11000 -f iter10000.scaffolds.fa -s all.long.harmonia.fasta -b iter11000
    LINKS -l 1 -d 12000 -f iter11000.scaffolds.fa -s all.long.harmonia.fasta -b iter12000
    LINKS -l 1 -d 13000 -f iter12000.scaffolds.fa -s all.long.harmonia.fasta -b iter13000
    LINKS -l 1 -d 14000 -f iter13000.scaffolds.fa -s all.long.harmonia.fasta -b iter14000
    LINKS -l 1 -d 15000 -f iter14000.scaffolds.fa -s all.long.harmonia.fasta -b iter15000
    LINKS -l 1 -d 16000 -f iter15000.scaffolds.fa -s all.long.harmonia.fasta -b iter16000
    LINKS -l 1 -d 17000 -f iter16000.scaffolds.fa -s all.long.harmonia.fasta -b iter17000
    LINKS -l 1 -d 18000 -f iter17000.scaffolds.fa -s all.long.harmonia.fasta -b iter18000
    LINKS -l 1 -d 19000 -f iter18000.scaffolds.fa -s all.long.harmonia.fasta -b iter19000
    LINKS -l 1 -d 20000 -f iter19000.scaffolds.fa -s all.long.harmonia.fasta -b iter20000
    LINKS -l 1 -d 21000 -f iter20000.scaffolds.fa -s all.long.harmonia.fasta -b iter21000
    LINKS -l 1 -d 22000 -f iter21000.scaffolds.fa -s all.long.harmonia.fasta -b iter22000
    LINKS -l 1 -d 23000 -f iter22000.scaffolds.fa -s all.long.harmonia.fasta -b iter23000
   

Mya links

<<<<<<< Updated upstream
    LINKS -l 2 -d 500 -t 100 -f mya.fa -s ../pacbio/fasta/mya.pacbio.fasta -b iter500
    LINKS -l 2 -d 600 -f iter500.scaffolds.fa -s ../pacbio/fasta/mya.pacbio.fasta -b iter600
    LINKS -l 2 -d 700 -f iter600.scaffolds.fa -s ../pacbio/fasta/mya.pacbio.fasta -b iter700
    LINKS -l 2 -d 800 -f iter700.scaffolds.fa -s ../pacbio/fasta/mya.pacbio.fasta -b iter800
    LINKS -l 2 -d 900 -f iter800.scaffolds.fa -s ../pacbio/fasta/mya.pacbio.fasta -b iter900   
    LINKS -l 2 -d 1000 -f iter900.scaffolds.fa -s ../pacbio/fasta/mya.pacbio.fasta -b iter1000   
    LINKS -l 2 -d 1500 -f iter1000.scaffolds.fa -s ../pacbio/fasta/mya.pacbio.fasta -b iter1500   
    LINKS -l 2 -d 2000 -f iter1500.scaffolds.fa -s ../pacbio/fasta/mya.pacbio.fasta -b iter2000
    LINKS -l 2 -d 2500 -f iter2000.scaffolds.fa -s ../pacbio/fasta/mya.pacbio.fasta -b iter2500
    LINKS -l 2 -d 3000 -f iter2500.scaffolds.fa -s ../pacbio/fasta/mya.pacbio.fasta -b iter3000
    LINKS -l 2 -d 3500 -f iter3000.scaffolds.fa -s ../pacbio/fasta/mya.pacbio.fasta -b iter3500
    LINKS -l 2 -d 4000 -f iter3500.scaffolds.fa -s ../pacbio/fasta/mya.pacbio.fasta -b iter4000
    LINKS -l 2 -d 4500 -f iter4000.scaffolds.fa -s ../pacbio/fasta/mya.pacbio.fasta -b iter4500
    LINKS -l 2 -d 5000 -f iter4500.scaffolds.fa -s ../pacbio/fasta/mya.pacbio.fasta -b iter5000
    LINKS -l 2 -d 5500 -f iter5000.scaffolds.fa -s ../pacbio/fasta/mya.pacbio.fasta -b iter5500
    LINKS -l 2 -d 6000 -f iter5500.scaffolds.fa -s ../pacbio/fasta/mya.pacbio.fasta -b iter6000
    LINKS -l 2 -d 7000 -f iter6000.scaffolds.fa -s ../pacbio/fasta/mya.pacbio.fasta -b iter7000
    LINKS -l 2 -d 8000 -f iter7000.scaffolds.fa -s ../pacbio/fasta/mya.pacbio.fasta -b iter8000
    LINKS -l 2 -d 9000 -f iter8000.scaffolds.fa -s ../pacbio/fasta/mya.pacbio.fasta -b iter9000
    LINKS -l 2 -d 10000 -f iter9000.scaffolds.fa -s ../pacbio/fasta/mya.pacbio.fasta -b iter10000
    LINKS -l 2 -d 11000 -f iter10000.scaffolds.fa -s ../pacbio/fasta/mya.pacbio.fasta -b iter11000
    LINKS -l 2 -d 12000 -f iter11000.scaffolds.fa -s ../pacbio/fasta/mya.pacbio.fasta -b iter12000
    LINKS -l 2 -d 13000 -f iter12000.scaffolds.fa -s ../pacbio/fasta/mya.pacbio.fasta -b iter13000
    LINKS -l 2 -d 14000 -f iter13000.scaffolds.fa -s ../pacbio/fasta/mya.pacbio.fasta -b iter14000
    LINKS -l 2 -d 15000 -f iter14000.scaffolds.fa -s ../pacbio/fasta/mya.pacbio.fasta -b iter15000
    LINKS -l 2 -d 16000 -f iter15000.scaffolds.fa -s ../pacbio/fasta/mya.pacbio.fasta -b iter16000
    LINKS -l 2 -d 17000 -f iter16000.scaffolds.fa -s ../pacbio/fasta/mya.pacbio.fasta -b iter17000
    LINKS -l 2 -d 18000 -f iter17000.scaffolds.fa -s ../pacbio/fasta/mya.pacbio.fasta -b iter18000
    LINKS -l 2 -d 19000 -f iter18000.scaffolds.fa -s ../pacbio/fasta/mya.pacbio.fasta -b iter19000
    LINKS -l 2 -d 20000 -f iter19000.scaffolds.fa -s ../pacbio/fasta/mya.pacbio.fasta -b iter20000
    LINKS -l 2 -d 21000 -f iter20000.scaffolds.fa -s ../pacbio/fasta/mya.pacbio.fasta -b iter21000
    LINKS -l 2 -d 22000 -f iter21000.scaffolds.fa -s ../pacbio/fasta/mya.pacbio.fasta -b iter22000
    LINKS -l 2 -d 23000 -f iter22000.scaffolds.fa -s ../pacbio/fasta/mya.pacbio.fasta -b iter23000
=======
    LINKS -l 4 -d 500 -f mya.fa -s pacbio2.fa -b iter500
    LINKS -l 4 -d 600 -f iter500.scaffolds.fa -s pacbio2.fa -b iter600
    LINKS -l 4 -d 700 -f iter600.scaffolds.fa -s pacbio2.fa -b iter700
    LINKS -l 4 -d 800 -f iter700.scaffolds.fa -s pacbio2.fa -b iter800
    LINKS -l 4 -d 900 -f iter800.scaffolds.fa -s pacbio2.fa -b iter900   
    LINKS -l 4 -d 1000 -f iter900.scaffolds.fa -s pacbio2.fa -b iter1000   
    LINKS -l 4 -d 1500 -f iter1000.scaffolds.fa -s pacbio2.fa -b iter1500   
    LINKS -l 4 -d 2000 -f iter1500.scaffolds.fa -s pacbio2.fa -b iter2000
    LINKS -l 4 -d 2500 -f iter2000.scaffolds.fa -s pacbio2.fa -b iter2500
    LINKS -l 4 -d 3000 -f iter2500.scaffolds.fa -s pacbio2.fa -b iter3000
    LINKS -l 4 -d 3500 -f iter3000.scaffolds.fa -s pacbio2.fa -b iter3500
    LINKS -l 4 -d 4000 -f iter3500.scaffolds.fa -s pacbio2.fa -b iter4000
    LINKS -l 4 -d 4500 -f iter4000.scaffolds.fa -s pacbio2.fa -b iter4500
    LINKS -l 4 -d 5000 -f iter4500.scaffolds.fa -s pacbio2.fa -b iter5000
    LINKS -l 4 -d 5500 -f iter5000.scaffolds.fa -s pacbio2.fa -b iter5500
    LINKS -l 4 -d 6000 -f iter5500.scaffolds.fa -s pacbio2.fa -b iter6000
    LINKS -l 4 -d 7000 -f iter6000.scaffolds.fa -s pacbio2.fa -b iter7000
    LINKS -l 4 -d 8000 -f iter7000.scaffolds.fa -s pacbio2.fa -b iter8000
    LINKS -l 4 -d 9000 -f iter8000.scaffolds.fa -s pacbio2.fa -b iter9000
    LINKS -l 4 -d 10000 -f iter9000.scaffolds.fa -s pacbio2.fa -b iter10000
    LINKS -l 4 -d 11000 -f iter10000.scaffolds.fa -s pacbio2.fa -b iter11000
    LINKS -l 4 -d 12000 -f iter11000.scaffolds.fa -s pacbio2.fa -b iter12000
    LINKS -l 4 -d 13000 -f iter12000.scaffolds.fa -s pacbio2.fa -b iter13000
    LINKS -l 4 -d 14000 -f iter13000.scaffolds.fa -s pacbio2.fa -b iter14000
    LINKS -l 4 -d 15000 -f iter14000.scaffolds.fa -s pacbio2.fa -b iter15000
    LINKS -l 4 -d 16000 -f iter15000.scaffolds.fa -s pacbio2.fa -b iter16000
    LINKS -l 4 -d 17000 -f iter16000.scaffolds.fa -s pacbio2.fa -b iter17000
    LINKS -l 4 -d 18000 -f iter17000.scaffolds.fa -s pacbio2.fa -b iter18000
    LINKS -l 4 -d 19000 -f iter18000.scaffolds.fa -s pacbio2.fa -b iter19000
    LINKS -l 4 -d 20000 -f iter19000.scaffolds.fa -s pacbio2.fa -b iter20000
    LINKS -l 4 -d 21000 -f iter20000.scaffolds.fa -s pacbio2.fa -b iter21000
    LINKS -l 4 -d 22000 -f iter21000.scaffolds.fa -s pacbio2.fa -b iter22000
    LINKS -l 4 -d 23000 -f iter22000.scaffolds.fa -s pacbio2.fa -b iter23000
>>>>>>> Stashed changes
