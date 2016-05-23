Hotel
================

``` r
library("jsonlite")
Hotel_data <- fromJSON("http://data.taipei.gov.tw/opendata/apply/query/NDQxOEM2MDAtRDdGNS00NkQ2LUJCMUYtMURBMjlEQUI5MUU5?$format=json")
head(Hotel_data)
```

    ##   rownumber ref_wp cat1         cat2            serial_no   memo_tel
    ## 1        91      6 住宿 國際觀光旅館                B0321 0287706565
    ## 2   1000042      0                   C4_382000000A_001614           
    ## 3        92      6 住宿 國際觀光旅館                B0357 0223215511
    ## 4        93      6 住宿     一般旅館                B0486 0228988661
    ## 5        94      6 住宿     一般旅館                B0485 0223140245
    ## 6        95      6 住宿 國際觀光旅館                B0327 0223115151
    ##     memo_fax memo_cost memo_time               stitle
    ## 1 0287706555                       台北威斯汀六福皇宮
    ## 2                                 溫莎堡-香草花園民宿
    ## 3 0223944240                     台北寒舍喜來登大飯店
    ## 4 0228988662 12800以上             北投天玥泉溫泉會館
    ## 5 0223822425  2000以上                 古奈堡商務旅館
    ## 6 0223319944                           台北凱撒大飯店
    ##                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                xbody
    ## 1                                                                                                                                                                                      國際連鎖飯店六福皇宮The Westin Taipei，座落於台北市南京東路金融商圈及娛樂中心，臨近大眾捷運系統與松山機場，四十分鐘可抵達桃園國際機場。飯店樓高十五層地下四層，設有二百八十八間現代化設計客房與四十二間高級套房及八間頂級餐廳與酒吧。 飯店的室內空間設計是以流行生活品味的語彙~精品飯店(Boutique Hotel)為主要設計走向，並以精緻甚至是結合摩登前衛取勝，以對比一般五星級飯店的華麗 鋪排。館內傢俱皆以金屬原色及深咖啡色為主要色 系，呈現出沉穩、自信的風采，讓蒞臨賓客體會到最時尚的空間潮流。
    ## 2                                                                                                                                                                                                                                                                                       溫莎堡香草庭院民宿打造了最頂級的休閒住宿場所，客房設施配備豪華，重金禮聘名設計師規劃浪漫溫馨的客房裝潢設計，耗費鉅資打造專屬於您的浪漫隱密空間。　以提供舒適的住宿環境為我們的最高宗旨，更希望能讓前來住宿的朋友們對九份甚至於附近的金瓜石、東北角及平溪等地有深入的認識。　精心策劃出六條半日遊的路線供您自由選擇，讓您來九份不但能夠住的舒服，也能夠玩的精采豐富，歡迎家族、團體來電預約！
    ## 3 台北喜來登大飯店自1981年3月24日起，以『來來香格里拉大飯店』之名正式開幕。同時並與國際喜達屋酒店管理顧問集團簽訂世界性連鎖業務技術合作契約至今，提供五星級的優質設施與服務。自2002年7月1日起，飯店正式由寒舍餐旅管理顧問股份有限公司接掌營運，並更名為台北喜來登大飯店。為了能夠創造出煥然一新的精緻時尚風格，並保留古典中國優雅蘊歛的文化元素，台北喜來登大飯店經過近三年的全館重新裝修後，館內處處可見精心擺置的古董藝術精品，及饒富趣味的古中國意象圖騰。台北喜來登共擁有688間全新設計裝潢的各式客房及套房，及多間中、西、日式美食餐廳，提供賓客最豐富精采的食宿享受。傳承二十餘年來一貫溫婉細膩的服務精神，台北喜來登大飯店誠摯邀請您一同驗證這場充滿感動與驚喜的時尚風華再現。
    ## 4                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   
    ## 5                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        台北西門捷運站6號出口，紅樓，西門徒步區，西門町鬧區商場大街
    ## 6                                                                                                                                                                                                          台北凱撒大飯店前身為台灣首座知名國際五星級連鎖飯店 (台北希爾頓大飯店)，曾接待過無數國內外知名重量級人士，秉持一貫的專業態度與優質服務，讓曾經入住的貴賓們皆擁有愉悅而舒適的住宿回憶。台北凱撒位於城市中心點，除了為連結高鐵、台鐵、捷運等三鐵匯集之交通樞紐，並鄰近全省巴士轉運站，更直接與台北捷運車站六號出口連通，優越的地理環境結合多元的美食及優雅舒適的住宿，讓入住飯店的貴賓們能輕鬆自在地暢遊、閱覽台北市的絢麗繁華及其近郊的風光美景，為來台觀光商務的最佳首選。
    ##      avbegin      avend       idpt                                   xurl
    ## 1 2008-10-20 2013-04-10 臺北旅遊網               http://www.westin.com.tw
    ## 2 1900-01-01 1900-01-01                                                  
    ## 3 2008-10-20 2013-04-10 臺北旅遊網 http://www.sheratongrandetaipei.com.tw
    ## 4 2008-10-20 2015-12-16 臺北旅遊網                  http://www.tyq.com.tw
    ## 5 2008-10-20 2016-05-09 臺北旅遊網               http://good9stay.okgo.tw
    ## 6 2008-10-20 2012-11-22 臺北旅遊網       http://taipei.caesarpark.com.tw/
    ##                         address  xpostdate langinfo poi info   longitude
    ## 1 臺北市中山區南京東路三段133號 2013-04-10       10   Y      121.5411869
    ## 2        新北市瑞芳區基山街62號 1900-01-01        0            121.84325
    ## 3  臺北市中正區忠孝東路一段12號 2013-04-10       10   Y      121.5220851
    ## 4      臺北市北投區中山路3號3樓 2015-12-16       10   Y      121.5054429
    ## 5  臺北市萬華區峨眉街28號5樓之1 2016-05-09       10   Y      121.5068005
    ## 6  臺北市中正區忠孝西路一段38號 2012-11-22       10   Y      121.5165968
    ##     latitude
    ## 1 25.0521017
    ## 2   25.10808
    ## 3  25.045031
    ## 4 25.1371628
    ## 5 25.0434921
    ## 6 25.0462151
    ##                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                file
    ## 1                                                                                                                <file><img description="台北威斯汀六福皇宮1">http://www.travel.taipei/d_upload_ttn/frontsite/tw/hotel/B0321/B0321_1.jpg</img><img description="台北威斯汀六福皇宮2">http://www.travel.taipei/d_upload_ttn/frontsite/tw/hotel/B0321/B0321_2.jpg</img><img description="台北威斯汀六福皇宮3">http://www.travel.taipei/d_upload_ttn/frontsite/tw/hotel/B0321/B0321_3.jpg</img></file>
    ## 2                                                                                                                                                                                                                                                                                                                                                                                                                                                                   http://windsor.idv.tw/index.asp
    ## 3 <file><img description="台北寒舍喜來登大飯店1">http://www.travel.taipei/d_upload_ttn/frontsite/tw/hotel/B0357/B0357_38f9fa5f-aa37-41e7-9caf-4a15171ba0e9.jpg</img><img description="台北寒舍喜來登大飯店2">http://www.travel.taipei/d_upload_ttn/frontsite/tw/hotel/B0357/B0357_97ef577f-1b14-450c-a859-b96f9caef5f4.jpg</img><img description="台北寒舍喜來登大飯店3">http://www.travel.taipei/d_upload_ttn/frontsite/tw/hotel/B0357/B0357_dd296d04-f122-41f7-85f4-b6859f170223.jpg</img></file>
    ## 4                                                                                                                                                                 <file><img description="北投天玥泉溫泉會館1">http://www.travel.taipei/d_upload_ttn/frontsite/tw/hotel/B0486/B0486_d41ba168-f70f-4716-b688-b9d5d5ecef51.jpg</img><img description="北投天玥泉溫泉會館2">http://www.travel.taipei/d_upload_ttn/frontsite/tw/hotel/B0486/B0486_e57e4a37-e1e6-4416-b865-6de7f02ff402.jpg</img></file>
    ## 5                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  
    ## 6                   <file><img description="台北凱撒大飯店1">http://www.travel.taipei/d_upload_ttn/frontsite/tw/hotel/B0327/B0327_9054654e-7ae6-4679-ba13-77514f6df4b8.jpg</img><img description="台北凱撒大飯店2">http://www.travel.taipei/d_upload_ttn/frontsite/tw/hotel/B0327/B0327_fb8f8f4b-0091-4861-b4a2-2facf8f36619.jpg</img><img description="台北凱撒大飯店3">http://www.travel.taipei/d_upload_ttn/frontsite/tw/hotel/B0327/B0327_b6e1857e-146e-48b5-82ef-693469abc437.jpg</img></file>

