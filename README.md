# 16S tutorial - METABARCODING (Using QIIME2)
>[!WARNING]
>This tutorial will work with a Unix Terminal, please make sure you are using linux :penguin: or apple :apple: OS

## Table of Contentents



## Data Knowledge

During your work with paired-end sequenced data you will see primarly two types of files EMP or Casava
You can differenciate them by the name of the files to work with.

**EMP** files are labeled as ```forward.fastq.gz```, ```reverse.fastq.gz``` and ```barcodes.fastq.gz```; while **Casava** files are labeled as ```L25357_15_L001__R1_001.fastq.gz``` and ```L25357_15_L001__R1_002.fastq.gz```
.

In Casava ```R1``` and ```R2``` stand for forward and reverse, while the other part of the name in order refers to: ```sample identifier (L25357)```, ```barcode identifier (15)```, ```lane number (L001)``` ```and the set number (001)```

## Installation of QIIME2

>[!NOTE]
>It is important for you that the package QIIME2 is pronounced as _"Shyme2"_ this could be important when talking with other colleagues :smile:

For installing the QIIME2 package please go to their website and follow the stablished protocols.[LINK]()

If you are having problems with the installation try to install it using a conda environment (python=3.8)

```Bash
conda install -c qiime2 qiime2
```

You can also install it using ```Docker``` (you will see all the information regarding this installation in the same link above). But remember that you will always need to execute the commands with:
```Bash
docker run -t -i -v $(pwd):/data quay.io/qiime2/core:2023.7 qiime <whatever_follows>
```

## Import Demultiplexed data

EMP paire-end reads are multiplexed (you have only one forward and one reverse fastq.gz file containing raw data for all of your samples) and therefore we need to **demultiplex** them.
>[!IMPORTANT]
>make sure you are working in an empty directory that only contains the 3 EMP files ```forward.fastq.gz```, ```reverse.fastq.gz``` and ```barcodes.fastq.gz```

```Bash
mkdir <EMP_directory>
qiime tools import --type EMPPairedEndSequences --input-path <EMP_directory> \
  --output-path emp-paired-end-sequences.qza
```

Casava files instead are already demultiplexed, for importing the data we should use another command

```Bash
mkdir <Casava_directory>
tools import --type 'SampleData[PairedEndSequencesWithQuality]' --input-path <Casava_directory> \
  --input-format CasavaOneEightSingleLanePerSampleDirFmt --output-path demux-paired-end.qza
```
