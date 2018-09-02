Classified Ads for Cars Datatset Analysis
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
tb <- dbGetQuery(conn, "select * from events limit 30")
print(xtable(tb), type = "html", scalebox=.5)
```

<table border="1">

<tr>

<th>

</th>

<th>

events.maker

</th>

<th>

events.model

</th>

<th>

events.mileage

</th>

<th>

events.manufacture\_year

</th>

<th>

events.engine\_displacement

</th>

<th>

events.engine\_power

</th>

<th>

events.body\_type

</th>

<th>

events.color\_slug

</th>

<th>

events.stk\_year

</th>

<th>

events.transmission

</th>

<th>

events.door\_count

</th>

<th>

events.seat\_count

</th>

<th>

events.fuel\_type

</th>

<th>

events.date\_created

</th>

<th>

events.date\_last\_seen

</th>

<th>

events.price\_eur

</th>

</tr>

<tr>

<td align="right">

1

</td>

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

<td align="right">

2

</td>

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

<td align="right">

3

</td>

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

<td align="right">

4

</td>

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

<td align="right">

5

</td>

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

<td align="right">

6

</td>

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

<td align="right">

7

</td>

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

<td align="right">

8

</td>

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

<td align="right">

9

</td>

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

<td align="right">

10

</td>

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

<tr>

<td align="right">

11

</td>

<td>

</td>

<td>

</td>

<td align="right">

202136.00

</td>

<td align="right">

2002.00

</td>

<td align="right">

1400.00

</td>

<td align="right">

55.00

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

2015-11-14 18:10:06.962

</td>

<td>

2016-01-27 20:40:15.463

</td>

<td align="right">

740.19

</td>

</tr>

<tr>

<td align="right">

12

</td>

<td>

</td>

<td>

</td>

<td align="right">

263840.00

</td>

<td align="right">

1998.00

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

2015-11-14 18:10:06.993

</td>

<td>

2016-01-27 20:40:15.463

</td>

<td align="right">

999.26

</td>

</tr>

<tr>

<td align="right">

13

</td>

<td>

</td>

<td>

</td>

<td align="right">

105394.00

</td>

<td align="right">

2000.00

</td>

<td align="right">

1360.00

</td>

<td align="right">

55.00

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

3.00

</td>

<td align="right">

5.00

</td>

<td>

gasoline

</td>

<td>

2015-11-14 18:10:07.036

</td>

<td>

2016-01-27 20:40:15.463

</td>

<td align="right">

1665.43

</td>

</tr>

<tr>

<td align="right">

14

</td>

<td>

skoda

</td>

<td>

favorit

</td>

<td align="right">

41250.00

</td>

<td align="right">

1990.00

</td>

<td align="right">

1300.00

</td>

<td align="right">

44.00

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

2015-11-14 18:10:07.051

</td>

<td>

2016-01-27 20:40:15.463

</td>

<td align="right">

370.10

</td>

</tr>

<tr>

<td align="right">

15

</td>

<td>

suzuki

</td>

<td>

swift

</td>

<td align="right">

122100.00

</td>

<td align="right">

2003.00

</td>

<td align="right">

1000.00

</td>

<td align="right">

39.00

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

2015-11-14 18:10:07.116

</td>

<td>

2016-01-27 20:40:15.463

</td>

<td align="right">

999.26

</td>

</tr>

<tr>

<td align="right">

16

</td>

<td>

nissan

</td>

<td>

x-trail

</td>

<td align="right">

149465.00

</td>

<td align="right">

2005.00

</td>

<td align="right">

2500.00

</td>

<td align="right">

121.00

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

gasoline

</td>

<td>

2015-11-14 18:10:07.484

</td>

<td>

2016-01-27 20:40:15.463

</td>

<td align="right">

4811.25

</td>

</tr>

<tr>

<td align="right">

17

</td>

<td>

</td>

<td>

</td>

<td align="right">

115879.00

</td>

<td align="right">

2003.00

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

2015-11-14 18:10:07.571

</td>

<td>

2016-01-27 20:40:15.463

</td>

<td align="right">

2220.58

</td>

</tr>

<tr>

<td align="right">

18

</td>

<td>

opel

</td>

<td>

astra

</td>

<td align="right">

316054.00

</td>

<td align="right">

2005.00

</td>

<td align="right">

1700.00

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

diesel

</td>

<td>

2015-11-14 18:10:07.585

</td>

<td>

2016-01-27 20:40:15.463

</td>

<td align="right">

2331.61

</td>

</tr>

<tr>

<td align="right">

19

</td>

<td>

skoda

</td>

<td>

superb

</td>

<td align="right">

269398.00

</td>

<td align="right">

2005.00

</td>

<td align="right">

1900.00

</td>

<td align="right">

96.00

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

4.00

</td>

<td align="right">

5.00

</td>

<td>

diesel

</td>

<td>

2015-11-14 18:10:07.599

</td>

<td>

2016-01-27 20:40:15.463

</td>

<td align="right">

4663.21

</td>

</tr>

<tr>

<td align="right">

20

</td>

<td>

skoda

</td>

<td>

fabia

</td>

<td align="right">

87257.00

</td>

<td align="right">

2008.00

</td>

<td align="right">

1200.00

</td>

<td align="right">

44.00

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

2015-11-14 18:10:07.627

</td>

<td>

2016-01-27 20:40:15.463

</td>

<td align="right">

4219.10

</td>

</tr>

<tr>

<td align="right">

21

</td>

<td>

skoda

</td>

<td>

fabia

</td>

<td align="right">

130340.00

</td>

<td align="right">

2001.00

</td>

<td align="right">

1400.00

</td>

<td align="right">

50.00

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

2015-11-14 18:10:07.638

</td>

<td>

2016-01-27 20:40:15.463

</td>

<td align="right">

2442.64

</td>

</tr>

<tr>

<td align="right">

22

</td>

<td>

ford

</td>

<td>

focus

</td>

<td align="right">

227415.00

</td>

<td align="right">

2002.00

</td>

<td align="right">

1800.00

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

2015-11-14 18:10:07.648

</td>

<td>

2016-01-27 20:40:15.463

</td>

<td align="right">

2146.56

</td>

</tr>

<tr>

<td align="right">

23

</td>

<td>

</td>

<td>

</td>

<td align="right">

229642.00

</td>

<td align="right">

2002.00

</td>

<td align="right">

1900.00

</td>

<td align="right">

75.00

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

2015-11-14 18:10:07.672

</td>

<td>

2016-01-27 20:40:15.463

</td>

<td align="right">

2220.58

</td>

</tr>

<tr>

<td align="right">

24

</td>

<td>

ford

</td>

<td>

fiesta

</td>

<td align="right">

84476.00

</td>

<td align="right">

1997.00

</td>

<td align="right">

1300.00

</td>

<td align="right">

44.00

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

2015-11-14 18:10:07.683

</td>

<td>

2016-01-27 20:40:15.463

</td>

<td align="right">

740.19

</td>

</tr>

<tr>

<td align="right">

25

</td>

<td>

citroen

</td>

<td>

c4-picasso

</td>

<td align="right">

112313.00

</td>

<td align="right">

2007.00

</td>

<td align="right">

1700.00

</td>

<td align="right">

92.00

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

gasoline

</td>

<td>

2015-11-14 18:10:07.694

</td>

<td>

2016-01-27 20:40:15.463

</td>

<td align="right">

7105.85

</td>

</tr>

<tr>

<td align="right">

26

</td>

<td>

seat

</td>

<td>

ibiza

</td>

<td align="right">

86484.00

</td>

<td align="right">

2007.00

</td>

<td align="right">

1200.00

</td>

<td align="right">

51.00

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

2015-11-14 18:10:07.729

</td>

<td>

2016-01-27 20:40:15.463

</td>

<td align="right">

3700.96

</td>

</tr>

<tr>

<td align="right">

27

</td>

<td>

kia

</td>

<td>

</td>

<td align="right">

19400.00

</td>

<td align="right">

2014.00

</td>

<td align="right">

1400.00

</td>

<td align="right">

73.00

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

2015-11-14 18:10:07.742

</td>

<td>

2016-01-27 20:40:15.463

</td>

<td align="right">

10917.84

</td>

</tr>

<tr>

<td align="right">

28

</td>

<td>

audi

</td>

<td>

a6

</td>

<td align="right">

207427.00

</td>

<td align="right">

2007.00

</td>

<td align="right">

2700.00

</td>

<td align="right">

132.00

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

2015-11-14 18:10:07.751

</td>

<td>

2016-01-27 20:40:15.463

</td>

<td align="right">

8882.31

</td>

</tr>

<tr>

<td align="right">

29

</td>

<td>

</td>

<td>

</td>

<td align="right">

44971.00

</td>

<td align="right">

2011.00

</td>

<td align="right">

1400.00

</td>

<td align="right">

54.00

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

2015-11-14 18:10:07.761

</td>

<td>

2016-01-27 20:40:15.463

</td>

<td align="right">

6291.64

</td>

</tr>

<tr>

<td align="right">

30

</td>

<td>

suzuki

</td>

<td>

swift

</td>

<td align="right">

113175.00

</td>

<td align="right">

2013.00

</td>

<td align="right">

1600.00

</td>

<td align="right">

100.00

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

3.00

</td>

<td align="right">

4.00

</td>

<td>

gasoline

</td>

<td>

2015-11-14 18:10:07.784

</td>

<td>

2016-01-27 20:40:15.463

</td>

<td align="right">

7401.92

</td>

</tr>

</table>

``` r
dbDisconnect(conn)
```

\[1\] TRUE

``` r
# descr <- dbGetQuery(conn, "describe events")
# descr
```
