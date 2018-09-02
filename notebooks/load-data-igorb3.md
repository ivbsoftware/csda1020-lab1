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

Events table size and
    head:

``` r
dbGetQuery(conn, "select * from events limit 30")
```

    ##    events.maker events.model events.mileage events.manufacture_year
    ## 1          ford       galaxy         151000                    2011
    ## 2         skoda      octavia         143476                    2012
    ## 3           bmw                       97676                    2010
    ## 4         skoda        fabia         111970                    2004
    ## 5         skoda        fabia         128886                    2004
    ## 6         skoda        fabia         140932                    2003
    ## 7         skoda        fabia         167220                    2001
    ## 8           bmw                      148500                    2009
    ## 9         skoda      octavia         105389                    2003
    ## 10                                   301381                    2002
    ## 11                                   202136                    2002
    ## 12                                   263840                    1998
    ## 13                                   105394                    2000
    ## 14        skoda      favorit          41250                    1990
    ## 15       suzuki        swift         122100                    2003
    ## 16       nissan      x-trail         149465                    2005
    ## 17                                   115879                    2003
    ## 18         opel        astra         316054                    2005
    ## 19        skoda       superb         269398                    2005
    ## 20        skoda        fabia          87257                    2008
    ## 21        skoda        fabia         130340                    2001
    ## 22         ford        focus         227415                    2002
    ## 23                                   229642                    2002
    ## 24         ford       fiesta          84476                    1997
    ## 25      citroen   c4-picasso         112313                    2007
    ## 26         seat        ibiza          86484                    2007
    ## 27          kia                       19400                    2014
    ## 28         audi           a6         207427                    2007
    ## 29                                    44971                    2011
    ## 30       suzuki        swift         113175                    2013
    ##    events.engine_displacement events.engine_power events.body_type
    ## 1                        2000                 103                 
    ## 2                        2000                  81                 
    ## 3                        1995                  85                 
    ## 4                        1200                  47                 
    ## 5                        1200                  47                 
    ## 6                        1200                  40                 
    ## 7                        1400                  74                 
    ## 8                        2000                 130                 
    ## 9                        1900                  81                 
    ## 10                       1900                  88                 
    ## 11                       1400                  55                 
    ## 12                       1900                  81                 
    ## 13                       1360                  55                 
    ## 14                       1300                  44                 
    ## 15                       1000                  39                 
    ## 16                       2500                 121                 
    ## 17                       1900                  88                 
    ## 18                       1700                  74                 
    ## 19                       1900                  96                 
    ## 20                       1200                  44                 
    ## 21                       1400                  50                 
    ## 22                       1800                  85                 
    ## 23                       1900                  75                 
    ## 24                       1300                  44                 
    ## 25                       1700                  92                 
    ## 26                       1200                  51                 
    ## 27                       1400                  73                 
    ## 28                       2700                 132                 
    ## 29                       1400                  54                 
    ## 30                       1600                 100                 
    ##    events.color_slug events.stk_year events.transmission events.door_count
    ## 1                               None                 man                 5
    ## 2                               None                 man                 5
    ## 3                               None                 man                 5
    ## 4                               None                 man                 5
    ## 5                               None                 man                 5
    ## 6                               None                 man                 5
    ## 7                               None                 man                 5
    ## 8                               None                auto                 5
    ## 9                               None                 man                 5
    ## 10                              None                 man                 5
    ## 11                              None                 man                 5
    ## 12                              None                 man                 5
    ## 13                              None                 man                 3
    ## 14                              None                 man                 5
    ## 15                              None                 man                 5
    ## 16                              None                auto                 5
    ## 17                              None                 man                 5
    ## 18                              None                 man                 5
    ## 19                              None                 man                 4
    ## 20                              None                 man                 5
    ## 21                              None                 man                 5
    ## 22                              None                 man                 5
    ## 23                              None                 man                 5
    ## 24                              None                 man                 5
    ## 25                              None                 man                 5
    ## 26                              None                 man                 5
    ## 27                              None                 man                 5
    ## 28                              None                auto                 5
    ## 29                              None                 man                 5
    ## 30                              None                 man                 3
    ##    events.seat_count events.fuel_type     events.date_created
    ## 1                  7           diesel 2015-11-14 18:10:06.838
    ## 2                  5           diesel 2015-11-14 18:10:06.853
    ## 3                  5           diesel 2015-11-14 18:10:06.861
    ## 4                  5         gasoline 2015-11-14 18:10:06.872
    ## 5                  5         gasoline  2015-11-14 18:10:06.88
    ## 6                  5         gasoline 2015-11-14 18:10:06.894
    ## 7                  5         gasoline 2015-11-14 18:10:06.915
    ## 8                  5           diesel 2015-11-14 18:10:06.924
    ## 9                  5           diesel 2015-11-14 18:10:06.936
    ## 10                 5           diesel 2015-11-14 18:10:06.954
    ## 11                 5         gasoline 2015-11-14 18:10:06.962
    ## 12                 5           diesel 2015-11-14 18:10:06.993
    ## 13                 5         gasoline 2015-11-14 18:10:07.036
    ## 14                 5         gasoline 2015-11-14 18:10:07.051
    ## 15                 5         gasoline 2015-11-14 18:10:07.116
    ## 16                 5         gasoline 2015-11-14 18:10:07.484
    ## 17                 5           diesel 2015-11-14 18:10:07.571
    ## 18                 5           diesel 2015-11-14 18:10:07.585
    ## 19                 5           diesel 2015-11-14 18:10:07.599
    ## 20                 5         gasoline 2015-11-14 18:10:07.627
    ## 21                 5         gasoline 2015-11-14 18:10:07.638
    ## 22                 5           diesel 2015-11-14 18:10:07.648
    ## 23                 5           diesel 2015-11-14 18:10:07.672
    ## 24                 5         gasoline 2015-11-14 18:10:07.683
    ## 25                 7         gasoline 2015-11-14 18:10:07.694
    ## 26                 5         gasoline 2015-11-14 18:10:07.729
    ## 27                 5         gasoline 2015-11-14 18:10:07.742
    ## 28                 5           diesel 2015-11-14 18:10:07.751
    ## 29                 5         gasoline 2015-11-14 18:10:07.761
    ## 30                 4         gasoline 2015-11-14 18:10:07.784
    ##      events.date_last_seen events.price_eur
    ## 1  2016-01-27 20:40:15.463         10584.75
    ## 2  2016-01-27 20:40:15.463          8882.31
    ## 3  2016-01-27 20:40:15.463         12065.06
    ## 4  2016-01-27 20:40:15.463          2960.77
    ## 5  2016-01-27 20:40:15.463          2738.71
    ## 6  2016-01-27 20:40:15.463          1628.42
    ## 7  2016-01-27 20:40:15.463          2072.54
    ## 8  2016-01-27 20:40:15.463         10547.74
    ## 9  2016-01-27 20:40:15.463          4293.12
    ## 10 2016-01-27 20:40:15.463          1332.35
    ## 11 2016-01-27 20:40:15.463           740.19
    ## 12 2016-01-27 20:40:15.463           999.26
    ## 13 2016-01-27 20:40:15.463          1665.43
    ## 14 2016-01-27 20:40:15.463           370.10
    ## 15 2016-01-27 20:40:15.463           999.26
    ## 16 2016-01-27 20:40:15.463          4811.25
    ## 17 2016-01-27 20:40:15.463          2220.58
    ## 18 2016-01-27 20:40:15.463          2331.61
    ## 19 2016-01-27 20:40:15.463          4663.21
    ## 20 2016-01-27 20:40:15.463          4219.10
    ## 21 2016-01-27 20:40:15.463          2442.64
    ## 22 2016-01-27 20:40:15.463          2146.56
    ## 23 2016-01-27 20:40:15.463          2220.58
    ## 24 2016-01-27 20:40:15.463           740.19
    ## 25 2016-01-27 20:40:15.463          7105.85
    ## 26 2016-01-27 20:40:15.463          3700.96
    ## 27 2016-01-27 20:40:15.463         10917.84
    ## 28 2016-01-27 20:40:15.463          8882.31
    ## 29 2016-01-27 20:40:15.463          6291.64
    ## 30 2016-01-27 20:40:15.463          7401.92

``` r
descr <- dbGetQuery(conn, "describe events")
descr
```

    ##               col_name     data_type comment
    ## 1                maker        string        
    ## 2                model        string        
    ## 3              mileage           int        
    ## 4     manufacture_year           int        
    ## 5  engine_displacement           int        
    ## 6         engine_power           int        
    ## 7            body_type        string        
    ## 8           color_slug        string        
    ## 9             stk_year        string        
    ## 10        transmission        string        
    ## 11          door_count           int        
    ## 12          seat_count           int        
    ## 13           fuel_type        string        
    ## 14        date_created     timestamp        
    ## 15      date_last_seen     timestamp        
    ## 16           price_eur decimal(13,2)