``` r
library(reshape2)
Hotel_data.m <- melt(Hotel_data,id.vars = c('cat1','cat2','stitle','address'))
head(Hotel_data.m)
```

    ##   cat1         cat2               stitle                       address
    ## 1 住宿 國際觀光旅館   台北威斯汀六福皇宮 臺北市中山區南京東路三段133號
    ## 2                    溫莎堡-香草花園民宿        新北市瑞芳區基山街62號
    ## 3 住宿 國際觀光旅館 台北寒舍喜來登大飯店  臺北市中正區忠孝東路一段12號
    ## 4 住宿     一般旅館   北投天玥泉溫泉會館      臺北市北投區中山路3號3樓
    ## 5 住宿     一般旅館       古奈堡商務旅館  臺北市萬華區峨眉街28號5樓之1
    ## 6 住宿 國際觀光旅館       台北凱撒大飯店  臺北市中正區忠孝西路一段38號
    ##    variable   value
    ## 1 rownumber      91
    ## 2 rownumber 1000042
    ## 3 rownumber      92
    ## 4 rownumber      93
    ## 5 rownumber      94
    ## 6 rownumber      95

雙北市住宿分類
==============

``` r
aggregate(Hotel_data.m$cat2,by=list(Hotel_data.m$cat2),FUN=length)
```

    ##        Group.1    x
    ## 1              7942
    ## 2     一般旅館 8987
    ## 3 一般觀光旅館  323
    ## 4 國際觀光旅館  494

