Feeding Final
--

on davinci

    /mnt/data3/macmanes/subsamp/100M_corr/raw.100M.SRR797058_1.fastq.gz
    /mnt/data3/macmanes/subsamp/100M_corr/raw.100M.SRR797058_2.fastq.gz
    /mnt/data3/macmanes/subsamp/20M_corr/raw.20M.SRR797058_1.fastq.gz
    /mnt/data3/macmanes/subsamp/20M_corr/raw.20M.SRR797058_2.fastq.gz
    /mnt/data3/macmanes/subsamp/10M_corr/raw.10M.SRR797058_1.fastq.gz
    /mnt/data3/macmanes/subsamp/10M_corr/raw.10M.SRR797058_2.fastq.gz
    /mnt/data3/macmanes/subsamp/50M_corr/raw.50M.SRR797058_1.fastq.gz
    /mnt/data3/macmanes/subsamp/50M_corr/raw.50M.SRR797058_2.fastq.gz
    


aws stuff

	sudo bash
	apt-get update
	apt-get -y upgrade
	apt-get -y install subversion tmux git curl bowtie libncurses5-dev samtools gcc make g++ python-dev unzip dh-autoreconf default-jre python-pip zlib1g-dev
	sudo apt-get update && sudo apt-get install python-software-properties
	sudo add-apt-repository ppa:ubuntu-on-ec2/ec2-tools
	sudo sed -i "/^# deb.*multiverse/ s/^# //" /etc/apt/sources.list
	apt-get install ec2-api-tools
	ec2-create-image -b "/dev/sdb=ephemeral0"
	

	git clone https://github.com/trinityrnaseq/trinityrnaseq.git

download data

	scp macmanes@davinci.unh.edu:/mnt/data3/macmanes/subsamp/10M_corr/raw.10M.SRR797058_*.fastq.gz .
	scp macmanes@davinci.unh.edu:/mnt/data3/macmanes/subsamp/20M_corr/raw.20M.SRR797058_*.fastq.gz .

	scp macmanes@davinci.unh.edu:/mnt/data3/macmanes/subsamp/100M_corr/raw.100M.SRR797058_*.fastq.gz .


on AWS 10M

    ~/trinityrnaseq/Trinity --seqType fq --max_memory 40G --trimmomatic \
        --left /mnt/raw.10M.SRR797058_1.fastq.gz  \
        --right /mnt/raw.10M.SRR797058_2.fastq.gz \
        --CPU 32 --output trinity_10M_raw

on AWS 20M

    ~/trinityrnaseq/Trinity --seqType fq --max_memory 40G --trimmomatic \
        --left /mnt/raw.20M.SRR797058_1.fastq.gz  \
        --right /mnt/raw.20M.SRR797058_2.fastq.gz \
        --CPU 32 --output trinity_20M_raw

        
100M

    ~/trinityrnaseq/Trinity --seqType fq --max_memory 40G --trimmomatic \
        --left /mnt/raw.100M.SRR797058_1.fastq.gz \
        --right /mnt/raw.100M.SRR797058_2.fastq.gz \
        --CPU 32 --output trinity_100M_raw


lets see if 100M run can work with 60Gb RAM...