長庚大學 大數據分析方法 作業三
================

網站資料爬取
------------

``` r
#install.packages("rvest")
library(rvest)
```

    ## Warning: package 'rvest' was built under R version 3.3.3

    ## Loading required package: xml2

    ## Warning: package 'xml2' was built under R version 3.3.3

``` r
PTT<-read_html("https://www.ptt.cc/bbs/Tech_Job/index.html")
btnURL<-PTT  %>% html_nodes("a[class ='btn wide']") %>% html_attr("href")
indexNum<-as.numeric(gsub("/bbs/Tech_Job/index|.html","",btnURL[2]))
totalPage<-NULL
for(i in (indexNum-4):(indexNum+1)){
   
    PTT=paste("https://www.ptt.cc/bbs/Tech_Job/index",i,".html",sep="")

    
Title <- read_html(PTT) %>% html_nodes(".title") %>% html_text() 

PushNum <- read_html(PTT) %>% html_nodes(".nrec") %>% html_text() 

Author <- read_html(PTT) %>% html_nodes(".author") %>% html_text() 

PTT_news <- data.frame(Title,PushNum,Author)


  
    totalPage<-rbind(totalPage,PTT_news)
}

  

View(totalPage)
```

爬蟲結果呈現
------------

``` r
knitr::kable(totalPage) 
```