``` r
#第一個欄位是未分類的數量，每個數字加總就是雙北市總共的旅館數
```

台北市住宿分類
--------------

``` r
Taipei <-Hotel_data.m[grep("臺北市",Hotel_data.m$address),]
aggregate(Taipei$cat2,by=list(Taipei$cat2),FUN=length)
```

    ##        Group.1    x
    ## 1     一般旅館 8987
    ## 2 一般觀光旅館  228
    ## 3 國際觀光旅館  456

台北市 中正區

``` r
Taipei.100 <-Taipei[grep("中正區",Taipei$address),]
aggregate(Taipei.100$cat2,by=list(Taipei.100$cat2),FUN=length)
```

    ##        Group.1    x
    ## 1     一般旅館 1235
    ## 2 一般觀光旅館   57
    ## 3 國際觀光旅館   38

台北市 大同區

``` r
Taipei.103 <-Taipei[grep("大同區",Taipei$address),]
aggregate(Taipei.103$cat2,by=list(Taipei.103$cat2),FUN=length)
```

    ##        Group.1   x
    ## 1     一般旅館 912
    ## 2 國際觀光旅館  19

台北市 中山區

``` r
Taipei.104 <-Taipei[grep("中山區",Taipei$address),]
aggregate(Taipei.104$cat2,by=list(Taipei.104$cat2),FUN=length)
```

    ##        Group.1    x
    ## 1     一般旅館 2166
    ## 2 一般觀光旅館  133
    ## 3 國際觀光旅館  228

台北市 松山區

