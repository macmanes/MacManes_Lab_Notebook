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



sudo mkfs -t ext4 /dev/xvdf
sudo mount /dev/xvdf /mnt
sudo chown -R ubuntu:ubuntu /mnt
```


```
PATH=$PATH:/home/ubuntu/seqtk:/home/ubuntu/bwa:/home/ubuntu/transrate-1.0.1-linux-x86_64:/home/ubuntu/BUSCO_v1.1b1:/home/ubuntu/augustus-3.0.2/bin:/home/ubuntu/augustus-3.0.2/scripts:/home/ubuntu/ncbi-blast-2.2.31+/bin:/home/ubuntu/TransDecoder:/home/ubuntu/bamtools/bin
export AUGUSTUS_CONFIG_PATH=/home/ubuntu/augustus-3.0.2/config/

```