| Title                                               | PushNum | Author       |
|:----------------------------------------------------|:--------|:-------------|
| 敬鵬-資訊系統開發管理師                             | 2       | incoterms    |
| \[請益\] 美亞科技                                   | 6       | key9028      |
| \[新聞\] 總經理巡廠要整理桌面　群創員工爆比當兵     | 35      | zzzz8931     |
| Re: \[討論\] 關於機台零件是不是都撐到最後？         | 1       | c1823akimo   |
| 創群科技                                            | 12      | jamiefly     |
| \[討論\] 有人因為辦公室太舊太髒離職的嗎??           | 45      | yamakazi     |
| (本文已被刪除) \[VamYU\]                            | 12      | -            |
| Re: \[心得\] 我在拓凱(台中工業區)的日子             | 6       | simplep2002  |
| Re: \[新聞\]【台GG別走動畫】台積傳將赴美砸5千億建3  | 2       | egnaro123    |
| \[聘書\] 緯創/建漢/帆宣                             | 3       | tomandjim    |
| (本文已被刪除) \[piggg\]                            |         | -            |
| \[徵才\] 交大電子所誠徵碩士級研究助理               | 1       | xgin         |
| \[情報\] 國網中心擴大舉辦工讀生/實習生徵才活動      |         | ZhaoYun      |
| \[請益\] 亞太國際電機 製程 疑問                     | 1       | ian00727     |
| \[徵才\] 掃描器/光學元件/韌體工程師 BioInspira, Inc |         | Herc         |
| (本文已被刪除) \[Crosswise\]                        | 1       | -            |
| Re: \[心得\]小寶跟大寶 真的不一樣                   | 24      | ikeru        |
| Re: \[請益\] Offer請益 英業達/鴻海                  | 1       | wer11        |
| (本文已被刪除) \[pjc202\]                           |         | -            |
| Re: \[請益\] 陶氏化學CDP面試詢問                    | 8       | piggg        |
| 捷普 綠點刀具                                       | 3       | tn372845     |
| \[請益\] 日商安立知                                 | 4       | pjc202       |
| \[情報\] 蘋果申請具備iPhone核心之Macbook產品        | 5       | zxcvxx       |
| \[請益\]有人收到德州儀器技術行銷工程師面試邀請?     | 4       | wer11        |
| \[請益\] 請問陸資的IC設計公司                       | 10      | DigiTalent   |
| \[請益\] 德州儀器設備工程師實習                     | 4       | oeys         |
| \[討論\] 國家光電好嗎                               |         | chag06       |
| Re: \[請益\] 請問陸資的IC設計公司                   | 20      | DigiTalent   |
| \[請益\] 是否該調往偏鄉工作？                       | 52      | NakiXIII     |
| (本文已被刪除) \[lponnn\]                           | 5       | -            |
| \[請益\] 關於科技業或是保險                         | 3       | dfg512       |
| \[請益\] Advantest二手設備商                        | 5       | CA42         |
| Fw: \[請益\] 夜間進修                               |         | neon2102     |
| \[請益\] 華通電腦                                   | 6       | jackjack0805 |
| \[討論\] 矽品好像沒有板上說的那麼不好吧~            | 62      | goodlike     |
| (本文已被刪除) \[ScrewYou\]                         | 15      | -            |
| \[討論\] 台積電VS中油                               | 13      | ej4g4        |
| (本文已被刪除) \[p4818046\]                         | 1       | -            |
| \[請益\] 金屬工業中心面試                           | 1       | huaygina     |
| \[請益\] 在職碩班選擇請益，中興vs中央               | 11      | AKFG         |
| Re: \[討論\] 台積電VS中油                           | 7       | tomtowin     |
| \[請益\] 台積vs世界                                 | 51      | q7w8s5       |
| \[請益\] 暑期實習請益                               | 5       | quasi        |
| Fw: \[台北\] 推手媒體誠徵後端工程師                 |         | ssmartdan841 |
| (本文已被刪除) \[sheu123\]                          | 1       | -            |
| \[請益\] Offer請益(仁寶/緯創)                       | 16      | johnnypk321  |
| \[新聞\] 台積i8單 下月量產                          | 20      | unrest       |
| \[討論\] 聯穎光電面試                               |         | key9028      |
| \[請益\] 大中積體電路                               |         | pieceofacake |
| \[請益\] 弘馳公司 面試前的準備                      | 3       | AlioAlio     |
| \[討論\] 離職最後一根稻草                           | 49      | NTUlosers    |
| \[請益\]力成panel fan-out 製程整合 & 群創製程       | 5       | vacfann      |
| Re: \[討論\] 試用期超過三個月                       | 4       | dakkk        |
| \[討論\] （樹林）瑞傳 smt                           |         | usa71111     |
| \[請益\] 關於AirU x FinTech                         | 1       | Wizarc       |
| \[新聞\] 虧得一塌糊塗 太陽能矽晶圓廠等待黎明        | 16      | ErioT        |
| \[請益\] 台積測試設備助工                           | 22      | qlb144       |
| \[請益\] 推薦的layout工程師工作                     | 8       | ihavejason   |
| \[討論\] 一天實際工作的時數？                       | 8       | lukenming    |
| \[請益\] 面試要報告的 碩士論文                      |         | KIRA47       |
| \[心得\] 皮卡丘 五年工作心得                        | 23      | xx10231202   |
| \[請益\] 請問南科統新光訊                           | 3       | ggyy08957    |
| \[請益\] 新規則，休息日加班請假？                   | 14      | ggg1356114   |
| \[新聞\]新日光永旺能源獲8億聯貸 持續擴建太陽能      |         | moonth66     |
| \[新聞\] 工程師癱瘓全台YouBike 恐賠2242萬           | 28      | kellywu      |
| (本文已被刪除) \[hebeisme5566\]                     | 1       | -            |
| \[請益\] 台達研究院面試?                            | 3       | Aloha0527    |
| \[問卷\]數位族群數位金融潛力研究                    |         | olivesu      |
| \[請益\] 高雄日月光 offer                           | 12      | RacingSport  |
| Re: \[討論\] 台積電VS中油                           | 10      | FcukYouChina |
| \[請益\] 暢星科技                                   |         | Eighteen18   |
| \[新聞\] IC設計兩岸較勁 台廠轉型壓力加劇            | 8       | Nicher116    |
| (本文已被刪除) \[Kalisi\]                           | 6       | -            |
| \[討論\] 工程師的定義?                              | 29      | nhcuejunk    |
| Fw: \[徵才\]台中外商徵angular / hybrid app開發人員  |         | uborek       |
| \[請益\] Offer請益 怡利/友達                        | 4       | ccc0901      |
| \[請益\] 請問SKF這間公司                            |         | sercet0728   |
| \[請益\] offer請益 國巨/緯創                        | 2       | Pand         |
| \[徵才\] 北科車輛所徵求碩士級專任助理兩名           |         | Pocky5566    |
| \[請益\] 利得儀器-工程部助工                        |         | shinfon      |
| \[聘書\] 昇陽光電 VS 漢磊科技                       | 6       | qazwsx517    |
| Re: \[心得\] 皮卡丘 五年工作心得                    | 4       | magic704226  |
| 宜特 Ic 測試助理工程師面試                          | 2       | yens1        |
| (本文已被刪除) \[KEEPLOVING\]                       |         | -            |
| (本文已被刪除) \[scntu\]                            | 1       | -            |
| \[新聞\] 就是要力挺！仁寶參與樂視致新現增7億人      | 9       | wahaha23     |
| \[情報\] 智慧醫療人才培育計畫 徵求赴美人才          |         | Gojilla      |
| \[情報\] 智慧機械及航太研發補助計畫宣導說明會       |         | gil729181    |
| \[請益\] 漢民客服工程師（中科）                     | 10      | qoo63112000  |
| \[情報\] 台灣史丹福醫材人培計畫 徵求赴美人才        |         | Gojilla      |
| \[請益\] 有人聽過縯忠實業嗎？                       |         | foc0327      |
| \[請益\] 30歲製造業轉職                             | 7       | shesaya1     |
| Re: \[請益\] 新規則，休息日加班請假？               | 5       | eladamri     |
| \[問卷\] 科技業知識分享影響之探討(抽小七禮卷)       |         | awkman       |
| \[請益\] 台塑網面試                                 | 1       | pttstrider   |
| (本文已被刪除) \[d062637776\]                       | 1       | -            |
| (本文已被刪除) \[shrines\]                          |         | -            |
| \[請益\] 關於台積電分紅制度                         | X1      | likeyoutoboy |
| (本文已被刪除) \[likeyoutoboy\]                     |         | -            |
| \[請益\] 桃園和台北的薪水                           | 4       | J774         |
| \[請益\] offer請益 友達/華碩                        | 4       | s98115145    |
| \[請益\] 什麼狀況下會選擇"不"出國工作               |         | douglennon   |
| 律師為您解惑－線上勞動法免費諮詢即日為勞工 …        | 爆      | pzs          |
| \[公告\] Tech\_Job板板規 2014.03.01                 | 7       | mmkntust     |
| \[公告\] 置底 檢舉/推薦 文章                        | 爆      | mmkntust     |
| \[免費\]工作人生顧問                                | 爆      | zodiac       |

