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

# 2) Clean the data 

Use grep, uniq, sed. Check that all of the species names are spelled correctly in the file iris-data-dirty.csv. Also check for missing values stored as NA. Create a new file where mispelled names are replaced with the correct values, and lines with NA are excluded, and save it as iris-data-clean.csv. Use cut, sort and uniq to list the number of data values there are for each species in the new cleaned data file.

To check that all the species names were spelled correctly, I sorted iris-data-dirty.csv with 'sort' and looked at the unique values with 'uniq.' From here, after seeing the incorrect spellings, I used 

```
5.1,3.5,1.4,0.2,Iris-setosa
4.9,3.0,1.4,0.2,Iris-setosa
4.7,3.2,1.3,0.2,Iris-setosa
4.6,3.1,1.5,0.2,Iris-setosa
5.0,3.6,1.4,0.2,Iris-setosa
5.4,3.9,1.7,0.4,Iris-setosa
4.6,3.4,1.4,0.3,Iris-setosa
5.0,3.4,1.5,0.2,Iris-setosa
4.4,2.9,1.4,0.2,Iris-setosa
4.9,3.1,1.5,0.1,Iris-setosa
5.4,3.7,1.5,0.2,Iris-setosa
4.8,3.4,1.6,0.2,Iris-setosa
4.8,3.0,1.4,0.1,Iris-setosa
4.3,3.0,1.1,0.1,Iris-setosa
5.8,4.0,1.2,0.2,Iris-setosa
5.7,4.4,1.5,0.4,Iris-setosa
5.4,3.9,1.3,0.4,Iris-setosa
5.1,3.5,1.4,0.3,Iris-setosa
5.7,3.8,1.7,0.3,Iris-setosa
5.1,3.8,1.5,0.3,Iris-setosa
5.4,3.4,1.7,0.2,Iris-setosa
5.1,3.7,1.5,0.4,Iris-setosa
4.6,3.6,1.0,0.2,Iris-setosa
5.1,3.3,1.7,0.5,Iris-setosa
4.8,3.4,1.9,0.2,Iris-setosa
5.0,3.0,1.6,0.2,Iris-setosa
5.0,3.4,1.6,0.4,Iris-setosa
5.2,3.5,1.5,0.2,Iris-setosa
5.2,3.4,1.4,0.2,Iris-setosa
4.7,3.2,1.6,0.2,Iris-setosa
4.8,3.1,1.6,0.2,Iris-setosa
5.4,3.4,1.5,0.4,Iris-setosa
5.2,4.1,1.5,0.1,Iris-setosa
5.5,4.2,1.4,0.2,Iris-setosa
4.9,3.1,1.5,0.1,Iris-setosa
5.0,3.2,1.2,0.2,Iris-setosa
5.5,3.5,1.3,0.2,Iris-setosa
4.9,3.1,1.5,0.1,Iris-setosa
4.4,3.0,1.3,0.2,Iris-setosa
5.1,3.4,1.5,0.2,Iris-setosa
5.0,3.5,1.3,0.3,Iris-setosa
4.5,2.3,1.3,0.3,Iris-setosa
4.4,3.2,1.3,0.2,Iris-setosa
5.0,3.5,1.6,0.6,Iris-setosa
5.1,3.8,1.9,0.4,Iris-setosa
4.8,3.0,1.4,0.3,Iris-setosa
5.1,3.8,1.6,0.2,Iris-setosa
4.6,3.2,1.4,0.2,Iris-setosa
5.3,3.7,1.5,0.2,Iris-setosa
5.0,3.3,1.4,0.2,Iris-setosa
7.0,3.2,4.7,1.4,Iris-versicolor
6.4,3.2,4.5,1.5,Iris-versicolor
6.9,3.1,4.9,1.5,Iris-versicolor
5.5,2.3,4.0,1.3,Iris-versicolor
6.5,2.8,4.6,1.5,Iris-versicolor
5.7,2.8,4.5,1.3,Iris-versicolor
6.3,3.3,4.7,1.6,Iris-versicolor
4.9,2.4,3.3,1.0,Iris-versicolor
6.6,2.9,4.6,1.3,Iris-versicolor
5.2,2.7,3.9,1.4,Iris-versicolor
5.0,2.0,3.5,1.0,Iris-versicolor
5.9,3.0,4.2,1.5,Iris-versicolor
6.0,2.2,4.0,1.0,Iris-versicolor
6.1,2.9,4.7,1.4,Iris-versicolor
5.6,2.9,3.6,1.3,Iris-versicolor
6.7,3.1,4.4,1.4,Iris-versicolor
5.6,3.0,4.5,1.5,Iris-versicolor
5.8,2.7,4.1,1.0,Iris-versicolor
6.2,2.2,4.5,1.5,Iris-versicolor
5.6,2.5,3.9,1.1,Iris-versicolor
5.9,3.2,4.8,1.8,Iris-versicolor
6.1,2.8,4.0,1.3,Iris-versicolor
6.1,2.8,4.7,1.2,Iris-versicolor
6.4,2.9,4.3,1.3,Iris-versicolor
6.6,3.0,4.4,1.4,Iris-versicolor
6.8,2.8,4.8,1.4,Iris-versicolor
6.7,3.0,5.0,1.7,Iris-versicolor
6.0,2.9,4.5,1.5,Iris-versicolor
5.7,2.6,3.5,1.0,Iris-versicolor
5.5,2.4,3.8,1.1,Iris-versicolor
5.5,2.4,3.7,1.0,Iris-versicolor
5.8,2.7,3.9,1.2,Iris-versicolor
6.0,2.7,5.1,1.6,Iris-versicolor
5.4,3.0,4.5,1.5,Iris-versicolor
6.0,3.4,4.5,1.6,Iris-versicolor
6.7,3.1,4.7,1.5,Iris-versicolor
6.3,2.3,4.4,1.3,Iris-versicolor
5.5,2.5,4.0,1.3,Iris-versicolor
5.5,2.6,4.4,1.2,Iris-versicolor
6.1,3.0,4.6,1.4,Iris-versicolor
5.8,2.6,4.0,1.2,Iris-versicolor
5.0,2.3,3.3,1.0,Iris-versicolor
5.6,2.7,4.2,1.3,Iris-versicolor
5.7,3.0,4.2,1.2,Iris-versicolor
5.7,2.9,4.2,1.3,Iris-versicolor
6.2,2.9,4.3,1.3,Iris-versicolor
5.1,2.5,3.0,1.1,Iris-versicolor
5.7,2.8,4.1,1.3,Iris-versicolor
6.3,3.3,6.0,2.5,Iris-virginica
5.8,2.7,5.1,1.9,Iris-virginica
7.1,3.0,5.9,2.1,Iris-virginica
6.3,2.9,5.6,1.8,Iris-virginica
6.5,3.0,5.8,2.2,Iris-virginica
7.6,3.0,6.6,2.1,Iris-virginica
4.9,2.5,4.5,1.7,Iris-virginica
7.3,2.9,6.3,1.8,Iris-virginica
6.7,2.5,5.8,1.8,Iris-virginica
7.2,3.6,6.1,2.5,Iris-virginica
6.5,3.2,5.1,2.0,Iris-virginica
6.4,2.7,5.3,1.9,Iris-virginica
6.8,3.0,5.5,2.1,Iris-virginica
5.7,2.5,5.0,2.0,Iris-virginica
5.8,2.8,5.1,2.4,Iris-virginica
6.4,3.2,5.3,2.3,Iris-virginica
6.5,3.0,5.5,1.8,Iris-virginica
7.7,3.8,6.7,2.2,Iris-virginica
7.7,2.6,6.9,2.3,Iris-virginica
6.0,2.2,5.0,1.5,Iris-virginica
6.9,3.2,5.7,2.3,Iris-virginica
5.6,2.8,4.9,2.0,Iris-virginica
7.7,2.8,6.7,2.0,Iris-virginica
6.3,2.7,4.9,1.8,Iris-virginica
6.7,3.3,5.7,2.1,Iris-virginica
7.2,3.2,6.0,1.8,Iris-virginica
6.2,2.8,4.8,1.8,Iris-virginica
6.1,3.0,4.9,1.8,Iris-virginica
6.4,2.8,5.6,2.1,Iris-virginica
7.2,3.0,5.8,1.6,Iris-virginica
7.4,2.8,6.1,1.9,Iris-virginica
7.9,3.8,6.4,2.0,Iris-virginica
6.4,2.8,5.6,2.2,Iris-virginica
6.3,2.8,5.1,1.5,Iris-virginica
6.1,2.6,5.6,1.4,Iris-virginica
7.7,3.0,6.1,2.3,Iris-virginica
6.3,3.4,5.6,2.4,Iris-virginica
6.4,3.1,5.5,1.8,Iris-virginica
6.0,3.0,4.8,1.8,Iris-virginica
6.9,3.1,5.4,2.1,Iris-virginica
6.7,3.1,5.6,2.4,Iris-virginica
6.9,3.1,5.1,2.3,Iris-virginica
5.8,2.7,5.1,1.9,Iris-virginica
6.8,3.2,5.9,2.3,Iris-virginica
6.7,3.3,5.7,2.5,Iris-virginica
6.7,3.0,5.2,2.3,Iris-virginica
6.3,2.5,5.0,1.9,Iris-virginica
6.5,3.0,5.2,2.0,Iris-virginica
6.2,3.4,5.4,2.3,Iris-virginica
5.9,3.0,5.1,1.8,Iris-virginica
```






