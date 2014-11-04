Mytilus Project
--

	scp /Users/macmanes/Desktop/Newest\ 454/RL1\ copy/454AllContigs.fna macmanes@132.177.115.145:/mouse/Mytilus/RL1.454AllContigs.fna
	scp /Users/macmanes/Desktop/Newest\ 454/RL2\ copy/454AllContigs.fna macmanes@132.177.115.145:/mouse/Mytilus/RL2.454AllContigs.fna
	scp /Users/macmanes/Desktop/Newest\ 454/RL3\ copy/454AllContigs.fna macmanes@132.177.115.145:/mouse/Mytilus/RL3.454AllContigs.fna
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
	
stats


    macmanes@davinci:/mouse/Mytilus$ abyss-fac Mytilus.cdhit.fasta Mytilus.fasta
    n	n:500	n:N50	min	N80	N50	N20	E-size	max	sum	name
    4183	1687	613	500	601	787	1148	934	6060	1336802	Mytilus.cdhit.fasta
    6674	2705	973	500	597	775	1155	941	6060	2138125	Mytilus.fasta
    
    
    macmanes@davinci:/mouse/Mytilus$ abyss-fac *fna
    n	n:500	n:N50	min	N80	N50	N20	E-size	max	sum	name
    295	157	62	500	568	680	913	805	2343	111919	RL10.454AllContigs.fna
    337	132	53	500	566	710	917	750	1445	92893	RL11.454AllContigs.fna
    306	180	70	501	564	684	978	796	1987	129217	RL12.454AllContigs.fna
    657	192	68	502	583	751	1233	962	3997	151026	RL1.454AllContigs.fna
    1145	562	205	500	614	806	1158	925	3557	452732	RL2.454AllContigs.fna
    926	289	103	500	591	770	1214	953	4518	227453	RL3.454AllContigs.fna
    1281	397	138	500	596	796	1210	1031	6060	321883	RL4.454AllContigs.fna
    158	115	41	507	628	816	1335	1008	2746	96661	RL5.454AllContigs.fna
    526	218	77	500	620	838	1292	1041	4496	185211	RL6.454AllContigs.fna
    236	95	33	500	647	830	1405	1018	2198	82171	RL7.454AllContigs.fna
    364	206	74	501	622	854	1149	994	3652	172306	RL8.454AllContigs.fna
    443	162	65	500	557	681	911	796	2191	114653	RL9.454AllContigs.fna

    

blast

	blastx -db /home/macmanes/spider/refined/refseq/refseq -query Mytilus.cdhit.fasta -outfmt 6 -evalue 1e-5 -num_threads 30 -out mytilus.blast