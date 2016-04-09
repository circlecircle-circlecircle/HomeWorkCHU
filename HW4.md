Facebook粉絲團分析（分析專頁名稱朱立倫）
================

分析朱立倫從2016/01/01到2016/04/09發出的文章。

``` r
if (!require('Rfacebook')){
    install.packages("Rfacebook")
    library(Rfacebook)
}
```

    ## Loading required package: Rfacebook

    ## Warning: package 'Rfacebook' was built under R version 3.2.4

    ## Loading required package: httr

    ## Warning: package 'httr' was built under R version 3.2.4

    ## Loading required package: rjson

    ## Loading required package: httpuv

    ## Warning: package 'httpuv' was built under R version 3.2.4

    ## 
    ## Attaching package: 'Rfacebook'

    ## The following object is masked from 'package:methods':
    ## 
    ##     getGroup

讀取朱立倫粉絲團資料
--------------------

``` r
token<-'CAACEdEose0cBAH8cf30YKx4eU6SxmZBSGnDMxgqaMuyv4cZCAxtiuZBtJeVJhmZAtZALrZAexD80buXzPhZAaF6TKjnrOCZBjtaqBRZBTY1BcNZAnK1N0kin7ZCH3bTObZC0I01mP8cf8ABrjLmYNUqrzMxk9PqlWU2VVqNPQven7z4EEr6y38hZA4CRA9zW6AmjMaeZBVoZC0CZCnEXhdDSDstZBXEXufMsgTyZB04zYZD'
totalPage<-NULL
lastDate<-Sys.Date()
DateVectorStr<-as.character(seq(as.Date("2016-01-01"),lastDate,by="5 days"))
for(i in 1:(length(DateVectorStr)-1)){
    tempPage<-getPage("llchu", token,
                      since = DateVectorStr[i],until = DateVectorStr[i+1])
    totalPage<-rbind(totalPage,tempPage)
}
```

    ## 14 posts 13 posts 25 posts 4 posts 5 posts 5 posts 7 posts 5 posts 1 posts 6 posts 5 posts 3 posts 4 posts 6 posts 4 posts 8 posts 5 posts 5 posts 4 posts

``` r
nrow(totalPage)
```

    ## [1] 129

發現立倫今年起到04/09共發了129篇文章!

每日發文數分析
--------------

發現在2016/01/12那天發文數是最多次的，可能是因為靠近01/16選舉日那天了，多多提倡大家來投票，也順便發了幾篇在拜票過成的感觸。

``` r
totalPage$datetime <- as.POSIXct(totalPage$created_time, 
                                 format = "%Y-%m-%dT%H:%M:%S+0000", 
                                 tz = "GMT") #2016-01-16T15:05:36+0000
totalPage$dateTPE <- format(totalPage$datetime, "%Y-%m-%d", 
                            tz = "Asia/Taipei") #2016-01-16
totalPage$weekdays <-weekdays(as.Date(totalPage$dateTPE))
PostCount<-aggregate(id~dateTPE,totalPage,length)
library(knitr)
kable(head(PostCount[order(PostCount$id,decreasing = T),]))
```

|     | dateTPE    |   id|
|-----|:-----------|----:|
| 12  | 2016-01-12 |    7|
| 13  | 2016-01-13 |    5|
| 14  | 2016-01-14 |    5|
| 15  | 2016-01-15 |    5|
| 65  | 2016-03-20 |    4|
| 1   | 2016-01-01 |    3|

每日獲得讚數分析
----------------

分析後發現2016/01/16，也就是大選當天po的文章讚數平均有高達8萬個!! 平均讚數最高的第2名是02/06那天Po的一篇文章，內容是新北市派出30為特搜大隊去台南幫忙救災!!!!!!!! 果然~感人的舉動只要一篇就能獲得廣大的讚。

``` r
totalPage$datetime <- as.POSIXct(totalPage$created_time, 
                                 format = "%Y-%m-%dT%H:%M:%S+0000", 
                                 tz = "GMT") #2016-01-16T15:05:36+0000
totalPage$dateTPE <- format(totalPage$datetime, "%Y-%m-%d", 
                            tz = "Asia/Taipei") #2016-01-16
totalPage$weekdays <-weekdays(as.Date(totalPage$dateTPE))
LikeCount<-aggregate(likes_count~dateTPE,totalPage,mean)
library(knitr)
kable(head(LikeCount[order(LikeCount$likes_count,decreasing = T),]))
```

|     | dateTPE    |  likes\_count|
|-----|:-----------|-------------:|
| 16  | 2016-01-16 |       83386.0|
| 34  | 2016-02-06 |       57639.0|
| 9   | 2016-01-09 |       52729.5|
| 15  | 2016-01-15 |       49404.8|
| 17  | 2016-01-18 |       46132.0|
| 36  | 2016-02-08 |       41877.0|

每日評論數分析
--------------

評論數最高的前幾名也都是大選前幾天!!可見大家都有很多的話想要跟朱立倫說~

``` r
totalPage$datetime <- as.POSIXct(totalPage$created_time, 
                                 format = "%Y-%m-%dT%H:%M:%S+0000", 
                                 tz = "GMT") #2016-01-16T15:05:36+0000
totalPage$dateTPE <- format(totalPage$datetime, "%Y-%m-%d", 
                            tz = "Asia/Taipei") #2016-01-16
totalPage$weekdays <-weekdays(as.Date(totalPage$dateTPE))
CommentsCount<-aggregate(comments_count~dateTPE,totalPage,mean)
library(knitr)
kable(head(CommentsCount[order(CommentsCount$comments_count,decreasing = T),]))
```

|     | dateTPE    |  comments\_count|
|-----|:-----------|----------------:|
| 16  | 2016-01-16 |          10605.5|
| 15  | 2016-01-15 |           7843.8|
| 17  | 2016-01-18 |           3629.0|
| 9   | 2016-01-09 |           1883.0|
| 18  | 2016-01-19 |           1649.0|
| 34  | 2016-02-06 |           1377.0|

每日分享數分析
--------------

在大選前日感覺大家都動員起來，為朱立倫宣傳他的理念，想讓更多人看到。

``` r
totalPage$datetime <- as.POSIXct(totalPage$created_time, 
                                 format = "%Y-%m-%dT%H:%M:%S+0000", 
                                 tz = "GMT") #2016-01-16T15:05:36+0000
totalPage$dateTPE <- format(totalPage$datetime, "%Y-%m-%d", 
                            tz = "Asia/Taipei") #2016-01-16
totalPage$weekdays <-weekdays(as.Date(totalPage$dateTPE))
SharesCount<-aggregate(shares_count~dateTPE,totalPage,mean)
library(knitr)
kable(head(SharesCount[order(SharesCount$shares_count,decreasing = T),]))
```

|     | dateTPE    |  shares\_count|
|-----|:-----------|--------------:|
| 15  | 2016-01-15 |       2342.600|
| 1   | 2016-01-01 |       1521.000|
| 16  | 2016-01-16 |       1363.500|
| 34  | 2016-02-06 |       1265.000|
| 12  | 2016-01-12 |       1000.571|
| 9   | 2016-01-09 |        937.000|
