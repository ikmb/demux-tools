Bootstrap:docker
From:nfcore/base

%labels
    MAINTAINER Marc Hoeppner <m.hoeppner@ikmb.uni-kiel.de>
    DESCRIPTION Singularity image containing all requirements for the CCGA demux pipeline
    VERSION 1.0

%environment
    PATH=/opt/conda/envs/ikmb-demux-1.0/bin:/opt/cellranger-3.1.0:/opt/longranger-2.2.2:/opt/supernova-2.1.1:$PATH
    export PATH

    CPLUS_INCLUDE_PATH=/usr/include/x86_64-linux-gnu
    export CPLUS_INCLUDE_PATH

%files
    environment.yml /
    10x/cellranger-3.1.0.tar.gz /opt
    10x/longranger-2.2.2.tar.gz /opt
    10x/supernova-2.1.1.tar.gz /opt

%post

    /opt/conda/bin/conda env create -f /environment.yml
    /opt/conda/bin/conda clean -a

    mkdir -p /ifs
    apt-get -y update
    apt-get -y install procps make gcc unzip zlib1g-dev build-essential libc6-dev
    
    mkdir -p /usr/include/sys
    cd /usr/include/sys
    ln -s /usr/include/x86_64-linux-gnu/sys/stat.h

    # Install bcl2fastq
    mkdir -p /opt/bcl2fastq
    cd /opt/bcl2fastq
    wget ftp://webdata2:webdata2@ussd-ftp.illumina.com/downloads/software/bcl2fastq/bcl2fastq2-v2-20-0-tar.zip
    unzip bcl2fastq2-v2-20-0-tar.zip
    tar -xvf bcl2fastq2-v2.20.0.422-Source.tar.gz
    mv bcl2fastq source
    mkdir build
    cd build
    ../source/src/configure --prefix=/opt/bcl2fastq/2.20.0 LDFLAGS=-I/usr/include/x86_64-linux-gnu CFLAGS=-I/usr/include/x86_64-linux-gnu
    make install
    cd ..
    rm -Rf source build *.tar.gz *.zip
    echo 'export PATH=$PATH:/opt/bcl2fastq/2.20.0/bin' >> /environment

   # Get cell ranger    
   cd /opt
   tar -xvf cellranger-3.1.0.tar.gz
   rm cellranger*.tar.gz

   # Get Supernova
   cd /opt
   tar -xvf supernova-2.1.1.tar.gz
   rm supernova-2.1.1.tar.gz

   # Get Longranger
   cd /opt
   tar -xvf longranger-2.2.2.tar.gz 
   rm longranger-2.2.2.tar.gz
   
