# Loading Classified Ads for Cars Data

This is the link fo the dataset. Download it locally:

https://www.kaggle.com/mirosval/personal-cars-classifieds/

Logib ti the Hortonworks VM and create folder for the project:

```bash
ssh maria_dev@127.0.0.1 -p 2222
cd used-cars/
exit
```

From the Git bash or Putty console copy the file to the Hortonworks VM:

```bash
scp -P 2222 classified-ads-for-cars.zip maria_dev@127.0.0.1:/home/maria_dev/used-cars
```

Login to VM, unzip the file and count the number of lines in the created file (should be about 3.5M):

```bash
ssh maria_dev@127.0.0.1 -p 2222
cd used-cars/
gzip -d --suffix=.zip *.*
wc -l classified-ads-for-cars
```

Copy first line of the file to 'headers' file

```bash
 head -1 classified-ads-for-cars > headers
```

Split the file into 100 chunks and remove headers line from the first file:

```bash
mkdir chunks
cd chunks
split --number=l/100 ../classified-ads-for-cars classified-ads-for-cars_
sed -i 1d classified-ads-for-cars_aa
```

# Copy the files to hdfs: 

Create a directory in hadoop called baranov/cars/classified by using the following command: 
   
 ```bash
 hdfs dfs -mkdir -p  baranov/cars/classified
 ```

You can now copy the event files you downloaded earlier to the hdfs directory you just created by running the following commands. Those commands for each file with CSV extension will print the name of the file (to see the progress), then load the file to HDFS and then move the processed file to folder ../loaded-files:
 
```bash
mkdir ../loaded-files
for file in *; do echo $file;  hdfs dfs -put $file baranov/cars/classified/; mv $file -f ../loaded-files; done
```

To check how many unloaded files left, run the following commabd from another(!) bash window:

```bash
ls events/ | wc -l
```

List files copied to hadoop by running the following command: 

```bash
hdfs dfs -ls baranov/cars/classified/
```
