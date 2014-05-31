Pigeon


Mapping
	
	STAR --genomeDir livia --readFilesIn /mnt/data3/macmanes/pero_pigeons_ladybugs/O.trim_1P.fq /mnt/data3/macmanes/pero_pigeons_ladybugs/O.trim_2P.fq \
	--runThreadN 30 --genomeLoad LoadAndKeep --outFilterIntronMotifs RemoveNoncanonical --outFileNamePrefix Ovary


	STAR --genomeDir livia --readFilesIn /mnt/data3/macmanes/pero_pigeons_ladybugs/Pit.trim_1P.fq /mnt/data3/macmanes/pero_pigeons_ladybugs/Pit.trim_2P.fq \
	--runThreadN 30 --genomeLoad LoadAndKeep --outFilterIntronMotifs RemoveNoncanonical --outFileNamePrefix Pit

	STAR --genomeDir livia --readFilesIn /mnt/data3/macmanes/pero_pigeons_ladybugs/TE.trim_1P.fq /mnt/data3/macmanes/pero_pigeons_ladybugs/TE.trim_2P.fq \
	--runThreadN 30 --genomeLoad LoadAndKeep --outFilterIntronMotifs RemoveNoncanonical --outFileNamePrefix testes

	STAR --genomeDir livia --readFilesIn /mnt/data3/macmanes/pero_pigeons_ladybugs/Hy.trim_1P.fq /mnt/data3/macmanes/pero_pigeons_ladybugs/Hy.trim_2P.fq \
	--runThreadN 30 --genomeLoad LoadAndKeep --outFilterIntronMotifs RemoveNoncanonical --outFileNamePrefix Hypo