``` r
Taipei.105 <-Taipei[grep("松山區",Taipei$address),]
aggregate(Taipei.105$cat2,by=list(Taipei.105$cat2),FUN=length)
```

    ##        Group.1   x
    ## 1     一般旅館 608
    ## 2 國際觀光旅館  38

台北市 大安區

``` r
Taipei.106 <-Taipei[grep("大安區",Taipei$address),]
aggregate(Taipei.106$cat2,by=list(Taipei.106$cat2),FUN=length)
```

    ##        Group.1   x
    ## 1     一般旅館 741
    ## 2 一般觀光旅館  19
    ## 3 國際觀光旅館  76

台北市 萬華區

``` r
Taipei.108 <-Taipei[grep("萬華區",Taipei$address),]
aggregate(Taipei.108$cat2,by=list(Taipei.108$cat2),FUN=length)
```

    ##        Group.1    x
    ## 1     一般旅館 1786
    ## 2 國際觀光旅館   19

台北市 信義區

``` r
Taipei.110 <-Taipei[grep("信義區",Taipei$address),]
aggregate(Taipei.110$cat2,by=list(Taipei.110$cat2),FUN=length)
```

    ##        Group.1   x
    ## 1     一般旅館 228
    ## 2 國際觀光旅館  19

台北市 士林區

``` r
Taipei.111 <-Taipei[grep("士林區",Taipei$address),]
aggregate(Taipei.111$cat2,by=list(Taipei.111$cat2),FUN=length)
```

    ##        Group.1   x
    ## 1     一般旅館 323
    ## 2 國際觀光旅館  19

台北市 北投區

``` r
Taipei.112 <-Taipei[grep("北投區",Taipei$address),]
aggregate(Taipei.112$cat2,by=list(Taipei.112$cat2),FUN=length)
```

    ##        Group.1   x
    ## 1     一般旅館 665
    ## 2 一般觀光旅館  19

台北市 內湖區

``` r
Taipei.114 <-Taipei[grep("內湖區",Taipei$address),]
aggregate(Taipei.114$cat2,by=list(Taipei.114$cat2),FUN=length)
```

    ##    Group.1  x
    ## 1 一般旅館 76

台北市 南港區

``` r
Taipei.115 <-Taipei[grep("南港區",Taipei$address),]
aggregate(Taipei.115$cat2,by=list(Taipei.115$cat2),FUN=length)
```

    ##    Group.1   x
    ## 1 一般旅館 171

台北市 文山區

``` r
Taipei.116 <-Taipei[grep("文山區",Taipei$address),]
aggregate(Taipei.116$cat2,by=list(Taipei.116$cat2),FUN=length)
```

    ##    Group.1  x
    ## 1 一般旅館 76

新北市住宿分類(發現他們都沒有分類ex:一般旅館,一般觀光旅館...)
-------------------------------------------------------------

``` r
NEW_Taipei <-Hotel_data.m[grep("新北市",Hotel_data.m$address),]
aggregate(NEW_Taipei$cat2,by=list(NEW_Taipei$cat2),FUN=length)
```

    ##   Group.1    x
    ## 1         7942

新北市 萬里區

``` r
NEW_Taipei.207 <-NEW_Taipei[grep("萬里區",NEW_Taipei$address),]
aggregate(NEW_Taipei.207$cat2,by=list(NEW_Taipei.207$cat2),FUN=length)
```

    ##   Group.1   x
    ## 1         513

新北市 金山區

``` r
NEW_Taipei.208 <-NEW_Taipei[grep("金山區",NEW_Taipei$address),]
aggregate(NEW_Taipei.208$cat2,by=list(NEW_Taipei.208$cat2),FUN=length)
```

    ##   Group.1   x
    ## 1         361

新北市 板橋區

``` r
NEW_Taipei.220 <-NEW_Taipei[grep("板橋區",NEW_Taipei$address),]
aggregate(NEW_Taipei.220$cat2,by=list(NEW_Taipei.220$cat2),FUN=length)
```

    ##   Group.1   x
    ## 1         836

新北市 汐止區

