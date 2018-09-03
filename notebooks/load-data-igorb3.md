Classified Ads for Cars Dataset Analysis
================

## Connecting to HIVE runnubg on Hortonworks Sandbox VM

    options( java.parameters = "-Xmx8g" )
    library(rJava)
    library(RJDBC)
     
    cp = c("//d:/tools/apache-hive-1.2.2/lib/hive-jdbc-1.2.2-standalone.jar",
           "//d:/tools/hadoop-2.7.7/share/hadoop/common/hadoop-common-2.7.7.jar")
    .jinit(classpath=cp) 
     
    drv <- JDBC(driverClass = "org.apache.hive.jdbc.HiveDriver",
                classPath = "//d:/tools/apache-hive-1.2.2/lib/hive-jdbc-1.2.2-standalone.jar",
                 identifier.quote="`")
     
    conn <- dbConnect(drv, "jdbc:hive2://127.0.0.1:10000/used_cars", "maria_dev", "maria_dev")

## Discover the used\_cars database

## Discover the used\_cars database

Events table size and head:

``` r
library(xtable)
options(xtable.floating = TRUE)
options(xtable.timestamp = "")
options(xtable.comment = FALSE)

dbSendUpdate(conn, "USE used_cars")

cars <- dbGetQuery(conn, "select * from events limit 10")
colnames(cars) <- c(
  "maker", "model","mileage","year", "disp", "pwr", "body", "color", "stk", 
  "trans", "doors", "seats",  "fuel", "listed", "unlisted", "euro")

print(xtable(cars), 
      caption="Classified Ads for Cars Dataset",
      type = "html", 
      include.rownames=FALSE, 
      caption.placement='top',
      html.table.attributes='align="left"')
```

<table>

<tr>

<th>

maker

</th>

<th>

model

</th>

<th>

mileage

</th>

<th>

year

</th>

<th>

disp

</th>

<th>

pwr

</th>

<th>

body

</th>

<th>

color

</th>

<th>

stk

</th>

<th>

trans

</th>

<th>

doors

</th>

<th>

seats

</th>

<th>

fuel

</th>

<th>

listed

</th>

<th>

unlisted

</th>

<th>

euro

</th>

</tr>

<tr>

<td>

ford

</td>

<td>

galaxy

</td>

<td align="right">

151000.00

</td>

<td align="right">

2011.00

</td>

<td align="right">

2000.00

</td>

<td align="right">

103.00

</td>

<td>

</td>

<td>

</td>

<td>

None

</td>

<td>

man

</td>

<td align="right">

5.00

</td>

<td align="right">

7.00

</td>

<td>

diesel

</td>

<td>

2015-11-14 18:10:06.838

</td>

<td>

2016-01-27 20:40:15.463

</td>

<td align="right">

10584.75

</td>

</tr>

<tr>

<td>

skoda

</td>

<td>

octavia

</td>

<td align="right">

143476.00

</td>

<td align="right">

2012.00

</td>

<td align="right">

2000.00

</td>

<td align="right">

81.00

</td>

<td>

</td>

<td>

</td>

<td>

None

</td>

<td>

man

</td>

<td align="right">

5.00

</td>

<td align="right">

5.00

</td>

<td>

diesel

</td>

<td>

2015-11-14 18:10:06.853

</td>

<td>

2016-01-27 20:40:15.463

</td>

<td align="right">

8882.31

</td>

</tr>

<tr>

<td>

bmw

</td>

<td>

</td>

<td align="right">

97676.00

</td>

<td align="right">

2010.00

</td>

<td align="right">

1995.00

</td>

<td align="right">

85.00

</td>

<td>

</td>

<td>

</td>

<td>

None

</td>

<td>

man

</td>

<td align="right">

5.00

</td>

<td align="right">

5.00

</td>

<td>

diesel

</td>

<td>

2015-11-14 18:10:06.861

</td>

<td>

