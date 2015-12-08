AWS Configure
--

```
sudo apt-get update && sudo apt-get -y upgrade

sudo apt-get -y install cmake sparsehash valgrind libboost-atomic1.55-dev libibnetdisc-dev ruby-full gsl-bin libgsl0-dev libgsl0ldbl libboost1.55-all-dev libboost1.55-dbg subversion tmux git curl bowtie libncurses5-dev samtools gcc make g++ python-dev unzip dh-autoreconf default-jre python-pip zlib1g-dev hmmer cmake libhdf5-dev


sudo cpan URI::Escape

cd $HOME
git clone https://github.com/lh3/seqtk.git
cd seqtk
make -j4
PATH=$PATH:$(pwd)

cd $HOME
git clone https://github.com/lh3/bwa.git
cd bwa
make -j4
PATH=$PATH:$(pwd)

sudo easy_install -U setuptools
sudo pip install khmer

cd $HOME
git clone https://github.com/pachterlab/kallisto.git
cd kallisto
mkdir build
cd build
cmake ..
make
sudo make install

cd $HOME
curl -LO https://github.com/COMBINE-lab/salmon/archive/v0.5.1.tar.gz
tar -zxf v0.5.1.tar.gz
cd salmon-0.5.1/
mkdir build
cd build
cmake ..
make -j6
sudo make all install


cd
curl -LO https://bintray.com/artifact/download/blahah/generic/transrate-1.0.1-linux-x86_64.tar.gz
tar -zxf transrate-1.0.1-linux-x86_64.tar.gz
PATH=$PATH:/home/ubuntu/transrate-1.0.1-linux-x86_64

cd
curl -LO http://busco.ezlab.org/files/BUSCO_v1.1b1.tar.gz
tar -zxf BUSCO_v1.1b1.tar.gz
cd BUSCO_v1.1b1
PATH=$PATH:$(pwd)
curl -LO http://busco.ezlab.org/files/metazoa_buscos.tar.gz
curl -LO http://busco.ezlab.org/files/vertebrata_buscos.tar.gz
tar -zxf vertebrata_buscos.tar.gz
tar -zxf metazoa_buscos.tar.gz


cd
git clone git://github.com/pezmaster31/bamtools.git
cd bamtools && mkdir build && cd build && cmake .. && make

cd
curl -LO http://bioinf.uni-greifswald.de/augustus/binaries/old/augustus-3.0.2.tar.gz
tar -zxf augustus-3.0.2.tar.gz
cd augustus-3.0.2/
make
PATH=$PATH:$(pwd)/bin:$(pwd)/scripts
export AUGUSTUS_CONFIG_PATH=/home/ubuntu/augustus-3.0.2/config/

cd
curl -LO ftp://ftp.ncbi.nlm.nih.gov/blast/executables/blast+/LATEST/ncbi-blast-2.2.31+-x64-linux.tar.gz
tar -zxf ncbi-blast-2.2.31+-x64-linux.tar.gz
PATH=$PATH:/home/ubuntu/ncbi-blast-2.2.31+/bin


cd 
git clone https://github.com/TransDecoder/TransDecoder.git
cd TransDecoder
make -j4

cd
git clone https://github.com/trinityrnaseq/trinityrnaseq.git
cd trinityrnaseq
make -j6
PATH:$PATH:$(pwd)

#sudo mkfs -t ext4 /dev/xvdf
sudo mount /dev/xvdf /mnt
sudo chown -R ubuntu:ubuntu /mnt
```


```
PATH=$PATH:/home/ubuntu/seqtk:/home/ubuntu/bwa:/home/ubuntu/transrate-1.0.1-linux-x86_64:/home/ubuntu/BUSCO_v1.1b1:/home/ubuntu/augustus-3.0.2/bin:/home/ubuntu/augustus-3.0.2/scripts:/home/ubuntu/ncbi-blast-2.2.31+/bin:/home/ubuntu/TransDecoder:/home/ubuntu/bamtools/bin:/home/ubuntu/salmon-0.5.1/bin:/home/ubuntu/trinityrnaseq

export AUGUSTUS_CONFIG_PATH=/home/ubuntu/augustus-3.0.2/config/
export LD_LIBRARY_PATH=/home/ubuntu/salmon-0.5.1/lib

alias df='df -kTh'
alias h='history'
alias c='clear'
alias gh='history | grep'
alias ll='logout'
alias n='nano'
alias l='ls -lth'
alias m='more'
alias vm='vmstat -anwS M 10 5'
alias ...="../../"
alias ....="../../../"
alias mv='mv -i'
alias cp='cp -i'
alias targz='tar -zcf'
alias utargz='tar -zxf'
alias tn="tmux new -s"
alias ta="tmux attach -t"
alias tl="tmux ls"
alias tk="tmux kill-session -t"

```