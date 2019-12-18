Bootstrap:docker
From:nfcore/base

%labels
    MAINTAINER Marc Hoeppner <m.hoeppner@ikmb.uni-kiel.de>
    DESCRIPTION Singularity image containing all requirements for the CCGA demux pipeline
    VERSION 1.1

%environment
    PATH=/opt/conda/envs/ikmb-demux-1.0/bin:/opt/cellranger-3.1.0:/opt/longranger-2.2.2:/opt/supernova-2.1.1:/opt/spaceranger-1.0.0:/opt/cellranger-atac-1.2.0:/opt/bcl2fastq/2.20.0/bin:$PATH
    export PATH

    CPLUS_INCLUDE_PATH=/usr/include/x86_64-linux-gnu
    export CPLUS_INCLUDE_PATH

%files
    environment.yml /
%post

    mkdir -p /ifs
    apt-get -y update
    apt-get -y install procps make gcc unzip zlib1g-dev build-essential libc6-dev wget

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
    make -j4 install
    cd ..
    rm -Rf source build *.tar.gz *.zip

    # Get CellRanger ATAC
    cd /opt
    wget -O cellranger-atac-1.2.0.tar.gz "http://cf.10xgenomics.com/releases/cell-atac/cellranger-atac-1.2.0.tar.gz?Expires=1576711332&Policy=eyJTdGF0ZW1lbnQiO$
    tar -xvf cellranger-atac-1.2.0.tar.gz
    rm cellranger-atac-1.2.0.tar.gz

   # Get cell ranger    
   cd /opt
   wget wget -O cellranger-3.1.0.tar.gz "http://cf.10xgenomics.com/releases/cell-exp/cellranger-3.1.0.tar.gz?Expires=1576711236&Policy=eyJTdGF0ZW1lbnQiOlt7IlJlc291cmNlIjoiaHR0cDovL2NmLjEweGdlbm9taWNzLmNvbS9yZWxlYXNlcy9jZWxsLWV4cC9jZWxscmFuZ2VyLTMuMS4wLnRhci5neiIsIkNvbmRpdGlvbiI6eyJEYXRlTGVzc1RoYW4iOnsiQVdTOkVwb2NoVGltZSI6MTU3NjcxMTIzNn19fV19&Signature=QWIpKVBb9WQLi-6y8a8hXN8fFln1qehzTge9i9yTfKbhx34LQMFspzeVRAX7Jwjw93wOp26qLtC8PRt~~TH6STE8tA9Jam1NdegDRjVlQ4UuM~icynhPIpy3-y0pPW8W1WfF9sgw9S8EgHxIVK~VeFXPWqHrzfFQ73oWh-aVlEZWSsdseuQlLReNqD~8I3-en0I~B6yeyh8NR5kf5A8-b5kHj8~p3Mb6M350diXEj~2~i2beGHoEoVgPc5YRPN1if26wGJvJwDH6SwA8zn70uhmFvw8eM2ue81UfApi1ujoI3HZ-D3bWaMQg2rIFUv5SKuqocbL3hcy8W2idd0rdDg__&Key-Pair-Id=APKAI7S6A5RYOXBWRPDA"
   tar -xvf cellranger-3.1.0.tar.gz
   rm cellranger*.tar.gz

   # Get Supernova
   cd /opt
   wget wget -O supernova-2.1.1.tar.gz "http://cf.10xgenomics.com/releases/assembly/supernova-2.1.1.tar.gz?Expires=1576711280&Policy=eyJTdGF0ZW1lbnQiOlt7IlJlc291cmNlIjoiaHR0cDovL2NmLjEweGdlbm9taWNzLmNvbS9yZWxlYXNlcy9hc3NlbWJseS9zdXBlcm5vdmEtMi4xLjEudGFyLmd6IiwiQ29uZGl0aW9uIjp7IkRhdGVMZXNzVGhhbiI6eyJBV1M6RXBvY2hUaW1lIjoxNTc2NzExMjgwfX19XX0_&Signature=MUcIQm3X4EnJiysWHp7cMn4Gqd3gDDkbcX3nMYnIGr1ZhchHAmEoghtst70NRA7ibXzlC7PSIMIMIkvF5etuwjeY~uGMHZeuCgWYbY4b3g~uMoCPQF4o9WeQPNlxj6~Sq5aAqvgIb79GV6Wk3s-IYFlHgGAaYU5X35QHCjiRqJuND4wNHIMN1HHqMNA~czbWY8DyuA-ArpkZgZDqj9KFQNPBGxW2rBCJATPEeGOEieydOFBw5CwkPwFJNTCK7D26Pem1w6OUug1amTCxRLm8BJclr2KBQdFWPmWncZwwWXO6Pv-16eqYRMKf~mCwdyEoTZ-B5z~5Tk8uyIe0rc~y3w__&Key-Pair-Id=APKAI7S6A5RYOXBWRPDA"
   tar -xvf supernova-2.1.1.tar.gz
   rm supernova-2.1.1.tar.gz

   # Get Longranger
   cd /opt
   wget -O longranger-2.2.2.tar.gz "http://cf.10xgenomics.com/releases/genome/longranger-2.2.2.tar.gz?Expires=1576711297&Policy=eyJTdGF0ZW1lbnQiOlt7IlJlc291cmNlIjoiaHR0cDovL2NmLjEweGdlbm9taWNzLmNvbS9yZWxlYXNlcy9nZW5vbWUvbG9uZ3Jhbmdlci0yLjIuMi50YXIuZ3oiLCJDb25kaXRpb24iOnsiRGF0ZUxlc3NUaGFuIjp7IkFXUzpFcG9jaFRpbWUiOjE1NzY3MTEyOTd9fX1dfQ__&Signature=fwDF75~A2MRfuRwDHp4OV9Tg3yDN3Fih6Icf7O6aCEL-GC0qA5mA0BWwT975FTc6lBmEaLVX8U8ClmdJxfNRjw1ccTwg4FLJpqK1tNhfVaxPItcSLmdeHmIi6H7xi5vaS6YTpcO7bMUIvvBoiqAUapcXGW-sbDiGKkyxu4dqZBBceM-Y-4UShA3K~QllZvG~dLLR3Pr5nZOm1CbA0cCM7ri0VuDiil9NPRv7VKnCR6u0ZJk5B4dEvbAijtbCPXHp~ul71QoxWjfY-ISXAD49nm1KiQAOX9hq2xBOLckAELpFIMmiT67~urT7D29z0libFAXNREn6eBa5BDvwPWO02g__&Key-Pair-Id=APKAI7S6A5RYOXBWRPDA"
   tar -xvf longranger-2.2.2.tar.gz 
   rm longranger-2.2.2.tar.gz
   
   # Get SpaceRanger
   cd /opt
   wget -O spaceranger-1.0.0.tar.gz "http://cf.10xgenomics.com/releases/spatial-exp/spaceranger-1.0.0.tar.gz?Expires=1576711312&Policy=eyJTdGF0ZW1lbnQiOlt7IlJlc291cmNlIjoiaHR0cDovL2NmLjEweGdlbm9taWNzLmNvbS9yZWxlYXNlcy9zcGF0aWFsLWV4cC9zcGFjZXJhbmdlci0xLjAuMC50YXIuZ3oiLCJDb25kaXRpb24iOnsiRGF0ZUxlc3NUaGFuIjp7IkFXUzpFcG9jaFRpbWUiOjE1NzY3MTEzMTJ9fX1dfQ__&Signature=GPa9eywJnEqgwp0Cdo8MZTcy9EIXQld~WITf7ftR6RubgFoNz13-cdmmpEnLobUpZiiWZQc9-olbPDF7Pu71RVXqg9aHtlFLiQdmevPIDiJga7pZWFl7oinFs-JrG8V7Z~GcDGpGvlnoPGvxCcpLVRe3g85JpwLsGXJwvCaNov8MQDwOgYS37zu8mNWTATsFyg9MxUA8IRSEXPyp61dKULf~yUqm5zf5NIykGdgYftXip3omdM-99QCDs9kV~-KHFwYFOG1TUlg4ob-2WFMuKLlUy8CaZ-KK~ZnQDrDh5rKB8PdSguBxcI5UpsdcDGaahFWWeKfDpUcdWD991wZJVg__&Key-Pair-Id=APKAI7S6A5RYOXBWRPDA"
   tar -xvf spaceranger-1.0.0.tar.gz
   rm spaceranger-1.0.0.tar.gz
 
