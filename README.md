長庚大學 大數據分析方法 作業三
================

作業說明 （繳交時請直接刪除這個章節）
-------------------------------------

作業目的：練習初級爬蟲，並將爬蟲結果整理成資料框data.frame

依下列指示，完成網站內文分析：

-   爬取指定網站內容
    -   學號結尾 0,4,8:[Ptt Tech\_Job 版](https://www.ptt.cc/bbs/Tech_Job/index.html)
    -   學號結尾 1,5,9:[Ptt NBA 版](https://www.ptt.cc/bbs/NBA/index.html)
    -   學號結尾 2,6:[Ptt LoL 版](https://www.ptt.cc/bbs/LoL/index.html)
    -   學號結尾 3,7:[Ptt movie 版](https://www.ptt.cc/bbs/movie/index.html)
-   試著爬出**至少100篇**文章（`30pt`）的**標題**、**推文數**與**作者ID**（各`10pt`）
    -   資料框欄位名稱：
        -   **標題**：Title
        -   **推文數**：PushNum
        -   **作者ID**：Author
    -   一頁只有20篇，該怎麼辦？
        -   提示：使用for + rbind()將分批爬取出的資料結合
        -   範例：dataframeAll&lt;-rbind(dataframe1,dataframe2)
        -   參考：[6.6 資料組合](http://yijutseng.github.io/DataScienceRBook/manipulation.html#section-6.6)
-   將爬取出的資料輸出至Markdown報告中（`10pt`）
    -   使用knitr::kable(資料框物件)整理輸出
-   用文字搭配程式碼解釋爬蟲結果
    -   共爬出幾篇文章標題？（程式碼與文字解釋各`5pt`）
        -   dim(), nrow(), str()皆可
    -   哪個作者文章數最多？（程式碼與文字解釋各`5pt`）
        -   table()
    -   其他爬蟲結果解釋（`10pt`）
        -   試著找出有趣的現象，不一定要用程式碼搭配解釋，也可只用文字

網站資料爬取
------------

``` r
#這是R Code Chunk
library(rvest) ##第一次使用要先安裝 install.packages("rvest")
```

    ## Loading required package: xml2

``` r
##read_html
##html_nodes
##html_text
```

爬蟲結果呈現
------------

``` r
#這是R Code Chunk
knitr::kable(iris) ##請將iris取代為上個步驟中產生的爬蟲資料資料框
```

|  Sepal.Length|  Sepal.Width|  Petal.Length|  Petal.Width| Species    |
|-------------:|------------:|-------------:|------------:|:-----------|
|           5.1|          3.5|           1.4|          0.2| setosa     |
|           4.9|          3.0|           1.4|          0.2| setosa     |
|           4.7|          3.2|           1.3|          0.2| setosa     |
|           4.6|          3.1|           1.5|          0.2| setosa     |
|           5.0|          3.6|           1.4|          0.2| setosa     |
|           5.4|          3.9|           1.7|          0.4| setosa     |
|           4.6|          3.4|           1.4|          0.3| setosa     |
|           5.0|          3.4|           1.5|          0.2| setosa     |
|           4.4|          2.9|           1.4|          0.2| setosa     |
|           4.9|          3.1|           1.5|          0.1| setosa     |
|           5.4|          3.7|           1.5|          0.2| setosa     |
|           4.8|          3.4|           1.6|          0.2| setosa     |
|           4.8|          3.0|           1.4|          0.1| setosa     |
|           4.3|          3.0|           1.1|          0.1| setosa     |
|           5.8|          4.0|           1.2|          0.2| setosa     |
|           5.7|          4.4|           1.5|          0.4| setosa     |
|           5.4|          3.9|           1.3|          0.4| setosa     |
|           5.1|          3.5|           1.4|          0.3| setosa     |
|           5.7|          3.8|           1.7|          0.3| setosa     |
|           5.1|          3.8|           1.5|          0.3| setosa     |
|           5.4|          3.4|           1.7|          0.2| setosa     |
|           5.1|          3.7|           1.5|          0.4| setosa     |
|           4.6|          3.6|           1.0|          0.2| setosa     |
|           5.1|          3.3|           1.7|          0.5| setosa     |
|           4.8|          3.4|           1.9|          0.2| setosa     |
|           5.0|          3.0|           1.6|          0.2| setosa     |
|           5.0|          3.4|           1.6|          0.4| setosa     |
|           5.2|          3.5|           1.5|          0.2| setosa     |
|           5.2|          3.4|           1.4|          0.2| setosa     |
|           4.7|          3.2|           1.6|          0.2| setosa     |
|           4.8|          3.1|           1.6|          0.2| setosa     |
|           5.4|          3.4|           1.5|          0.4| setosa     |
|           5.2|          4.1|           1.5|          0.1| setosa     |
|           5.5|          4.2|           1.4|          0.2| setosa     |
|           4.9|          3.1|           1.5|          0.2| setosa     |
|           5.0|          3.2|           1.2|          0.2| setosa     |
|           5.5|          3.5|           1.3|          0.2| setosa     |
|           4.9|          3.6|           1.4|          0.1| setosa     |
|           4.4|          3.0|           1.3|          0.2| setosa     |
|           5.1|          3.4|           1.5|          0.2| setosa     |
|           5.0|          3.5|           1.3|          0.3| setosa     |
|           4.5|          2.3|           1.3|          0.3| setosa     |
|           4.4|          3.2|           1.3|          0.2| setosa     |
|           5.0|          3.5|           1.6|          0.6| setosa     |
|           5.1|          3.8|           1.9|          0.4| setosa     |
|           4.8|          3.0|           1.4|          0.3| setosa     |
|           5.1|          3.8|           1.6|          0.2| setosa     |
|           4.6|          3.2|           1.4|          0.2| setosa     |
|           5.3|          3.7|           1.5|          0.2| setosa     |
|           5.0|          3.3|           1.4|          0.2| setosa     |
|           7.0|          3.2|           4.7|          1.4| versicolor |
|           6.4|          3.2|           4.5|          1.5| versicolor |
|           6.9|          3.1|           4.9|          1.5| versicolor |
|           5.5|          2.3|           4.0|          1.3| versicolor |
|           6.5|          2.8|           4.6|          1.5| versicolor |
|           5.7|          2.8|           4.5|          1.3| versicolor |
|           6.3|          3.3|           4.7|          1.6| versicolor |
|           4.9|          2.4|           3.3|          1.0| versicolor |
|           6.6|          2.9|           4.6|          1.3| versicolor |
|           5.2|          2.7|           3.9|          1.4| versicolor |
|           5.0|          2.0|           3.5|          1.0| versicolor |
|           5.9|          3.0|           4.2|          1.5| versicolor |
|           6.0|          2.2|           4.0|          1.0| versicolor |
|           6.1|          2.9|           4.7|          1.4| versicolor |
|           5.6|          2.9|           3.6|          1.3| versicolor |
|           6.7|          3.1|           4.4|          1.4| versicolor |
|           5.6|          3.0|           4.5|          1.5| versicolor |
|           5.8|          2.7|           4.1|          1.0| versicolor |
|           6.2|          2.2|           4.5|          1.5| versicolor |
|           5.6|          2.5|           3.9|          1.1| versicolor |
|           5.9|          3.2|           4.8|          1.8| versicolor |
|           6.1|          2.8|           4.0|          1.3| versicolor |
|           6.3|          2.5|           4.9|          1.5| versicolor |
|           6.1|          2.8|           4.7|          1.2| versicolor |
|           6.4|          2.9|           4.3|          1.3| versicolor |
|           6.6|          3.0|           4.4|          1.4| versicolor |
|           6.8|          2.8|           4.8|          1.4| versicolor |
|           6.7|          3.0|           5.0|          1.7| versicolor |
|           6.0|          2.9|           4.5|          1.5| versicolor |
|           5.7|          2.6|           3.5|          1.0| versicolor |
|           5.5|          2.4|           3.8|          1.1| versicolor |
|           5.5|          2.4|           3.7|          1.0| versicolor |
|           5.8|          2.7|           3.9|          1.2| versicolor |
|           6.0|          2.7|           5.1|          1.6| versicolor |
|           5.4|          3.0|           4.5|          1.5| versicolor |
|           6.0|          3.4|           4.5|          1.6| versicolor |
|           6.7|          3.1|           4.7|          1.5| versicolor |
|           6.3|          2.3|           4.4|          1.3| versicolor |
|           5.6|          3.0|           4.1|          1.3| versicolor |
|           5.5|          2.5|           4.0|          1.3| versicolor |
|           5.5|          2.6|           4.4|          1.2| versicolor |
|           6.1|          3.0|           4.6|          1.4| versicolor |
|           5.8|          2.6|           4.0|          1.2| versicolor |
|           5.0|          2.3|           3.3|          1.0| versicolor |
|           5.6|          2.7|           4.2|          1.3| versicolor |
|           5.7|          3.0|           4.2|          1.2| versicolor |
|           5.7|          2.9|           4.2|          1.3| versicolor |
|           6.2|          2.9|           4.3|          1.3| versicolor |
|           5.1|          2.5|           3.0|          1.1| versicolor |
|           5.7|          2.8|           4.1|          1.3| versicolor |
|           6.3|          3.3|           6.0|          2.5| virginica  |
|           5.8|          2.7|           5.1|          1.9| virginica  |
|           7.1|          3.0|           5.9|          2.1| virginica  |
|           6.3|          2.9|           5.6|          1.8| virginica  |
|           6.5|          3.0|           5.8|          2.2| virginica  |
|           7.6|          3.0|           6.6|          2.1| virginica  |
|           4.9|          2.5|           4.5|          1.7| virginica  |
|           7.3|          2.9|           6.3|          1.8| virginica  |
|           6.7|          2.5|           5.8|          1.8| virginica  |
|           7.2|          3.6|           6.1|          2.5| virginica  |
|           6.5|          3.2|           5.1|          2.0| virginica  |
|           6.4|          2.7|           5.3|          1.9| virginica  |
|           6.8|          3.0|           5.5|          2.1| virginica  |
|           5.7|          2.5|           5.0|          2.0| virginica  |
|           5.8|          2.8|           5.1|          2.4| virginica  |
|           6.4|          3.2|           5.3|          2.3| virginica  |
|           6.5|          3.0|           5.5|          1.8| virginica  |
|           7.7|          3.8|           6.7|          2.2| virginica  |
|           7.7|          2.6|           6.9|          2.3| virginica  |
|           6.0|          2.2|           5.0|          1.5| virginica  |
|           6.9|          3.2|           5.7|          2.3| virginica  |
|           5.6|          2.8|           4.9|          2.0| virginica  |
|           7.7|          2.8|           6.7|          2.0| virginica  |
|           6.3|          2.7|           4.9|          1.8| virginica  |
|           6.7|          3.3|           5.7|          2.1| virginica  |
|           7.2|          3.2|           6.0|          1.8| virginica  |
|           6.2|          2.8|           4.8|          1.8| virginica  |
|           6.1|          3.0|           4.9|          1.8| virginica  |
|           6.4|          2.8|           5.6|          2.1| virginica  |
|           7.2|          3.0|           5.8|          1.6| virginica  |
|           7.4|          2.8|           6.1|          1.9| virginica  |
|           7.9|          3.8|           6.4|          2.0| virginica  |
|           6.4|          2.8|           5.6|          2.2| virginica  |
|           6.3|          2.8|           5.1|          1.5| virginica  |
|           6.1|          2.6|           5.6|          1.4| virginica  |
|           7.7|          3.0|           6.1|          2.3| virginica  |
|           6.3|          3.4|           5.6|          2.4| virginica  |
|           6.4|          3.1|           5.5|          1.8| virginica  |
|           6.0|          3.0|           4.8|          1.8| virginica  |
|           6.9|          3.1|           5.4|          2.1| virginica  |
|           6.7|          3.1|           5.6|          2.4| virginica  |
|           6.9|          3.1|           5.1|          2.3| virginica  |
|           5.8|          2.7|           5.1|          1.9| virginica  |
|           6.8|          3.2|           5.9|          2.3| virginica  |
|           6.7|          3.3|           5.7|          2.5| virginica  |
|           6.7|          3.0|           5.2|          2.3| virginica  |
|           6.3|          2.5|           5.0|          1.9| virginica  |
|           6.5|          3.0|           5.2|          2.0| virginica  |
|           6.2|          3.4|           5.4|          2.3| virginica  |
|           5.9|          3.0|           5.1|          1.8| virginica  |

解釋爬蟲結果
------------

``` r
#這是R Code Chunk
```

解釋解釋解釋解釋

``` r
#這是R Code Chunk
```

解釋解釋解釋解釋

人工結論與解釋解釋解釋解釋解釋解釋解釋
