

```bash 

### RUNNING FASTQC 

## created a new analysis folder in /home/jferreira/ 
[jferreira@cbix2 ~]$ mkdir joao_analysis 

## go to location of data sets
[jferreira@cbix2 joao_analysis]$ cd
[jferreira@cbix2 ~]$ cd /mnt/data/encode_tissue_data/
[jferreira@cbix2 encode_tissue_data]$ ll

## copy liver and heart data folders to the liver and heart folders I made
[jferreira@cbix2 encode_tissue_data]$ cp -r liver /home/jferreira/joao_analysis/
[jferreira@cbix2 encode_tissue_data]$ cp -r heart /home/jferreira/joao_analysis/

## made a liver and heart fasqc analysis folder inside joao_analysis folder 
[jferreira@cbix2 ~]$ cd joao_analysis
[jferreira@cbix2 joao_analysis]$ mkdir fastqc_heart
[jferreira@cbix2 joao_analysis]$ mkdir fastqc_liver

## run fastqc on liver and heart, specify output locations to new folders
[jferreira@cbix2 joao_analysis]$ cd liver 
[jferreira@cbix2 liver]$ for i in *.fastq.gz; do fastqc $i -o /home/jferreira/joao_analysis/fastqc_liver/; done
Started analysis of liver_ENCFF001RNR_R1.fastq.gz
[jferreira@cbix2 joao_analysis]$ cd heart 
[jferreira@cbix2 liver]$ for i in *.fastq.gz; do fastqc $i -o /home/jferreira/joao_analysis/fastqc_heart/; done
Started analysis of heart_ENCFF001RNR_R1.fastq.gz

## Download fastqc HTMLs to local machine 
#log in to server using 
sftp jferreira@10.1.105.13 

#navigate to where html files are located copy them to local machine
sftp> ll 
sftp> cd /home/jferreira/joao_analysis/fastqc_liver/
sftp>  get *.html (file path on computer)
sftp> lpwd 


### TRIMMING 

## create trimming data folders 
[jferreira@cbix2 joao_analysis]$ mkdir trim_heart
[jferreira@cbix2 joao_analysis]$ mkdir trim_liver

## Run trimming command loop in folders with data
[jferreira@cbix2 heart]$  for i in *R1.fastq.gz; do trim_galore --paired --fastqc --illumina --output 
/home/jferreira/joao_analysis/trim_heart/ --retain_unpaired $i ${i/R1/R2}; done
[jferreira@cbix2 liver]$  for i in *R1.fastq.gz; do trim_galore --paired --fastqc --illumina --output 
/home/jferreira/joao_analysis/trim_liver/ --retain_unpaired $i ${i/R1/R2}; done

## Run trimming in tmux
[jferreira@cbix2 heart]$ tmux new -s trim_liver

# return to tmux session
tmux attatch -t trim_liver 



``` 








