# assignment-1

# 1) Get the data files 

To download the two files, I used the `curl` command, as the instructions specified, followed by `-O` to direct the files to a given location (my working directory). The file named "test.fastq.gz" needed to be unzipped with `gunzip` in order to be read using the `head` tool. I specified the number of lines to be printed using `head -n 5` which allowed me to print the first 5 lines from each file. The linked resources were used to help with [curl](https://curl.haxx.se/docs/manpage.html) and [head](https://stackoverflow.com/questions/20275072/read-first-x-lines-of-csv-into-new-outfile). 

```
@29154_superba.1 GRC13_0027_FC:4:1:12560:1179 length=74
TGCAGGAAGGAGATTTTCGNACGTAGTGNNNNNNNNNNNNNNGCCNTGGATNNANNNGTGTGCGTGAAGAANAN
+29154_superba.1 GRC13_0027_FC:4:1:12560:1179 length=74
IIIIIIIGIIIIIIFFFFF#EEFE<?################################################
@29154_superba.2 GRC13_0027_FC:4:1:15976:1183 length=74

5.1,3.5,1.4,0.2,Iris-setosa
4.9,3,1.4,0.2,Iris-setosa
4.7,3.2,1.3,0.2,Iris-setosa
4.6,3.1,1.5,0.2,Iris-setosa
5,3.6,1.4,0.2,Iris-setosa

```
Jessicas-Air:~ jessicahoch$ cd PDSB
Jessicas-Air:PDSB jessicahoch$ pwd
/Users/jessicahoch/PDSB
Jessicas-Air:PDSB jessicahoch$ curl -O http://eaton-lab.org/pdsb/iris-data-dirty.csv
Jessicas-Air:PDSB jessicahoch$ curl -O  http://eaton-lab.org/pdsb/test.fastq.gz
Jessicas-Air:PDSB jessicahoch$ zless test.fastq.gz
Jessicas-Air:PDSB jessicahoch$ zless iris-data-dirty.csv
Jessicas-Air:PDSB jessicahoch$ head -n 5 iris-data-dirty.csv
Jessicas-Air:PDSB jessicahoch$ gunzip test.fastq.gz
Jessicas-Air:PDSB jessicahoch$ head -n 5 test.fastq
```
