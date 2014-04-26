setup new computer
--

	sudo chown -R macmanes /mnt/data0
	sudo chmod -R o+x /share
	
set whole system variables:

	sudo nano /etc/environment
	
needed for samtools
	
	sudo apt-get install libncurses5-dev