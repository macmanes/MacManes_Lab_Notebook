SMRT analysis Setup

c3.8xl

--

	sudo bash
	chown -R ubuntu:ubuntu /mnt
	apt-get install git-core tmux unzip
	bash smrtanalysis_2.3.0.140936_linux_x86-64_libc-2.5_centos-53.run --rootdir /tmp --patchfile current-patch_smrtanalysis_2.3.0.140936_linux_x86-64_libc-2.5_centos-53.run --extract-only
	PATH=$PATH:/tmp/install/smrtanalysis_2.3.0.140936/analysis/bin/
	wget https://sites.google.com/site/dbg2olc/home/Programs.zip
	unzip Programs.zip
	mv Programs dbg2olc
	cd dbg2olc
	chmod +x DBG2OLC_Linux
	unzip split_and_run_pbdagcon.zip
	chmod +x SeqIO.py
	chmod +x split_reads_by_backbone.py
	chmod +x split_and_run_pbdagcon.sh
	PATH=$PATH:$(pwd)
	
load reads

	#PB reads
	scp -i /home/macmanes/ec2/AMI-davinci.pem /mouse/Mya/pacbio/fasta/mya.pacbio.fasta \
	ubuntu@ec2-54-174-186-18.compute-1.amazonaws.com:/mnt
	
	#Assembly
	scp -i /home/macmanes/ec2/AMI-davinci.pem /mouse/Mya/abyss/k67/clam67-6.fa \
	ubuntu@ec2-54-174-186-18.compute-1.amazonaws.com:/mnt
	