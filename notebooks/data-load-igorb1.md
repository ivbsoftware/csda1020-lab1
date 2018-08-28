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
ls events/ | wc -l
```

Unzip the files:

```bash
gzip -d --suffix=.zip *.*
```
