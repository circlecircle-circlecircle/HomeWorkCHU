FinalHW
================

糖尿病 預測模型
===============

資料前處理
----------

解釋資料
--------

此資料來源為UCI Machine Learning Repository。 資料是文森特Sigillito研究中心提供的，內有768筆資料，有8種屬性，主要是由糖尿病研究所中的消化和腎臟病的數據庫，來判斷這個人是否有可能罹患糖尿病的可能，此資料中有遺失的值。另外，分類結果為二元分類，藥檢呈陰性糖尿病 (neg) 與藥檢呈陽性糖尿病 (pos) 。

``` r
library(mlbench)
data(PimaIndiansDiabetes)
str(PimaIndiansDiabetes) 
```

    ## 'data.frame':    768 obs. of  9 variables:
    ##  $ pregnant: num  6 1 8 1 0 5 3 10 2 8 ...
    ##  $ glucose : num  148 85 183 89 137 116 78 115 197 125 ...
    ##  $ pressure: num  72 66 64 66 40 74 50 0 70 96 ...
    ##  $ triceps : num  35 29 0 23 35 0 32 0 45 0 ...
    ##  $ insulin : num  0 0 0 94 168 0 88 0 543 0 ...
    ##  $ mass    : num  33.6 26.6 23.3 28.1 43.1 25.6 31 35.3 30.5 0 ...
    ##  $ pedigree: num  0.627 0.351 0.672 0.167 2.288 ...
    ##  $ age     : num  50 31 32 21 33 30 26 29 53 54 ...
    ##  $ diabetes: Factor w/ 2 levels "neg","pos": 2 1 2 1 2 1 2 1 2 2 ...

把資料讀進來
------------

``` r
library(mlbench)
data(PimaIndiansDiabetes)
head(PimaIndiansDiabetes) 
```

    ##   pregnant glucose pressure triceps insulin mass pedigree age diabetes
    ## 1        6     148       72      35       0 33.6    0.627  50      pos
    ## 2        1      85       66      29       0 26.6    0.351  31      neg
    ## 3        8     183       64       0       0 23.3    0.672  32      pos
    ## 4        1      89       66      23      94 28.1    0.167  21      neg
    ## 5        0     137       40      35     168 43.1    2.288  33      pos
    ## 6        5     116       74       0       0 25.6    0.201  30      neg

資料前處理
----------

``` r
PimaIndiansDiabetesC<-
    PimaIndiansDiabetes[complete.cases(PimaIndiansDiabetes),] 
c(nrow(PimaIndiansDiabetes),nrow(PimaIndiansDiabetesC))
```

    ## [1] 768 768

分成訓練組跟測試組，並紀錄各組人數
----------------------------------

隨機將2/3的資料分到訓練組（Test==F），剩下1/3為測試組（Test==T）

``` r
PimaIndiansDiabetesC$Test<-F 
PimaIndiansDiabetesC[
    sample(1:nrow(PimaIndiansDiabetesC),nrow(PimaIndiansDiabetesC)/3),
     ]$Test<-T 
c(sum(PimaIndiansDiabetesC$Test==F),sum(PimaIndiansDiabetesC$Test==T)) 
```

    ## [1] 512 256

可見訓練組案例為512，測驗組案例為256

預測模型建立
------------

由於變數多，且輸出為二元類別變數，故選擇多變數線性迴歸演算法建立模型，並使用雙向逐步選擇最佳參數組合。

``` r
fit<-glm(diabetes~age+pedigree+mass+insulin+triceps+pressure+glucose+pregnant, PimaIndiansDiabetesC[PimaIndiansDiabetesC$Test==F,],family="binomial")

library(MASS)
finalFit<-stepAIC(fit,direction = "both",trace = F)
summary(finalFit)$coefficients
```

    ##                 Estimate   Std. Error   z value     Pr(>|z|)
    ## (Intercept) -7.818200567 0.8173905201 -9.564829 1.123871e-21
    ## pedigree     0.946467298 0.3466303771  2.730480 6.324218e-03
    ## mass         0.073239704 0.0171892407  4.260788 2.037077e-05
    ## insulin     -0.001969765 0.0009857966 -1.998145 4.570090e-02
    ## pressure    -0.010208418 0.0057390776 -1.778756 7.527979e-02
    ## glucose      0.037157075 0.0043717862  8.499289 1.907553e-17
    ## pregnant     0.116281769 0.0343544507  3.384766 7.123901e-04

模型說明
--------

由上述參數可知，使用多種參數來檢測人體所得到的資料，以多變數線性迴歸建立模型預測是否為糖尿病患者，經最佳化後，模型使用參數為age,pedigree+mass,insulin,triceps,pressure,glucose,pregnant，共個參數，各參數代表從人體檢測出來的數據值。

預測模型驗證
------------

``` r
MinePred<-predict(finalFit,newdata = PimaIndiansDiabetesC[PimaIndiansDiabetesC$Test==T,])
MineAns<-ifelse(MinePred<0.5,"neg","pos") #<0.5: Level 1
MineAns<-factor(MineAns,levels = c("neg","pos"))
```

``` r
library(caret) # install.packages("caret") #計算參數的packages
```

    ## Loading required package: lattice

    ## Loading required package: ggplot2

``` r
sensitivity(MineAns,PimaIndiansDiabetesC[PimaIndiansDiabetesC$Test==T,]$diabetes)
```

    ## [1] 0.9766082

``` r
specificity(MineAns,PimaIndiansDiabetesC[PimaIndiansDiabetesC$Test==T,]$diabetes)
```

    ## [1] 0.4588235

``` r
posPredValue(MineAns,PimaIndiansDiabetesC[PimaIndiansDiabetesC$Test==T,]$diabetes)
```

    ## [1] 0.7840376

``` r
negPredValue(MineAns,PimaIndiansDiabetesC[PimaIndiansDiabetesC$Test==T,]$diabetes)
```

    ## [1] 0.9069767

-   敏感度 97.6608187%
-   特異性 45.8823529%
-   陽性預測率 78.4037559%
-   陰性預測率 90.6976744%