``` r
NEW_Taipei.221 <-NEW_Taipei[grep("汐止區",NEW_Taipei$address),]
aggregate(NEW_Taipei.221 $cat2,by=list(NEW_Taipei.221 $cat2),FUN=length)
```

    ##   Group.1   x
    ## 1         152

新北市 深坑區

``` r
NEW_Taipei.222 <-NEW_Taipei[grep("深坑區",NEW_Taipei$address),]
aggregate(NEW_Taipei.222$cat2,by=list(NEW_Taipei.222$cat2),FUN=length)
```

    ##   Group.1  x
    ## 1         38

新北市 石碇區

``` r
NEW_Taipei.223 <-NEW_Taipei[grep("石碇區",NEW_Taipei$address),]
aggregate(NEW_Taipei.223$cat2,by=list(NEW_Taipei.223$cat2),FUN=length)
```

    ##   Group.1  x
    ## 1         19

新北市 瑞芳區

``` r
NEW_Taipei.224 <-NEW_Taipei[grep("瑞芳區",NEW_Taipei$address),]
aggregate(NEW_Taipei.224$cat2,by=list(NEW_Taipei.224$cat2),FUN=length)
```

    ##   Group.1    x
    ## 1         1463

新北市 平溪區

``` r
NEW_Taipei.226 <-NEW_Taipei[grep("平溪區",NEW_Taipei$address),]
aggregate(NEW_Taipei.226$cat2,by=list(NEW_Taipei.226$cat2),FUN=length)
```

    ##   Group.1   x
    ## 1         171

新北市 雙溪區

``` r
NEW_Taipei.227 <-NEW_Taipei[grep("雙溪區",NEW_Taipei$address),]
aggregate(NEW_Taipei.227$cat2,by=list(NEW_Taipei.227$cat2),FUN=length)
```

    ##   Group.1   x
    ## 1         266

新北市 貢寮區

``` r
NEW_Taipei.228 <-NEW_Taipei[grep("貢寮區",NEW_Taipei$address),]
aggregate(NEW_Taipei.228$cat2,by=list(NEW_Taipei.228$cat2),FUN=length)
```

    ##   Group.1   x
    ## 1         209

新北市 新店區

``` r
NEW_Taipei.231 <-NEW_Taipei[grep("新店區",NEW_Taipei$address),]
aggregate(NEW_Taipei.231$cat2,by=list(NEW_Taipei.231$cat2),FUN=length)
```

    ##   Group.1   x
    ## 1         285

新北市 坪林區

``` r
NEW_Taipei.232 <-NEW_Taipei[grep("坪林區",NEW_Taipei$address),]
NEW_Taipei.232
```

    ## [1] cat1     cat2     stitle   address  variable value   
    ## <0 rows> (or 0-length row.names)

新北市 烏來區

``` r
NEW_Taipei.233 <-NEW_Taipei[grep("烏來區",NEW_Taipei$address),]
aggregate(NEW_Taipei.233$cat2,by=list(NEW_Taipei.233$cat2),FUN=length)
```

    ##   Group.1   x
    ## 1         418

新北市 永和區

``` r
NEW_Taipei.234 <-NEW_Taipei[grep("永和區",NEW_Taipei$address),]
aggregate(NEW_Taipei.234$cat2,by=list(NEW_Taipei.234$cat2),FUN=length)
```

    ##   Group.1   x
    ## 1         190

新北市 中和區

``` r
NEW_Taipei.235 <-NEW_Taipei[grep("中和區",NEW_Taipei$address),]
aggregate(NEW_Taipei.235$cat2,by=list(NEW_Taipei.235$cat2),FUN=length)
```

    ##   Group.1   x
    ## 1         361

新北市 土城區

``` r
NEW_Taipei.236 <-NEW_Taipei[grep("土城區",NEW_Taipei$address),]
aggregate(NEW_Taipei.236$cat2,by=list(NEW_Taipei.236$cat2),FUN=length)
```

    ##   Group.1   x
    ## 1         171

新北市 三峽區

