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


    LINKS -l 2 -t 10 -d 500 -f mya.fa -s reads.txt -b iter500 -r mya.bloom
    LINKS -l 2 -t 10 -d 600 -f iter500.scaffolds.fa -s reads.txt -b iter600 -r mya.bloom
    LINKS -l 2 -t 10 -d 700 -f iter600.scaffolds.fa -s reads.txt -b iter700 -r mya.bloom
    LINKS -l 2 -t 10 -d 800 -f iter700.scaffolds.fa -s reads.txt -b iter800 -r mya.bloom
    LINKS -l 2 -t 10 -d 900 -f iter800.scaffolds.fa -s reads.txt -b iter900 -r mya.bloom   
    LINKS -l 2 -t 10 -d 1000 -f iter900.scaffolds.fa -s reads.txt -b iter1000 -r mya.bloom
    LINKS -l 2 -t 10 -d 1500 -f iter1000.scaffolds.fa -s reads.txt -b iter1500 -r mya.bloom 
    LINKS -l 2 -t 10 -d 2000 -f iter1500.scaffolds.fa -s reads.txt -b iter2000 -r mya.bloom
    LINKS -l 2 -t 10 -d 2500 -f iter2000.scaffolds.fa -s reads.txt -b iter2500 -r mya.bloom
    LINKS -l 2 -t 10 -d 3000 -f iter2500.scaffolds.fa -s reads.txt -b iter3000 -r mya.bloom
    LINKS -l 2 -t 10 -d 3500 -f iter3000.scaffolds.fa -s reads.txt -b iter3500 -r mya.bloom
    LINKS -l 2 -t 10 -d 4000 -f iter3500.scaffolds.fa -s reads.txt -b iter4000 -r mya.bloom
    LINKS -l 2 -t 10 -d 4500 -f iter4000.scaffolds.fa -s reads.txt -b iter4500 -r mya.bloom
    LINKS -l 2 -t 10 -d 5000 -f iter4500.scaffolds.fa -s reads.txt -b iter5000 -r mya.bloom
    LINKS -l 2 -t 10 -d 5500 -f iter5000.scaffolds.fa -s reads.txt -b iter5500 -r mya.bloom
    LINKS -l 2 -t 10 -d 6000 -f iter5500.scaffolds.fa -s reads.txt -b iter6000 -r mya.bloom
    LINKS -l 2 -t 10 -d 7000 -f iter6000.scaffolds.fa -s reads.txt -b iter7000 -r mya.bloom
    LINKS -l 2 -t 10 -d 8000 -f iter7000.scaffolds.fa -s reads.txt -b iter8000 -r mya.bloom
    LINKS -l 2 -t 10 -d 9000 -f iter8000.scaffolds.fa -s reads.txt -b iter9000 -r mya.bloom
    LINKS -l 2 -t 10 -d 10000 -f iter9000.scaffolds.fa -s reads.txt -b iter10000 -r mya.bloom
    LINKS -l 2 -t 10 -d 11000 -f iter10000.scaffolds.fa -s reads.txt -b iter11000 -r mya.bloom
    LINKS -l 2 -t 10 -d 12000 -f iter11000.scaffolds.fa -s reads.txt -b iter12000 -r mya.bloom
    LINKS -l 2 -t 10 -d 13000 -f iter12000.scaffolds.fa -s reads.txt -b iter13000 -r mya.bloom
    LINKS -l 2 -t 10 -d 14000 -f iter13000.scaffolds.fa -s reads.txt -b iter14000 -r mya.bloom
    LINKS -l 2 -t 10 -d 15000 -f iter14000.scaffolds.fa -s reads.txt -b iter15000 -r mya.bloom
    LINKS -l 2 -t 10 -d 16000 -f iter15000.scaffolds.fa -s reads.txt -b iter16000 -r mya.bloom
    LINKS -l 2 -t 10 -d 17000 -f iter16000.scaffolds.fa -s reads.txt -b iter17000 -r mya.bloom
    LINKS -l 2 -t 10 -d 18000 -f iter17000.scaffolds.fa -s reads.txt -b iter18000 -r mya.bloom
    LINKS -l 2 -t 10 -d 19000 -f iter18000.scaffolds.fa -s reads.txt -b iter19000 -r mya.bloom
    LINKS -l 2 -t 10 -d 20000 -f iter19000.scaffolds.fa -s reads.txt -b iter20000 -r mya.bloom
    LINKS -l 2 -t 10 -d 21000 -f iter20000.scaffolds.fa -s reads.txt -b iter21000 -r mya.bloom
    LINKS -l 2 -t 10 -d 22000 -f iter21000.scaffolds.fa -s reads.txt -b iter22000 -r mya.bloom
    LINKS -l 2 -t 10 -d 23000 -f iter22000.scaffolds.fa -s reads.txt -b iter23000 -r mya.bloom
>>>>>>> Stashed changes
