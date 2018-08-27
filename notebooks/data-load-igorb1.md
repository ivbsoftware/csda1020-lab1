# Loading Data



Download the latest GDELT masterfile:

```bash
cd /cygdrive/c/Users/ibaranov/Downloads/York/group-projects/csda1020-project-1/data
wget -c http://data.gdeltproject.org/gdeltv2/masterfilelist.txt
```

Extract last 2 years of the 'master' files list:

```bash
awk -v date="$(date --date='2 year ago' +%Y%m%d)" \
'{if (/export/ && int(substr($3, 38, 8)) > int(date)) print $3}' \
masterfilelist.txt > lasttwoyearslist.txt
```

Count the number of lines in the created file (should be about 69K):

```bash
wc -l lasttwoyearslist.txt
```

Download the files:

```bash
mkdir files
cd files
while read in; wget "$in"; done < ../lasttwoyearslist.txt
```

Unzip the files:

```bash
gzip -d --suffix=.zip *.*
```
