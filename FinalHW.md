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

由於變數多，且輸出為二元類別變數，故選擇邏輯迴歸演算法建立模型，並使用雙向逐步選擇最佳參數組合。

``` r
fit<-glm(diabetes~., PimaIndiansDiabetesC[PimaIndiansDiabetesC$Test==F,],family="binomial")
library(MASS)
finalFit<-stepAIC(fit,direction = "both",trace = F)
summary(finalFit)$coefficients
```

    ##                 Estimate  Std. Error   z value     Pr(>|z|)
    ## (Intercept) -9.252240868 0.943413544 -9.807195 1.048421e-22
    ## pregnant     0.099629169 0.039184946  2.542537 1.100510e-02
    ## glucose      0.038558105 0.004597741  8.386314 5.016209e-17
    ## pressure    -0.012000455 0.006679026 -1.796737 7.237732e-02
    ## insulin     -0.002087749 0.001133852 -1.841288 6.557935e-02
    ## mass         0.085699472 0.017867260  4.796453 1.614999e-06
    ## pedigree     1.159703360 0.381804615  3.037426 2.386078e-03
    ## age          0.030477252 0.012169764  2.504342 1.226794e-02

模型說明
--------

由上述參數可知，使用多種參數來檢測人體所得到的資料，以邏輯迴歸建立模型預測是否為糖尿病患者，經最佳化後，模型使用參數為pregnant, glucose, pressure, mass, pedigree,，共4個參數，各參數代表從人體檢測出來的數據值。

預測模型驗證
------------

``` r
MinePred<-predict(finalFit,newdata = PimaIndiansDiabetesC[PimaIndiansDiabetesC$Test==T,])
MineAns<-ifelse(MinePred<0.5,"neg","pos") #<0.5: Level 1
MineAns<-factor(MineAns,levels = c("neg","pos"))
MineAns
```

    ##  11  13  14  15  19  24  25  28  42  47  50  51  53  54  55  59  60  62 
    ## neg pos neg neg pos neg neg neg neg neg pos pos pos neg neg neg neg neg 
    ##  63  65  71  72  76  77  78  80  84  85  92  99 104 109 111 112 119 120 
    ## neg neg neg neg neg pos neg pos neg neg neg neg neg neg neg neg neg neg 
    ## 123 126 134 135 137 142 145 146 153 156 160 162 165 167 169 171 173 174 
    ## neg pos pos pos pos pos neg neg neg neg pos neg neg neg neg pos neg neg 
    ## 176 180 181 183 186 187 192 193 196 197 199 200 201 203 204 205 209 210 
    ## neg neg neg neg neg neg neg neg pos neg neg neg pos pos neg pos pos neg 
    ## 213 215 216 217 221 223 224 225 226 227 236 237 241 245 246 247 248 249 
    ## pos neg neg neg neg neg neg neg pos neg neg neg neg neg pos neg neg neg 
    ## 256 260 263 264 269 271 272 273 276 277 278 279 280 285 293 298 300 301 
    ## pos neg neg neg neg neg pos neg neg pos neg neg neg neg neg neg neg pos 
    ## 303 305 309 310 314 315 317 329 331 338 339 340 345 348 350 351 353 356 
    ## neg neg pos neg neg neg neg neg neg neg neg pos neg neg neg neg pos neg 
    ## 359 362 363 364 367 369 370 374 375 376 381 385 388 389 401 402 406 407 
    ## neg neg pos neg neg neg pos neg neg pos neg neg neg neg neg neg neg neg 
    ## 408 410 411 414 415 416 421 424 429 431 434 435 438 446 447 449 454 456 
    ## neg neg neg pos pos neg neg neg neg neg neg pos neg neg pos pos neg neg 
    ## 460 469 470 474 477 485 488 490 491 496 505 511 519 520 521 522 531 534 
    ## neg neg neg neg neg pos neg neg pos neg neg neg neg neg neg neg pos pos 
    ## 537 541 544 546 550 553 554 561 563 570 573 579 581 584 586 588 589 591 
    ## neg neg neg neg neg neg neg neg neg neg neg neg neg neg neg neg pos neg 
    ## 593 603 605 608 611 614 619 620 627 628 630 633 637 638 646 647 649 651 
    ## neg pos neg neg pos pos neg neg neg neg pos neg neg neg neg neg neg neg 
    ## 656 657 658 659 661 665 670 673 682 685 686 687 693 695 699 701 703 705 
    ## neg neg neg neg pos neg neg neg neg neg pos neg neg neg neg neg pos neg 
    ## 707 709 712 713 714 718 720 721 722 724 726 731 733 742 751 753 754 756 
    ## neg neg neg neg neg neg pos neg neg neg neg neg neg neg neg pos neg pos 
    ## 760 762 766 768 
    ## neg pos neg neg 
    ## Levels: neg pos

``` r
library(caret) # install.packages("caret") #計算參數的packages
```

    ## Loading required package: lattice

    ## Loading required package: ggplot2

``` r
sensitivity(MineAns,PimaIndiansDiabetesC[PimaIndiansDiabetesC$Test==T,]$diabetes)
```

    ## [1] 0.9360465

``` r
specificity(MineAns,PimaIndiansDiabetesC[PimaIndiansDiabetesC$Test==T,]$diabetes)
```

    ## [1] 0.5

``` r
posPredValue(MineAns,PimaIndiansDiabetesC[PimaIndiansDiabetesC$Test==T,]$diabetes)
```

    ## [1] 0.7931034

``` r
negPredValue(MineAns,PimaIndiansDiabetesC[PimaIndiansDiabetesC$Test==T,]$diabetes)
```

    ## [1] 0.7924528

-   敏感度 93.6046512%
-   特異性 50%
-   陽性預測率 79.3103448%
-   陰性預測率 79.245283%
