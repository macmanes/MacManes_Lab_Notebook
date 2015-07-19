Starcluster 
--

>>> Mounting EBS volume vol-1ef26cf4 on /genome...
!!! ERROR - Error occured while running plugin 'starcluster.clustersetup.DefaultClusterSetup':
!!! ERROR - remote command 'source /etc/profile && mount /genome' failed
!!! ERROR - with status 32:
!!! ERROR - mount: block device /dev/xvdz is write-protected, mounting
!!! ERROR - read-only
!!! ERROR - mount: you must specify the filesystem type


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
aws_access_key_id = AKIAJQYKA3447MYIHETA
aws_secret_access_key = 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
aws_user_id = 705503817198

[key mykey]
key_location = ~/.ssh/mykey.rsa


[cluster mediumcluster]
keyname = mykey
EXTENDS=smallcluster
NODE_INSTANCE_TYPE=m3.2xlarge
CLUSTER_SIZE=10
VOLUMES=mydata, myscripts 
```



starcluster createkey mykey -o ~/.ssh/mykey.rsa

```
starcluster start mycluster
starcluster sshmaster mycluster
logout
starcluster terminate mycluster


cd /mnt
tmux new -s dl
wget https://s3.amazonaws.com/mya-genome/clam.longreads.fastq
nano config

git clone https://github.com/macmanes-lab/wgs-assembler.git
cd wgs-assembler/kmer
make install

```

```
merSize=14
mhap=-k 14 -num-hashes 1024 -pacbio_fast
useGrid=1
scriptOnGrid=1

ovlMemory=64
ovlStoreMemory=64000
threads=96
ovlConcurrency=96
cnsConcurrency=90
merylThreads=90
merylMemory=32000
ovlRefBlockSize=20000
frgCorrThreads = 90
frgCorrBatchSize = 100000
ovlCorrBatchSize = 100000

sgeScript = -pe threads 90
sgeConsensus = -pe threads 90
sgeOverlap = -pe threads 90 -l mem=2GB
sgeCorrection = -pe threads 90 -l mem=2GB
sgeFragmentCorrection = -pe threads 90 -l mem=2GB
sgeOverlapCorrection = -pe threads 90 -l mem=16GB
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


starcluster createvolume 555 us-east-1c -n mya -m mkfs.ext4 --detach-volume

starcluster listclusters volumecreator