```
dyn-160-39-253-132:PDSB jessicahoch$ sort -t, -k5 iris-data-dirty.csv > sorted.csv
dyn-160-39-253-132:PDSB jessicahoch$ sort -u -t, -k5 sorted.csv > uniq.csv
dyn-160-39-253-132:PDSB jessicahoch$ cat uniq.csv
dyn-160-39-253-132:PDSB jessicahoch$ sed 's/Iris-setsa/Iris-setosa/g' iris-data-dirty.csv > iris-data-1.csv
dyn-160-39-253-132:PDSB jessicahoch$ sed 's/Iris-versicolour/Iris-versicolor/g' iris-data-1.csv > iris-data-2.csv 
dyn-160-39-253-132:PDSB jessicahoch$ cat iris-data-2.csv 
dyn-160-39-253-132:PDSB jessicahoch$ sed '/NA/d' iris-data-2.csv > iris-data-clean.csv
```



# 3) Summarize sequence data file 

Find how many lines in the data file test.fastq.gz start with "TGCAG" and end with "GAG" 

To find how many lines of the data file test.fastq start with "TCGAG," I used `grep` and "^" to indicate the beginning of the line, followed by the characters. To find how many lines end with "GAG," I used `grep` and "$" after the end of the line characters. I returned the output to a new file (summ.txt) and used `cat` followed by `-n` to find the number of rows. The linekd resources were used to figure out how to use `grep` with the [beginning](https://askubuntu.com/questions/639157/grep-beginning-of-line) and [end](http://uniforumchicago.org/slides/regexp/tsld016.htm) of a line. 

```
     1	TGCAGCAAGTAAAGGGCCGAGGGACCGGCCCGAGAGACGACGTCCTGGCGGAGTGCTGTTTGGTGATGGAGGAG
     2	TGCAGCAAGATAAAACACGTTGTGAAGAGAGCAGAAACACACACACAGACCAGCAACGCAAGAGAGTTCGGGAG
     3	TGCAGGTCTAAATAAAGGTTTAGCAAAACTTGATGAAATCCTAGCTCAAAGCTTTCCTGACTCAACCAAGAGAG
     4	TGCAGGGCGCAGAGGGAGAGGCAGCAGGAAGCTCAGGGGCATAGGAGGGGTGGGCTGTCGGGAAAGGGCCTGAG
     5	TGCAGTTCGATGCGCCGATCAAGACGCAGGCACTGGCCCAGATGATGGGCAATACGACCGGCTACCGGATCGAG
     6	TGCAGATGAGATAATCGACAATGTCGATATACCCGTTCGCTGAAGCCATGTGTAATGCTGGAAAATTACATGAG
     7	TGCAGCGCCGTGTCCTCCGCGTTGTTCTTGGCCACGCACCAGAGCTGGTTCCCTTGGGCGGAGACGAGAGAGAG
     8	TGCAGACTCCGCACTCGAAGGCGCGTCCTCCGGCGGTCATGGAGGCGGCGGCCCCGCCCCCCCGAGACGGGGAG
     9	TGCAGGCCGACTTTAGGGAAGTGTCTTTGTTTGAACTGCCCAGCAAACCGGACTGGATCGGCGGAGCAGACGAG
    10	TGCAGACTCCTAATTGAATCTAACAAAAAGAAGCGAGAAAATTGTGCTTACCAACGACGGGTGCCGAACAAGAG
    11	TGCAGGAAATCCTCGTTGCGTCGATTGCGTGGAACAAAAACCACGACATCACCGGTGGACTGGTCTGCGTGGAG
    12	TGCAGAGGCGGCATACCATCAGCGCTTTGGTTTCGAGAGGCGGGAGGGGGGTGGCCAAACCGCTACAAAGGGAG
    13	TGCAGCTGGAGCTTCGGGCCGCAATGGTTAATACGTGGAGGAACGGGACGTAGGGGATGTCTTTCGAGGATGAG
    14	TGCAGCTAGCCAAAGAAATTAATAAAGCCTTGCGCGTACCGCACGATGTGAAAATGCAGCTGGGGCTGCTGGAG
    15	TGCAGTTGTTGAAGTTATGGTTGGAAATTCGAGTTCCAGTAATTGTTCTTCAGGAAAACTTTTCACATGGGGAG
    16	TGCAGCGTATCCCGACACGACGGCGGGAGCGGCTAAGATGACTGATATGGGGGGAGGGGCAGAAGCTGTGTGAG
    17	TGCAGTTATCAGATGAACGCGTTCGCAATGTTCAACTCTAACAGCCTGTTGAGACAATTATTTAGGCATATGAG
    18	TGCAGGGGTCTTCTTTCCGACACACGTTTGAAGCAGCAAGAAATGAATAATAATGATGATATTGAAGCAATGAG
    19	TGCAGCTTGCCGGCAAGCAGGAGCGCGAGAACCGCATCGACGAGATCAAGGCTTCGGTCAAGGCCGACCTCGAG
    20	TGCAGCTTGGAACTATTGTTGTTGTTGTTGAACAGAGACGGTGGGATGTTGCCCGAGAAGGTGTTGTTTCTGAG
    21	TGCAGATCGCCCCAACACACCATTTCTTCCCAACAGCTTCACCCCGGGATTGTCGATAAGGTATCTCACCTGAG
    22	TGCAGACCGATAAGATCTGGACCGGCCGGCTCCGCGTCGTCTCTTGCGCTTCCCGGTGCGAGATCCGGCTCGAG
    23	TGCAGAAAACACATTTTTGTCAAACGTTGGCTGAAAAACATGGACTTACTTGTTAATGCTTAGTAGGACAAGAG
    24	TGCAGAGACTAAAGATCATCGAGCAGGAGATCAGAGACGTGAAGCAGGAGATTCAAGGTCTGAGATACTACGAG
    25	TGCAGAAACCAAGGGGACAAAAAATTGCTGCGGTGAGGTGTACTGTTACTGAGTGCACTTTGAGCCCTTGTGAG
    26	TGCAGCTGATACTCAAGTTGATTTGTCATGGCAGATGACTCTTCAGAAATTATGGGAAAGCCTCAGTCCTGGAG
    27	TGCAGCTCACCAGGTGGCTCTAGGTTCTCTAAAACTGTCTCCAGGGGCTTTGACAGTGTCCAGTGGGCTCTGAG
    28	TGCAGATTTTTTTTGCTGAAGAAGTGCTTTGAAGTTTAGATAACAACCAACTTCTAAACTAAATACAAAAGGAG
    29	TGCAGGCCGCTGAGTTTCGCGCCCTCGTCGAGGCCGATGAGCGGGACGCCCTGGGTGGCCCGGCCGAGTTCGAG
    30	TGCAGAGGGATGACACTTGAAGGGGGAAGAAGGATGGTCTTTGAAAGGGGATATCTTGAAGGGTCTTCAAAGAG
    31	TGCAGATGATCGCCACGGGCGAGGAGGTGAACCGCGTTCCCGACATGCTGATGCGCGCGGCCGAGCTGCACGAG
    32	TGCAGATGACCTGGATCTTCCTGAACCAACTCANNAAATTTGAGAAAACTATTGGATTATAATTCTTACTGGAG
    33	TGCAGACAACGATAATTCATTTGAAAAAAGAACAAAAAAAAAATCGATCAACCACATTTTTATAGGAATAGGAG
    34	TGCAGCTAAGAAACCTCCTGAGTTTGAAGAATTTGGAAAAGATGAAAAAGTTGAGGAACTTGGAGAACCTGGAG
    35	TGCAGCATGCTACGTATTGTCATCTCATGGTTGCAAGGCTTTACAAAACTGGCTTCCACCTACTCCTGTCAGAG
    36	TGCAGAGAAAATGCTACAAATAATGAAGAAACTTTACTGGAGCAGGAGGCATTGGAGGTGAATGGAAGAGAGAG
    37	TGCAGCCCTCGATTATATAATCTCTATAGAAAGTGACATTTTCGTTCCCTCCCATTCTGGTAACATGGCAAGAG
    38	TGCAGTACAAAAAGACCGGTGTGAAAGATGCAGGGATTGATAAAGGCAGCACAAAACTGGCCACATTGAAAGAG
    39	TGCAGAGGGCGCATCAGAAAGGGGTTAGTTTTTCTTTTTTCTTTAGTCCGTTTTGGGTTTTTAAGATTATGGAG
    40	TGCAGGGTTATCTAGAAGTACTTTGATAGGGAAATTGCCCGCCTTAGTTATGGCTGCTTCCAGGGCTTTGAGAG
    41	TGCAGGATCAAGCCATTCAACAGCAGGATACAAACATTGTGAGGCTTTATGCAAAATCTGCCGCATACCTTGAG
    42	TGCAGACTGTCGAGGGCAACGCTAATGTCCGAGTAGACCTCGTCGATAGACTTGCTCGAGTTGATCTGTTGGAG
    43	TGCAGCAGACCGATTTCCTCCTTTACTCTCCTCAAGTGCCTTTTGTCTGTGTCTTTGATAGCTTTCGCACTGAG
    44	TGCAGCGGCTGGTCTGGAACGGAGCCGTACCGTTTGAAATTCGGACGGGGAAAGCCATGCCCGACGGGTTCGAG
    ```
    
    ```
   Jessicas-Air:PDSB jessicahoch$ touch summ.txt
   Jessicas-Air:PDSB jessicahoch$ grep ^TGCAG test.fastq | grep 'GAG$' > summ.txt
   ```