解釋爬蟲結果
------------

``` r
nrow(totalPage)
```

    ## [1] 106

124篇

``` r
table(totalPage$Author)
```

    ## 
    ##            -   c1823akimo    egnaro123         Herc     ian00727 
    ##           15            1            1            1            1 
    ##        ikeru    incoterms     jamiefly      key9028        piggg 
    ##            1            1            1            2            1 
    ##  simplep2002    tomandjim        wer11         xgin     yamakazi 
    ##            1            1            2            1            1 
    ##      ZhaoYun     zzzz8931         AKFG         CA42       chag06 
    ##            1            1            1            1            1 
    ##       dfg512   DigiTalent        ej4g4     goodlike     huaygina 
    ##            1            2            1            1            1 
    ## jackjack0805     NakiXIII     neon2102         oeys       pjc202 
    ##            1            1            1            1            1 
    ##     tn372845       zxcvxx     AlioAlio        dakkk        ErioT 
    ##            1            1            1            1            1 
    ##   ihavejason  johnnypk321       KIRA47    lukenming    NTUlosers 
    ##            1            1            1            1            1 
    ## pieceofacake       q7w8s5       qlb144        quasi ssmartdan841 
    ##            1            1            1            1            1 
    ##     tomtowin       unrest     usa71111      vacfann       Wizarc 
    ##            1            1            1            1            1 
    ##    Aloha0527      ccc0901   Eighteen18 FcukYouChina   ggg1356114 
    ##            1            1            1            1            1 
    ##    ggyy08957      kellywu     moonth66    nhcuejunk    Nicher116 
    ##            1            1            1            1            1 
    ##      olivesu         Pand    Pocky5566  RacingSport   sercet0728 
    ##            1            1            1            1            1 
    ##      shinfon       uborek   xx10231202       awkman     eladamri 
    ##            1            1            1            1            1 
    ##      foc0327    gil729181      Gojilla         J774 likeyoutoboy 
    ##            1            1            2            1            1 
    ##  magic704226   pttstrider    qazwsx517  qoo63112000     shesaya1 
    ##            1            1            1            1            1 
    ##     wahaha23        yens1   douglennon     mmkntust          pzs 
    ##            1            1            1            2            1 
    ##    s98115145       zodiac 
    ##            1            1

無發文最多之作者

124篇文章中有18篇被刪除
