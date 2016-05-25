FinalHW
================

糖尿病 預測模型
===============

資料前處理
----------

解釋資料
--------

此資料來源為UCI Machine Learning Repository。 資料是文森特Sigillito研究中心提供的，內有768筆資料，有8種屬性，主要是由糖尿病研究所中的消化和腎臟病的數據庫，來判斷這個人是否有可能罹患糖尿病的可能，此資料中有遺失的值。另外，分類結果為二元分類，藥檢呈陰性糖尿病 (neg) 與藥檢呈陽性糖尿病 (pos)

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

    ##                 Estimate  Std. Error    z value     Pr(>|z|)
    ## (Intercept) -9.108468925 0.908970325 -10.020645 1.236931e-23
    ## pregnant     0.192655631 0.036602681   5.263430 1.413927e-07
    ## glucose      0.043484985 0.004741616   9.170921 4.689963e-20
    ## pressure    -0.016331008 0.006626344  -2.464558 1.371824e-02
    ## insulin     -0.003824707 0.001117187  -3.423515 6.181676e-04
    ## mass         0.100845849 0.018160660   5.552984 2.808345e-08
    ## pedigree     0.999617378 0.373992359   2.672828 7.521473e-03

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

    ##   2   4   7   8  11  14  15  16  17  21  22  26  28  31  33  37  39  41 
    ## neg neg neg neg neg neg neg neg neg pos neg neg neg neg neg pos pos neg 
    ##  42  44  45  46  53  63  65  66  69  72  74  79  80  81  82  84  87  97 
    ## neg neg neg neg neg neg pos pos neg pos neg neg neg neg neg neg pos neg 
    ##  98 100 107 108 109 113 117 121 127 131 136 139 143 149 150 152 153 160 
    ## neg neg neg neg neg pos neg neg pos neg neg pos neg neg neg neg neg neg 
    ## 162 166 167 168 169 171 176 182 184 186 190 192 197 198 200 202 205 206 
    ## pos pos neg neg neg neg neg neg neg neg neg neg neg neg pos pos neg pos 
    ## 207 209 211 212 213 217 222 223 226 234 235 239 241 245 246 248 249 251 
    ## neg neg neg neg pos neg neg neg neg neg neg pos pos neg pos neg neg neg 
    ## 257 258 259 260 263 264 267 273 274 275 277 279 280 285 286 288 290 291 
    ## neg pos pos neg pos neg neg neg neg neg neg pos neg neg neg neg neg pos 
    ## 297 298 303 307 308 309 312 313 317 324 331 334 337 340 341 343 345 346 
    ## neg neg neg neg neg neg neg neg neg neg neg pos neg pos neg neg pos neg 
    ## 349 350 356 357 358 359 364 368 369 371 372 375 383 384 387 389 390 391 
    ## neg neg neg neg neg neg pos pos pos neg neg neg pos neg pos neg neg neg 
    ## 396 398 401 402 406 407 415 417 418 422 423 425 427 437 438 439 442 443 
    ## neg pos neg neg pos neg neg neg neg neg neg neg neg pos neg neg pos neg 
    ## 445 447 448 454 456 464 468 471 472 474 475 477 481 482 483 489 491 492 
    ## pos pos neg neg neg neg neg pos pos neg neg pos neg pos pos neg neg neg 
    ## 495 497 501 502 505 510 512 518 519 522 528 537 546 548 551 554 557 558 
    ## pos neg neg neg neg pos pos pos neg neg neg neg neg neg neg neg pos neg 
    ## 561 562 563 565 570 575 579 580 581 585 600 606 607 610 611 612 623 627 
    ## neg neg neg neg neg neg neg neg neg neg neg neg neg neg neg neg pos neg 
    ## 629 636 642 643 650 652 655 656 659 660 663 665 670 672 682 692 693 695 
    ## neg neg neg pos neg neg neg neg pos pos neg neg neg pos neg neg neg pos 
    ## 696 702 704 705 708 710 714 721 725 726 727 729 735 740 745 747 748 749 
    ## neg neg neg pos neg neg neg neg neg neg neg pos pos neg neg neg neg neg 
    ## 754 755 756 762 
    ## neg neg neg neg 
    ## Levels: neg pos

``` r
library(caret) # install.packages("caret") #計算參數的packages
```

    ## Loading required package: lattice

    ## Loading required package: ggplot2

``` r
sensitivity(MineAns,PimaIndiansDiabetesC[PimaIndiansDiabetesC$Test==T,]$diabetes)
```

    ## [1] 0.8895706

``` r
specificity(MineAns,PimaIndiansDiabetesC[PimaIndiansDiabetesC$Test==T,]$diabetes)
```

    ## [1] 0.4193548

``` r
posPredValue(MineAns,PimaIndiansDiabetesC[PimaIndiansDiabetesC$Test==T,]$diabetes)
```

    ## [1] 0.7286432

``` r
negPredValue(MineAns,PimaIndiansDiabetesC[PimaIndiansDiabetesC$Test==T,]$diabetes)
```

    ## [1] 0.6842105

-   敏感度 88.9570552%
-   特異性 41.9354839%
-   陽性預測率 72.8643216%
-   陰性預測率 68.4210526%