2016-01-27 20:40:15.463

</td>

<td align="right">

12065.06

</td>

</tr>

<tr>

<td>

skoda

</td>

<td>

fabia

</td>

<td align="right">

111970.00

</td>

<td align="right">

2004.00

</td>

<td align="right">

1200.00

</td>

<td align="right">

47.00

</td>

<td>

</td>

<td>

</td>

<td>

None

</td>

<td>

man

</td>

<td align="right">

5.00

</td>

<td align="right">

5.00

</td>

<td>

gasoline

</td>

<td>

2015-11-14 18:10:06.872

</td>

<td>

2016-01-27 20:40:15.463

</td>

<td align="right">

2960.77

</td>

</tr>

<tr>

<td>

skoda

</td>

<td>

fabia

</td>

<td align="right">

128886.00

</td>

<td align="right">

2004.00

</td>

<td align="right">

1200.00

</td>

<td align="right">

47.00

</td>

<td>

</td>

<td>

</td>

<td>

None

</td>

<td>

man

</td>

<td align="right">

5.00

</td>

<td align="right">

5.00

</td>

<td>

gasoline

</td>

<td>

2015-11-14 18:10:06.88

</td>

<td>

2016-01-27 20:40:15.463

</td>

<td align="right">

2738.71

</td>

</tr>

<tr>

<td>

skoda

</td>

<td>

fabia

</td>

<td align="right">

140932.00

</td>

<td align="right">

2003.00

</td>

<td align="right">

1200.00

</td>

<td align="right">

40.00

</td>

<td>

</td>

<td>

</td>

<td>

None

</td>

<td>

man

</td>

<td align="right">

5.00

</td>

<td align="right">

5.00

</td>

<td>

gasoline

</td>

<td>

2015-11-14 18:10:06.894

</td>

<td>

2016-01-27 20:40:15.463

</td>

<td align="right">

1628.42

</td>

</tr>

<tr>

<td>

skoda

</td>

<td>

fabia

</td>

<td align="right">

167220.00

</td>

<td align="right">

2001.00

</td>

<td align="right">

1400.00

</td>

<td align="right">

74.00

</td>

<td>

</td>

<td>

</td>

<td>

None

</td>

<td>

man

</td>

<td align="right">

5.00

</td>

<td align="right">

5.00

</td>

<td>

gasoline

</td>

<td>

2015-11-14 18:10:06.915

</td>

<td>

2016-01-27 20:40:15.463

</td>

<td align="right">

2072.54

</td>

</tr>

<tr>

<td>

bmw

</td>

<td>

</td>

<td align="right">

148500.00

</td>

<td align="right">

2009.00

</td>

<td align="right">

2000.00

</td>

<td align="right">

130.00

</td>

<td>

</td>

<td>

</td>

<td>

None

</td>

<td>

auto

</td>

<td align="right">

5.00

</td>

<td align="right">

5.00

</td>

<td>

diesel

</td>

<td>

2015-11-14 18:10:06.924

</td>

<td>

2016-01-27 20:40:15.463

</td>

<td align="right">

10547.74

</td>

</tr>

<tr>

<td>

skoda

</td>

<td>

octavia

</td>

<td align="right">

105389.00

</td>

<td align="right">

2003.00

</td>

<td align="right">

1900.00

</td>

<td align="right">

81.00

</td>

<td>

</td>

<td>

</td>

<td>

None

</td>

<td>

man

</td>

<td align="right">

5.00

</td>

<td align="right">

5.00

</td>

<td>

diesel

</td>

<td>

2015-11-14 18:10:06.936

</td>

<td>

2016-01-27 20:40:15.463

</td>

<td align="right">

4293.12

</td>

</tr>

<tr>

<td>

</td>

<td>

</td>

<td align="right">

301381.00

</td>

<td align="right">

2002.00

</td>

<td align="right">

1900.00

</td>

<td align="right">

88.00

</td>

<td>

