Mapping
--

---

**Install BWA**

```
cd $HOME
git clone https://github.com/lh3/bwa.git
cd bwa
make -j4
PATH=$PATH:$(pwd)
```

**Install SAMBAMBA**

```
cd $HOME
curl -LO https://github.com/lomereiter/sambamba/releases/download/v0.5.8/sambamba_v0.5.8_linux.tar.bz2
tar -jxf sambamba_v0.5.8_linux.tar.bz2
sudo mv sambamba_v0.5.8 /usr/bin/sambamba_v0.5.8
```

**Install SEQTK**

```
cd $HOME
git clone https://github.com/lh3/seqtk.git
cd seqtk
make
PATH=$PATH:$(pwd)
```

**Install SKEWER**

```
cd $HOME
curl -LO https://s3.amazonaws.com/macmanes_general/adapters.fa
git clone https://github.com/relipmoc/skewer.git
cd skewer
make
PATH=$PATH:$(pwd)
```

**DO THE MAPPING for each file**
This recipe trims using the Truseq adapters - if these libraries were made with a Nextera kit, you'll need to use those adapters. Your output file will not be named `schizo.bam` but instead something else. 


```
bwa index -p index Genome.fasta

time seqtk mergepe \
../Schizo.50M.left.fq.gz \
../Schizo.50M.right.fq.gz \
| skewer -Q 2 -t 16 -x $HOME/adapters.fa - -1 \
| bwa mem -p -t 16 index - \
| sambamba_v0.5.8 view -l 0 -t 16 -S -f bam -o /dev/stdout /dev/stdin \
| sambamba_v0.5.8 sort -l 0 -t 15 -m 15G -o schizo.bam /dev/stdin
```

**MAPPING STATS**

```
sambamba flagstat schizo.bam
```
