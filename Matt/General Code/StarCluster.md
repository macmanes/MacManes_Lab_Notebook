Starcluster 
--

Make 14.04 AMI
--

```
sudo apt-get update
sudo apt-get upgrade
sudo apt-get install tmux libbz2-dev libmagic-dev git gcc make cmake ipython python-pip build-essential autoconf libtool pkg-config python-opengl python-imaging python-pyrex python-pyside.qtopengl idle-python2.7 qt4-dev-tools qt4-designer libqtgui4 libqtcore4 libqt4-xml libqt4-test libqt4-script libqt4-network libqt4-dbus python-qt4 python-qt4-gl libgle3 python-dev
```

Launch StarCluster 
--

```
starcluster createvolume 444 us-east-1c -n mya -m mkfs.ext4 --detach-volume
```

- add voluID to config file at `~/.starcluster/config`

```
starcluster start mycluster
starcluster sshmaster mycluster
```

```
sudo apt-get update
sudo apt-get upgrade
sudo apt-get install tmux libbz2-dev libmagic-dev git gcc make cmake ipython python-pip build-essential autoconf libtool pkg-config python-opengl python-imaging python-pyrex python-pyside.qtopengl idle-python2.7 qt4-dev-tools qt4-designer libqtgui4 libqtcore4 libqt4-xml libqt4-test libqt4-script libqt4-network libqt4-dbus python-qt4 python-qt4-gl libgle3 python-dev



wget http://star.mit.edu/media/uploads/cluster/downloads/starcluster-0.95.6.tar.gz
tar -zxf starcluster-0.95.6.tar.gz
cd StarCluster-0.95.6
sudo python distribute_setup.py
sudo python setup.py install


nano ~/.starcluster/config




[aws info]
aws_access_key_id = 
aws_secret_access_key = 
aws_user_id = 

[key mykey]
key_location = ~/.ssh/mykey.rsa


[cluster mediumcluster]
keyname = mykey
EXTENDS=smallcluster
NODE_INSTANCE_TYPE=m3.2xlarge
CLUSTER_SIZE=10
VOLUMES=mydata, myscripts 
```


```
starcluster createkey macmanes_starclust_key -o /home/macmanes/.ssh/mystarkey.rsa
```

```
starcluster start mycluster
starcluster sshmaster mycluster
logout
starcluster terminate mycluster


cd /genome
tmux new -s dl
wget https://s3.amazonaws.com/mya-genome/clam.longreads.fastq
nano config

git clone https://github.com/macmanes-lab/wgs-assembler.git
cd wgs-assembler/kmer
make install

```

```
merSize=14
mhap=-k 14 --num-hashes 1024 --pacbio_fast
useGrid=1
scriptOnGrid=1

ovlMemory=2
ovlStoreMemory=64000
threads=1
ovlConcurrency=96
cnsConcurrency=96
merylThreads=96
merylMemory=4000
ovlRefBlockSize=20000
frgCorrThreads = 96
frgCorrBatchSize = 100000
ovlCorrBatchSize = 100000

sgeScript = -pe orte 90
sgeConsensus = -pe orte 90
sgeOverlap = -pe orte 90
sgeCorrection = -pe orte 90
sgeFragmentCorrection = -pe orte 90
sgeOverlapCorrection = -pe orte 90
# relax overlap parameters
asmOvlErrorRate=0.10
asmUtgErrorRate=0.07
asmCgwErrorRate=0.10
asmCnsErrorRate=0.10
utgGraphErrorRate=0.07
utgGraphErrorLimit=3.25
utgMergeErrorRate=0.0825
utgMergeErrorLimit=5.25
asmOBT=0

```




starcluster listclusters volumecreator


```
PBcR -l Mya -s config \
-fastq clam.longreads.fastq.1 \
genomeSize=1000000000 \
sgeName=Mya "sge=-A Mya"


PBcR -l Mya_test -s config2 \
-fastq test.fq \
genomeSize=1000000000 \
sgeName=Mya "sge=-A Mya"

```

```
runCA -p Mya_asm -d Mya_asm -s config genomeSize=1000000000 \
sgeName=Mya "sge=-A Mya" Mya.frg
```