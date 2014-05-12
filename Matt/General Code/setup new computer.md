setup new computer
--

	sudo chown -R macmanes /mnt/data0
	sudo chmod -R o+x /share
	
set whole system variables:

	sudo nano /etc/environment
	
needed for samtools
	
	sudo apt-get install libncurses5-dev
	
new users

	sudo adduser --home /mnt/data2/lesser lesser
	sudo adduser --home /mnt/data1/walker walker
	sudo adduser --home /mnt/data0/lah lah
	
raid array not showing up:

	 *-disk
       description: SCSI Disk
       product: MR9286-8e
       vendor: LSI
       physical id: 2.0.0
       bus info: scsi@0:2.0.0
       logical name: /dev/sda
       version: 3.34
       serial: 00de7bad1225bdd91ac01f2407b00506
       size: 32TiB (36TB)
       capabilities: gpt-1.00 partitioned partitioned:gpt
       configuration: ansiversion=5 guid=c4cbfa78-d8c4-4d30-a560-97a972062144 sectorsize=4096
       
seems to be there, but:

	Filesystem     Type      Size  Used Avail Use% Mounted on
	/dev/sdb2      ext4       46G  8.7G   35G  20% /
	none           tmpfs     4.0K     0  4.0K   0% /sys/fs/cgroup
	udev           devtmpfs  252G  4.0K  252G   1% /dev
	tmpfs          tmpfs      51G  864K   51G   1% /run
	none           tmpfs     5.0M     0  5.0M   0% /run/lock
	none           tmpfs     252G     0  252G   0% /run/shm
	none           tmpfs     100M     0  100M   0% /run/user
	/dev/sdb5      ext4       46G  2.6G   41G   6% /tmp
	/dev/sdb1      ext2      461M   65M  373M  15% /boot
	/dev/sdb6      ext4      369G  114G  237G  33% /home
	/dev/sdc1      ext4      469G  5.4G  440G   2% /mnt/data0
	/dev/sdd1      ext4      469G   70M  445G   1% /mnt/data1
	/dev/sde1      ext4      469G   70M  445G   1% /mnt/data2
	
Doh, drive was commented out in fstab
--

for transferring files:

	scp -r pero-genome/ macmanes@132.177.114.158:/mnt/data3/macmanes
	
Mounting USB drive
	
	sudo fdisk -l # to see where USB drive is located.
	sudo mount -t ext4 /dev/sde /media/external
	mv /media/external/pero_genome/ /mnt/data3/macmanes/ # for instance
	

SGA

	./configure --with-sparsehash=/share \
	--with-bamtools=/share/bamtools \
	--with-jemalloc=share/lib --prefix=/share
	make -j12
	make all install
	
AMOS

WARNING! nucmer was not found but is required to run AMOScmp and minimus2
   install nucmer if planning on using these programs
WARNING! delta-filter was not found but is required to run AMOScmp-shortReads-alignmentTrimmed
   install delta-filter if planning on using AMOScmp-shortReads-alignmentTrimmed
WARNING! show-coords was not found but is required to run minimus2
   install show-coords if planning on using minimus2
WARNING! BLAT was not found but is required to run minimus2-blat
   install BLAT if planning on using minimus2-blat
WARNING! Qt4 toolkit malfunctioning but is required to run AMOS GUIs
   try compiling GUIs manually or reinstall Qt4 toolkit to build GUIs
   see config.log for more information on what went wrong
WARNING! Statistics::Descriptive Perl module was not found but is required to run some AMOS scripts