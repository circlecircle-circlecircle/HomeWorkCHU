Final-Taipei
================

``` r
library("jsonlite")
Hotel_data <- fromJSON("http://data.taipei.gov.tw/opendata/apply/query/NDQxOEM2MDAtRDdGNS00NkQ2LUJCMUYtMURBMjlEQUI5MUU5?$format=json")
head(Hotel_data)
```

    ##   rownumber ref_wp cat1         cat2            serial_no   memo_tel
    ## 1       177      6 住宿     一般旅館                B0168 0223116969
    ## 2   1000288      0                   C4_382000000A_002507           
    ## 3       178      6 住宿     一般旅館                B0075 0225520680
    ## 4       179      6 住宿     一般旅館                B0091 0223718812
    ## 5       180      6 住宿 國際觀光旅館                B0340 0225971234
    ## 6       181      6 住宿     一般旅館                B0369 0255793888
    ##     memo_fax memo_cost memo_time         stitle
    ## 1 0223116967  1920以上               東龍大飯店
    ## 2                                      晴天二館
    ## 3 0225520682   600以上               建山大旅社
    ## 4 0223895151  1780以上                 函舍旅館
    ## 5 0225969223                     亞都麗緻大飯店
    ## 6 0255793889 14000以上           宜津美侖大飯店
    ##                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  xbody
    ## 1                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     
    ## 2                         晴天團隊打造離台北最近的海邊度假民宿，由擔任室內設計師的民宿主人親自操刀，房型有法式簡約風《左岸天氣晴》、日本鄉村風《雜貨店》、日式極簡風《鐵道邊》。另提供中西式餐點、輕食、咖啡，還有雜貨、多肉植物盆栽販售，希望來造訪的朋友，不論好天氣、壞天氣，都能一直是晴天。　　《雜貨店》：以日本鄉村雜貨風為特色的《雜貨店》，黃、白色調的臥室，搭配各式各樣的鄉村雜貨，民宿主人打造一處溫馨小吧台，十足居家風格，景觀小陽台可飽覽東北角蔚藍海岸美景。室內設施有液晶電視、音響、無線網路、烤箱、煮水器等，另有數十種書籍、Cd供房客使用。　　《左岸天氣晴》：走法式簡約風格，民宿主人把約三坪大的陽台，打造成海景小花園，是享用早餐的絕佳地點；客房內有液晶有線電視、DVD視聽音響，還有書櫃閱讀沙發區，以及乾濕分離的衛浴設備，設備可不輸給五星級 
    ## 3                                                                                                                                                                                                                                                                     建山大旅社坐落於大稻埕中街，最接近大稻埕碼頭的位置。大稻埕從全台商業最為繁華鼎盛的傳奇年代，直到後來碼頭淤積失去貿易優勢而逐漸沒落的現代。惟有建山大旅社見證了大稻埕的興盛轉衰敗，卻也仍舊保有濃厚的人情味，默默地在此守護。2015年建山大旅社自詡成為大稻埕精神碼頭，藉此傳承歷史文化，重振過往繁華。你知道日本時期大稻埕的風采嗎?想一窺藝旦的生活嗎? 想了解茶葉起家的第一代富豪如何呼風喚雨嗎?建山大旅社希望藉由懷舊的現代感，讓更多人體驗過往的光輝年代，也為歷史注入新血，共創下一個百年輝煌。
    ## 4 本飯店座落於西門町繁華商圈，位置其有指標性作用，周邊環境有經規劃完善的觀光徒步區、電影街、以及購物商圈知名品牌林立，交通便捷緊鄰捷運西門站，至東區、市政府(世貿中心)、郊區至士林、北投、淡水、新店、板橋等四通八達，洽商便利，本旅店根據現代商務旅行及休閒遊憩設計，讓您身居於外，仍盡享居家寧靜悠閒。本館於2008年全新登場，鉅資新粧，結合藝術。全館並結合古董、文物、藝術品，古典優質花梨原木傢俱，舒適合諧的居住空間，並通過消防、全天候反偷拍與建築安檢合格，97年度更榮獲旅館三安優質住宿環境評核。精緻典雅客房八十間，舒適、安全及衛生品管，提供您住宿休憩的舒適空間館內鉅資打造專屬淤您的浪漫悠閒空間，另備有體貼您的24小時寬頻無線上網線路，讓您也能運籌帷幄其中以客為尊，質高價廉。24小時溫馨貼心專業服務是我們的經營理念，舒適安全隱密，竭誠歡迎您蒞臨指教。
    ## 5                                                                                                                                                                                                                                                                                                                                              亞都麗緻飯店以30年代裝飾藝術(Art Deco)為建築設計主體，沒有誇飾的裝潢，沒有炫麗的柱廊，一股散發自內在優雅蘊斂的氣質，及溫馨閒適的住房環境。 我們努力創造與秉持的，是人性化的管理與服務理念。客人會感受到自己所受到的尊重：從機場接機，進入大廳門房親切稱呼其姓名，接待人員引領其入座舒適地辦理住房登記，房內有專用的信紙與名片，甚至前次住宿所要求的事物或細節，我們都悉心準備好；這就是亞都麗緻，感染歡愉與貼心的地方。
    ## 6                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     
    ##      avbegin      avend       idpt                          xurl
    ## 1 2008-10-20 2015-09-09 臺北旅遊網 http://www.east-dragon.com.tw
    ## 2 1900-01-01 1900-01-01                                         
    ## 3 2008-10-20 2016-01-27 臺北旅遊網  http://www.jianshan1977.com/
    ## 4 2008-10-20 2015-09-09 臺北旅遊網 http://www.hansomehote.com.tw
    ## 5 2008-10-20 2010-03-02 臺北旅遊網   http://www.landistpe.com.tw
    ## 6 2008-10-20 2015-09-09 臺北旅遊網                              
    ##                                       address  xpostdate langinfo poi info
    ## 1             臺北市萬華區漢口街二段23號1-7樓 2015-09-09       10   Y     
    ## 2                   新北市瑞芳區建基路2段27號 1900-01-01        0         
    ## 3                臺北市大同區歸綏街182號2-4樓 2016-01-27       10   Y     
    ## 4                 臺北市萬華區成都路68號4-5樓 2015-09-09       10   Y     
    ## 5                臺北市中山區民權東路二段41號 2010-03-02       10   Y     
    ## 6 臺北市大安區復興南路1段315號317號及317號2樓 2015-09-09       10   Y     
    ##    longitude  latitude
    ## 1 121.508045 25.045481
    ## 2  121.80719  25.13312
    ## 3 121.512221 25.058066
    ## 4 121.505239 25.042837
    ## 5 121.530021 25.062857
    ## 6  121.54386 25.034083
    ##                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             file
    ## 1                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     <file><img description="東龍大飯店1">http://www.travel.taipei/d_upload_ttn/frontsite/tw/hotel/B0168/B0168_1.JPG</img><img description="東龍大飯店2">http://www.travel.taipei/d_upload_ttn/frontsite/tw/hotel/B0168/B0168_2.JPG</img><img description="東龍大飯店3">http://www.travel.taipei/d_upload_ttn/frontsite/tw/hotel/B0168/B0168_3.JPG</img></file>
    ## 2                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               http://blog.yam.com/cafesunshine
    ## 3                                                                      <file><img description="建山大旅社1">http://www.travel.taipei/d_upload_ttn/frontsite/tw/hotel/B0075/B0075_433a041a-271e-40db-9ae4-705be9700117.jpg</img><img description="建山大旅社2">http://www.travel.taipei/d_upload_ttn/frontsite/tw/hotel/B0075/B0075_ff14e911-e65c-4df6-874d-369839c63a01.jpg</img><img description="建山大旅社3">http://www.travel.taipei/d_upload_ttn/frontsite/tw/hotel/B0075/B0075_d6649199-e817-42b9-8d66-a52a66d51c93.jpg</img><img description="建山大旅社4">http://www.travel.taipei/d_upload_ttn/frontsite/tw/hotel/B0075/B0075_55323e4c-0ed6-4533-961a-be68e28a0a58.jpg</img><img description="建山大旅社5">http://www.travel.taipei/d_upload_ttn/frontsite/tw/hotel/B0075/B0075_2e4e3455-cf51-4c8c-b23e-4d409a5e8756.jpg</img><img description="建山大旅社6">http://www.travel.taipei/d_upload_ttn/frontsite/tw/hotel/B0075/B0075_c939a870-caee-46b6-8b14-b157bf3adedd.jpg</img></file>
    ## 4                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           <file><img description="函舍旅館1">http://www.travel.taipei/d_upload_ttn/frontsite/tw/hotel/B0091/B0091_1.jpg</img><img description="函舍旅館2">http://www.travel.taipei/d_upload_ttn/frontsite/tw/hotel/B0091/B0091_2.jpg</img><img description="函舍旅館3">http://www.travel.taipei/d_upload_ttn/frontsite/tw/hotel/B0091/B0091_3.jpg</img></file>
    ## 5 <file><img description="亞都麗緻大飯店1">http://www.travel.taipei/d_upload_ttn/frontsite/tw/hotel/B0340/B0340_1.jpg</img><img description="亞都麗緻大飯店2">http://www.travel.taipei/d_upload_ttn/frontsite/tw/hotel/B0340/B0340_2.jpg</img><img description="亞都麗緻大飯店3">http://www.travel.taipei/d_upload_ttn/frontsite/tw/hotel/B0340/B0340_3.jpg</img><img description="亞都麗緻大飯店4">http://www.travel.taipei/d_upload_ttn/frontsite/tw/hotel/B0340/B0340_157a24b2-7bc4-4de9-8863-9e6742a4b6c1.jpg</img><img description="亞都麗緻大飯店5">http://www.travel.taipei/d_upload_ttn/frontsite/tw/hotel/B0340/B0340_8e474abd-bb5d-48f4-8f28-7fe080b79ab8.jpg</img><img description="亞都麗緻大飯店6">http://www.travel.taipei/d_upload_ttn/frontsite/tw/hotel/B0340/B0340_8338cbf6-a044-47ab-849a-9aea33b0764c.jpg</img><img description="亞都麗緻大飯店7">http://www.travel.taipei/d_upload_ttn/frontsite/tw/hotel/B0340/B0340_3d7c69e2-a127-48ca-859d-85d782e30914.jpg</img></file>
    ## 6                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         <file><img description="宜津美侖大飯店1">http://www.travel.taipei/d_upload_ttn/frontsite/tw/hotel/B0369/B0369_1.jpg</img><img description="宜津美侖大飯店2">http://www.travel.taipei/d_upload_ttn/frontsite/tw/hotel/B0369/B0369_2.jpg</img><img description="宜津美侖大飯店3">http://www.travel.taipei/d_upload_ttn/frontsite/tw/hotel/B0369/B0369_3.jpg</img></file>

