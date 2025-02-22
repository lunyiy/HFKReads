# HFKReads
<b> An ultra-fast and efficient tool for high frequency kmer sequencing reads extraction</b>

##  1. Install
### (1) Pre-built binaries for x86_64 Linux
```
wget -c https://github.com/HuiyangYu/HFKReads/releases/download/v2.03/HFKReads-2.03-Linux-x86_64.tar.gz
tar zvxf HFKReads-2.03-Linux-x86_64.tar.gz
cd HFKReads-2.03-Linux-x86_64
./hfkreads -h
```
If the pre-built binaries are not functional, you need to install from the source code.
### (2) Building from source code （Linux or Mac）
```
git clone https://github.com/HuiyangYu/HFKReads.git
cd HFKReads
make
cd bin
./hfkreads -h
```
## 2. Usage
```
Usage: hfkreads -1 PE1.fq.gz -2 PE2.fq.gz -o OutPrefix
 Input/Output options:
   -1	<str>   paired-end fasta/q file1
   -2	<str>   paired-end fasta/q file2
   -s	<str>   single-end fasta/q file
   -o	<str>   prefix of output file
 Filter options:
   -b	<int>   min base quality [0]
   -q	<int>   min average base quality [20]
   -l	<int>   min length of read [half]
   -r	<float> max unknown base (N) ratio [0.1]
   -k	<int>   kmer length [31]
   -w	<int>   window size [10]
   -m	<int>   min count for high frequency kmer (HFK) [3] 
   -x	<float>	min ratio of HFK in the read [0.9]
   -n	<int>   read number to use [1000000]
   -a	        use all the read
 Other options:
   -d           drop the duplicated reads/pairs
   -f           output the kmer frequency file
   -A           keep base quality in output
   -t           number of threads [1]
   -h           show help [v2.03]
```
## 3. Example
### 3.1 Extracting high-frequency k-mer reads from paired-end sequencing reads
```
hfkreads -1 PE_1.fq.gz -2 PE_2.fq.gz -o test1
```
The output files consist of four files: <br>test1_pe_1.fa <br>test1_pe_2.fa <br>test1_se_1.fa <br>test1_se_2.fa <br>The output file with the 'se' label are unpaired high-frequency k-mer reads.

### 3.2 Extracting high-frequency k-mer reads from single-end sequencing reads
```
hfkreads -s SE.fq.gz -o test2
```
The output result consists of a single file named "test2.fa".

### 3.3 Extracting high-quality reads without filtering the k-mers
```
hfkreads -1 PE_1.fq.gz -2 PE_2.fq.gz -m 1 -o test3
hfkreads -s SE.fq.gz -m 1 -o test4
```
To filter out low-quality reads only, the default '-m 3' parameter should change to '-m 1'.

## 4. License
-------

This project is licensed under the GPL-3.0 license - see the [LICENSE](LICENSE) file for details
