# Loading Data

SSH to the VM (user maria_dev, password maria_dev):

```bash
ssh maria_dev@127.0.0.1 -p 2222
```

Download the latest GDELT masterfile:

```bash
wget -c http://data.gdeltproject.org/gdeltv2/masterfilelist.txt
```

Extract last 2 years of the 'master' files list. Note that insted of "2 year ago" you could use any of date utility's parameters, like "5 month ago" etc. Here is the Linux AWK command that does the following:
 
 - Creates variable dateFrom in format like '20160827'
 - For each line in masterfilelist.txt:
 
    * If the line has substring 'export' in it,
    * AND if the file date (8 chars at 38 position in 3rd column) bigger than dateFrom,
    * THEN the 3rd column of the line (file url) is copied to file lasttwoyearslist.txt,
    * OTHEWISE the line is skipped;

```bash
awk -v dateFrom="$(date --date='2 year ago' +%Y%m%d)" \
'{if (/export/ && int(substr($3, 38, 8)) > int(dateFrom)) print $3}' \
masterfilelist.txt > lasttwoyearslist.txt
```

Count the number of lines in the created file (should be about 69K):

```bash
wc -l lasttwoyearslist.txt
```

Download the files:

```bash
mkdir events
cd events
while read in; do wget "$in"; done < ../lasttwoyearslist.txt
```

While the files are being downloaded, open another SSH console and monitor the progress by counting number of files in events folder:

```bash
ls | wc -l
```

Unzip the files:

```bash
for file in *.zip; do echo $file; gzip -d -suffix=.zip $file; done
```

# Copy the file to hdfs: 

Create a directory in hadoop called gdelt/events by using the following command: 
   
 ```bash
 hdfs dfs -mkdir -p  mbaranov/gdelt/events
 ```
   
 For example if <your_id> is 3283939 the above command should be: 
    
 ```bash
 hdfs dfs -mkdir -p mbaranov/gdelt/events
 ```

You can now copy the event files you downloaded earlier to the hdfs directory you just created by running the following command 

```bash
mkdir ../loaded-files
for file in *.CSV; do echo $file;  hdfs dfs -put $file mbaranov/gdelt/events/; mv $file -f ../loaded-files; done
```

Check how many files left

```bash
ls events/ | wc -l
```

Confirm that the files have been copied to hadoop my running the following command: 

```bash
hdfs dfs -ls mbaranov/gdelt/events/
```
