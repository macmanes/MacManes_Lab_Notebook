Mytilus Project
--

	scp /Users/macmanes/Desktop/Newest\ 454/RL4\ copy/454AllContigs.fna macmanes@132.177.115.145:/mouse/Mytilus/RL4.454AllContigs.fna
	scp /Users/macmanes/Desktop/Newest\ 454/RL5\ copy/454AllContigs.fna macmanes@132.177.115.145:/mouse/Mytilus/RL5.454AllContigs.fna
	scp /Users/macmanes/Desktop/Newest\ 454/RL6\ copy/454AllContigs.fna macmanes@132.177.115.145:/mouse/Mytilus/RL6.454AllContigs.fna
	scp /Users/macmanes/Desktop/Newest\ 454/RL7\ copy/454AllContigs.fna macmanes@132.177.115.145:/mouse/Mytilus/RL7.454AllContigs.fna
	scp /Users/macmanes/Desktop/Newest\ 454/RL8\ copy/454AllContigs.fna macmanes@132.177.115.145:/mouse/Mytilus/RL8.454AllContigs.fna
	scp /Users/macmanes/Desktop/Newest\ 454/RL9\ copy/454AllContigs.fna macmanes@132.177.115.145:/mouse/Mytilus/RL9.454AllContigs.fna
	scp /Users/macmanes/Desktop/Newest\ 454/RL10\ copy/454AllContigs.fna macmanes@132.177.115.145:/mouse/Mytilus/RL10.454AllContigs.fna
	scp /Users/macmanes/Desktop/Newest\ 454/RL11\ copy/454AllContigs.fna macmanes@132.177.115.145:/mouse/Mytilus/RL11.454AllContigs.fna
	scp /Users/macmanes/Desktop/Newest\ 454/RL12\ copy/454AllContigs.fna macmanes@132.177.115.145:/mouse/Mytilus/RL12.454AllContigs.fna
	
cat them together

	cat *fna > Mytilus.fasta
	
cdhit

	cd-hit-est -M 5000 -T 24 -c .97 -i Mytilus.fasta -o Mytilus.cdhit.fasta
	
    abyss-fac Mytilus.cdhit.fasta Mytilus.fasta
    Mytilus.cdhit.fasta Mytilus.fasta
    n	n:500	n:N50	min	N80	N50	N20	E-size	max	sum	name
    4183	1687	613	500	601	787	1148	934	6060	1336802	Mytilus.cdhit.fasta
    6674	2705	973	500	597	775	1155	941	6060	2138125	
    

blast

	blastx -db /home/macmanes/spider/refined/refseq/refseq -query Mytilus.cdhit.fasta -outfmt 6 -evalue 1e-5 -num_threads 30 -out mytilus.blast