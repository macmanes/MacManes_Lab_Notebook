Pinky ABySS install
--
    sudo git clone https://github.com/bcgsc/abyss.git
    sudo ./autogen.sh
    sudo ./configure --enable-maxk=96  --with-mpi=/usr/lib/openmpi
    sudo make -j8
    sudo make all install