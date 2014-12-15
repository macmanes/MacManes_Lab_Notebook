SMRT analysis
--

	sudo bash
	apt-get git tmux unzip
	bash smrtanalysis_2.3.0.140936_linux_x86-64_libc-2.5_centos-53.run --rootdir /tmp --patchfile current-patch_smrtanalysis_2.3.0.140936_linux_x86-64_libc-2.5_centos-53.run --extract-only
	PATH=$PATH:/tmp/install/smrtanalysis_2.3.0.140936/analysis/bin/
	wget https://sites.google.com/site/dbg2olc/home/Programs.zip
	apt-get install unzip
	unzip Programs.zip
	mv Programs dbg2olc
	cd dbg2olc
	chmod +x DBG2OLC_Linux
	PATH=$PATH:$(pwd)
	