``` r
library(reshape2)
Hotel_data.m <- melt(Hotel_data,id.vars = c('cat1','cat2','stitle','address'))
head(Hotel_data.m)
```

    ##   cat1         cat2         stitle
    ## 1 住宿     一般旅館     東龍大飯店
    ## 2                         晴天二館
    ## 3 住宿     一般旅館     建山大旅社
    ## 4 住宿     一般旅館       函舍旅館
    ## 5 住宿 國際觀光旅館 亞都麗緻大飯店
    ## 6 住宿     一般旅館 宜津美侖大飯店
    ##                                       address  variable   value
    ## 1             臺北市萬華區漢口街二段23號1-7樓 rownumber     177
    ## 2                   新北市瑞芳區建基路2段27號 rownumber 1000288
    ## 3                臺北市大同區歸綏街182號2-4樓 rownumber     178
    ## 4                 臺北市萬華區成都路68號4-5樓 rownumber     179
    ## 5                臺北市中山區民權東路二段41號 rownumber     180
    ## 6 臺北市大安區復興南路1段315號317號及317號2樓 rownumber     181

``` r
library(ggmap)
```

    ## Loading required package: ggplot2

``` r
twmap.n <- get_map(c(121.43,24.93,121.62,25.19), zoom = 11,language = "zh-TW",maptype = 'roadmap')
```

    ## Warning: bounding box given to google - spatial extent only approximate.

    ## converting bounding box to center/zoom specification. (experimental)

    ## Map from URL : http://maps.googleapis.com/maps/api/staticmap?center=25.06,121.525&zoom=11&size=640x640&scale=2&maptype=roadmap&language=zh-TW&sensor=false

``` r
Hotel_data$longitude<-as.numeric(Hotel_data$longitude)
Hotel_data$latitude<-as.numeric(Hotel_data$latitude)

#ggmap(twmap.n) 

HotelMap = ggmap(twmap.n)+ geom_point(data=subset(Hotel_data), aes(x=Hotel_data$longitude, y=Hotel_data$latitude,color="red"))

HotelMap
```

    ## Warning: Removed 154 rows containing missing values (geom_point).

![](Hotel_Taipei_files/figure-markdown_github/unnamed-chunk-3-1.png)
