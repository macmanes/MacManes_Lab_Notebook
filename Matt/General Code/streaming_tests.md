Streaming Test
=

install stuff

```
sudo apt-get update
sudo apt-get -y upgrade
sudo apt-get -y install build-essential tmux git gcc make g++ python-dev libcurl4-openssl-dev zlib1g-dev python-pip libncurses5-dev

git clone https://github.com/dib-lab/khmer.git
sudo easy_install -U setuptools
cd khmer && make && sudo make install && cd 

git clone https://github.com/relipmoc/skewer.git
cd skewer && make && sudo make install && cd

git clone https://github.com/lh3/bwa.git
cd bwa && make && sudo make install && PATH=$PATH:$(pwd) && cd

git clone https://github.com/samtools/htslib.git
cd htslib && make && sudo make install && cd

git clone https://github.com/samtools/samtools.git
cd samtools  && make && sudo make install && cd

```

```

mkdir reads && cd reads




**FROM DAVINCI**

scp -i /home/macmanes/ec2/AMI-davinci.pem Mya* ubuntu@ec2-52-5-206-104.compute-1.amazonaws.com:/home/ubuntu/reads/

**BACK TO AWS**

curl -LO https://s3.amazonaws.com/mya-genome/clam-no-leukemia-MP-5k_CGATGTAT_BC7A4MANXX_L001_001.R1.fastq.gz
curl -LO https://s3.amazonaws.com/mya-genome/clam-no-leukemia-MP-5k_CGATGTAT_BC7A4MANXX_L001_001.R2.fastq.gz

gzip -cd clam-no-leukemia-MP-5k_CGATGTAT_BC7A4MANXX_L001_001.R1.fastq.gz | head -4000000 | gzip - > test1.fq.gz
gzip -cd clam-no-leukemia-MP-5k_CGATGTAT_BC7A4MANXX_L001_001.R2.fastq.gz | head -4000000 | gzip - > test2.fq.gz
```

**the tests**

```
time interleave-reads.py \
test1.fq.gz \
test2.fq.gz \
| skewer -Q 5 -t 2 -x adap.fa - -1 \
| extract-paired-reads.py -p - -s /dev/null - \
| bwa mem -p -t 4 Mya81-contigs.fa - \
| samtools view -Sb - \
| samtools sort -@ 2 -m 2G - clam.5kb

real	3m29.302s
user	17m54.692s
sys	0m6.893s

```

and

```
time interleave-reads.py \
test1.fq.gz \
test2.fq.gz \
| skewer -Q 5 -t 8 -x adap.fa - -1 \
| extract-paired-reads.py -p - -s /dev/null - \
| bwa mem -p -t 8 Mya81-contigs.fa - \
| samtools view -Sb - \
| samtools sort -@ 8 -m 2G - clam.5kb

real    3m9.517s
user    20m56.238s
sys     0m8.537s

real    3m10.844s
user    20m59.161s
sys     0m8.739s

```
and

```
time interleave-reads.py \
test1.fq.gz \
test2.fq.gz \
| skewer -Q 5 -t 8 -x adap.fa - -1 \
| extract-paired-reads.py -p - -s /dev/null - \
| bwa mem -p -t 8 Mya81-contigs.fa - \
| samtools view -Sb - \
| samtools sort -@ 1 -m 10G - clam.5kb

real    3m26.037s
user    20m48.158s
sys     0m8.213s

real    3m25.600s
user    20m46.601s
sys     0m7.605s

```

and

```
time interleave-reads.py \
test1.fq.gz \
test2.fq.gz \
| skewer -Q 5 -t 8 -x adap.fa - -1 \
| extract-paired-reads.py -p - -s /dev/null - \
| bwa mem -p -t 8 Mya81-contigs.fa - \
| samtools view -F4 -Sb - \
| samtools sort -@ 8 -m 2G - clam.5kb

real    3m8.675s
user    20m52.432s
sys     0m8.767s

real    3m8.409s

```

and

```
time interleave-reads.py \
test1.fq.gz \
test2.fq.gz \
| skewer -Q 5 -t 8 -x adap.fa - -1 \
| bwa mem -p -t 8 Mya81-contigs.fa - \
| samtools view -F4 -Sb - \
| samtools sort -@ 8 -m 2G - clam.5kb

real    3m8.437s
user    21m8.484s
sys     0m8.294s

real    3m8.945s

```

and

```
time interleave-reads.py \
test1.fq.gz \
test2.fq.gz \
| skewer -Q 5 -t 8 -x adap.fa - -1 \
| extract-paired-reads.py -p - -s /dev/null - \
| bwa mem -p -t 8 Mya81-contigs.fa - \
| samtools view -F4 -Sub - \
| samtools sort -@ 8 -m 2G - clam.5kb

real    3m0.778s
user    20m19.470s
sys     0m8.953s

real    3m0.674s

```

**samtools 2**

```
time interleave-reads.py \
test1.fq.gz \
test2.fq.gz \
| skewer -Q 5 -t 8 -x adap.fa - -1 \
| extract-paired-reads.py -p - -s /dev/null - \
| bwa mem -p -t 8 Mya81-contigs.fa - \
| samtools view -F4 -Sub - \
| samtools sort-@ 8 -m 2G - clam.5kb


real    2m59.531s
user    19m47.312s
sys     0m8.291s

real    2m59.521s
```

and

```
time interleave-reads.py \
test1.fq.gz \
test2.fq.gz \
| skewer -Q 5 -t 8 -x adap.fa - -1 \
| extract-paired-reads.py -p - -s /dev/null - \
| bwa mem -p -t 8 Mya81-contigs.fa - \
| samtools view -T . -F4 -bu - \
| samtools sort -l 0 -O bam -T tmp -@ 8 -m 2G -o clam.5kb.bam - 

real    2m59.058s
real    2m59.645s
```

and

```
time interleave-reads.py \
test1.fq.gz \
test2.fq.gz \
| skewer -Q 5 -t 4 -x adap.fa - -1 \
| extract-paired-reads.py -p - -s /dev/null - \
| bwa mem -p -t 8 Mya81-contigs.fa - \
| samtools view -T . -F4 -bu - \
| samtools sort -l 0 -O bam -T tmp -@ 8 -m 2G -o clam.5kb.bam - 

real    2m56.753s
real    2m56.200s
real    2m55.993s

```