</td>

<td>

</td>

<td>

None

</td>

<td>

man

</td>

<td align="right">

5.00

</td>

<td align="right">

5.00

</td>

<td>

diesel

</td>

<td>

2015-11-14 18:10:06.954

</td>

<td>

2016-01-27 20:40:15.463

</td>

<td align="right">

1332.35

</td>

</tr>

</table>

``` r
library(knitr)
kable(cars, digits=2)
```

| maker | model   | mileage | year | disp | pwr | body | color | stk  | trans | doors | seats | fuel     | listed                  | unlisted                |     euro |
| :---- | :------ | ------: | ---: | ---: | --: | :--- | :---- | :--- | :---- | ----: | ----: | :------- | :---------------------- | :---------------------- | -------: |
| ford  | galaxy  |  151000 | 2011 | 2000 | 103 |      |       | None | man   |     5 |     7 | diesel   | 2015-11-14 18:10:06.838 | 2016-01-27 20:40:15.463 | 10584.75 |
| skoda | octavia |  143476 | 2012 | 2000 |  81 |      |       | None | man   |     5 |     5 | diesel   | 2015-11-14 18:10:06.853 | 2016-01-27 20:40:15.463 |  8882.31 |
| bmw   |         |   97676 | 2010 | 1995 |  85 |      |       | None | man   |     5 |     5 | diesel   | 2015-11-14 18:10:06.861 | 2016-01-27 20:40:15.463 | 12065.06 |
| skoda | fabia   |  111970 | 2004 | 1200 |  47 |      |       | None | man   |     5 |     5 | gasoline | 2015-11-14 18:10:06.872 | 2016-01-27 20:40:15.463 |  2960.77 |
| skoda | fabia   |  128886 | 2004 | 1200 |  47 |      |       | None | man   |     5 |     5 | gasoline | 2015-11-14 18:10:06.88  | 2016-01-27 20:40:15.463 |  2738.71 |
| skoda | fabia   |  140932 | 2003 | 1200 |  40 |      |       | None | man   |     5 |     5 | gasoline | 2015-11-14 18:10:06.894 | 2016-01-27 20:40:15.463 |  1628.42 |
| skoda | fabia   |  167220 | 2001 | 1400 |  74 |      |       | None | man   |     5 |     5 | gasoline | 2015-11-14 18:10:06.915 | 2016-01-27 20:40:15.463 |  2072.54 |
| bmw   |         |  148500 | 2009 | 2000 | 130 |      |       | None | auto  |     5 |     5 | diesel   | 2015-11-14 18:10:06.924 | 2016-01-27 20:40:15.463 | 10547.74 |
| skoda | octavia |  105389 | 2003 | 1900 |  81 |      |       | None | man   |     5 |     5 | diesel   | 2015-11-14 18:10:06.936 | 2016-01-27 20:40:15.463 |  4293.12 |
|       |         |  301381 | 2002 | 1900 |  88 |      |       | None | man   |     5 |     5 | diesel   | 2015-11-14 18:10:06.954 | 2016-01-27 20:40:15.463 |  1332.35 |

``` r
descr <- dbGetQuery(conn, "describe events")
kable(descr)
```

| col\_name            | data\_type    | comment |
| :------------------- | :------------ | :------ |
| maker                | string        |         |
| model                | string        |         |
| mileage              | int           |         |
| manufacture\_year    | int           |         |
| engine\_displacement | int           |         |
| engine\_power        | int           |         |
| body\_type           | string        |         |
| color\_slug          | string        |         |
| stk\_year            | string        |         |
| transmission         | string        |         |
| door\_count          | int           |         |
| seat\_count          | int           |         |
| fuel\_type           | string        |         |
| date\_created        | timestamp     |         |
| date\_last\_seen     | timestamp     |         |
| price\_eur           | decimal(13,2) |         |

``` r
dbDisconnect(conn)
```

    ## [1] TRUE