``` r
NEW_Taipei.237 <-NEW_Taipei[grep("三峽區",NEW_Taipei$address),]
aggregate(NEW_Taipei.237$cat2,by=list(NEW_Taipei.237$cat2),FUN=length)
```

    ##   Group.1   x
    ## 1         152

新北市 樹林區

``` r
NEW_Taipei.238 <-NEW_Taipei[grep("樹林區",NEW_Taipei$address),]
aggregate(NEW_Taipei.238$cat2,by=list(NEW_Taipei.238$cat2),FUN=length)
```

    ##   Group.1   x
    ## 1         190

新北市 鶯歌區

``` r
NEW_Taipei.239 <-NEW_Taipei[grep("鶯歌區",NEW_Taipei$address),]
aggregate(NEW_Taipei.239$cat2,by=list(NEW_Taipei.239$cat2),FUN=length)
```

    ##   Group.1  x
    ## 1         76

新北市 三重區

``` r
NEW_Taipei.241 <-NEW_Taipei[grep("三重區",NEW_Taipei$address),]
aggregate(NEW_Taipei.241$cat2,by=list(NEW_Taipei.241$cat2),FUN=length)
```

    ##   Group.1   x
    ## 1         513

新北市 新莊區

``` r
NEW_Taipei.242 <-NEW_Taipei[grep("新莊區",NEW_Taipei$address),]
aggregate(NEW_Taipei.242$cat2,by=list(NEW_Taipei.242$cat2),FUN=length)
```

    ##   Group.1   x
    ## 1         190

新北市 泰山區

``` r
NEW_Taipei.243 <-NEW_Taipei[grep("泰山區",NEW_Taipei$address),]
aggregate(NEW_Taipei.243$cat2,by=list(NEW_Taipei.243$cat2),FUN=length)
```

    ##   Group.1  x
    ## 1         95

新北市 林口區

``` r
NEW_Taipei.244 <-NEW_Taipei[grep("林口區",NEW_Taipei$address),]
aggregate(NEW_Taipei.244$cat2,by=list(NEW_Taipei.244$cat2),FUN=length)
```

    ##   Group.1  x
    ## 1         38

新北市 蘆洲區

``` r
NEW_Taipei.247 <-NEW_Taipei[grep("蘆洲區",NEW_Taipei$address),]
aggregate(NEW_Taipei.247$cat2,by=list(NEW_Taipei.247$cat2),FUN=length)
```

    ##   Group.1   x
    ## 1         114

新北市 五股區

``` r
NEW_Taipei.248 <-NEW_Taipei[grep("五股區",NEW_Taipei$address),]
aggregate(NEW_Taipei.248$cat2,by=list(NEW_Taipei.248$cat2),FUN=length)
```

    ##   Group.1  x
    ## 1         19

新北市 八里區

``` r
NEW_Taipei.249 <-NEW_Taipei[grep("八里區",NEW_Taipei$address),]
aggregate(NEW_Taipei.249$cat2,by=list(NEW_Taipei.249$cat2),FUN=length)
```

    ##   Group.1  x
    ## 1         19

新北市 淡水區

``` r
NEW_Taipei.251 <-NEW_Taipei[grep("淡水區",NEW_Taipei$address),]
aggregate(NEW_Taipei.251$cat2,by=list(NEW_Taipei.251$cat2),FUN=length)
```

    ##   Group.1   x
    ## 1         608

新北市 三芝區

``` r
NEW_Taipei.252 <-NEW_Taipei[grep("三芝區",NEW_Taipei$address),]
aggregate(NEW_Taipei.252$cat2,by=list(NEW_Taipei.252$cat2),FUN=length)
```

    ##   Group.1   x
    ## 1         399

新北市 石門區

``` r
NEW_Taipei.253 <-NEW_Taipei[grep("石門區",NEW_Taipei$address),]
aggregate(NEW_Taipei.253$cat2,by=list(NEW_Taipei.253$cat2),FUN=length)
```

    ##   Group.1  x
    ## 1         57
