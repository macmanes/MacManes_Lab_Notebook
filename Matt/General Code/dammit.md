dammit
--

```
sudo apt-get update && sudo apt-get upgrade

sudo apt-get -y install python-pip python-dev python-numpy git ruby hmmer unzip \
    infernal ncbi-blast+ liburi-escape-xs-perl emboss liburi-perl tmux \
    python-sklearn build-essential libsm6 libxrender1 libfontconfig1 \
    pkg-config libpng12-dev libfreetype6-dev libboost1.55-all-dev libboost1.55-dbg
```



```
cd
curl -LO https://github.com/TransDecoder/TransDecoder/archive/2.0.1.tar.gz
tar -xvzf 2.0.1.tar.gz
cd TransDecoder-2.0.1; make
export PATH=$PATH:$HOME/TransDecoder-2.0.1

cd
curl -LO http://last.cbrc.jp/last-658.zip
unzip last-658.zip
cd last-658
make
export PATH=$PATH:$HOME/last-658/src

cd
curl -LO http://busco.ezlab.org/files/BUSCO_v1.1b1.tar.gz
tar -zxf BUSCO_v1.1b1.tar.gz
cd BUSCO_v1.1b1
chmod +x BUSCO_v1.1b1.py
PATH=$PATH:$(pwd)

cd
curl -LO http://bioinf.uni-greifswald.de/augustus/binaries/old/augustus-3.0.2.tar.gz
tar -zxf augustus-3.0.2.tar.gz
cd augustus-3.0.2/
make
PATH=$PATH:$(pwd)/bin:$(pwd)/scripts
export AUGUSTUS_CONFIG_PATH=/home/ubuntu/augustus-3.0.2/config/
```

```
echo 'export PATH=$PATH:$HOME/TransDecoder-2.0.1' >> $HOME/.bashrc
echo 'export PATH=$PATH:$HOME/last-658/src' >> $HOME/.bashrc
echo 'export PATH=$PATH:$HOME/BUSCO_v1.1b1' >> $HOME/.bashrc
```

```
sudo gem install crb-blast
sudo pip install -U setuptools
sudo pip install numpy --upgrade
sudo pip install matplotlib --upgrade
sudo pip install dammit
```