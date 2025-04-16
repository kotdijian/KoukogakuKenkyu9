name: inverse
layout: true
class: center, middle, inverse
---
# ガイダンス・考古地理空間情報の基礎

## 考古学研究9 第1回目

[授業ページトップに戻る](https://kotdijian.github.io/KoukogakuKenkyu9/)

---
layout: false

###### 0
# 考古学研究9

## GISを利用した考古地理空間情報の解析

考古学研究において、地理空間情報は分布や地域性などの把握に不可欠なものであり、時間（時代・年代）情報と並び重要なデータである。この授業ではGIS（地理情報システム）の利用を前提として、考古地理空間情報データの取得・作成と各種分析方法、さらに統計解析用プログラミング言語であるRを用いた空間分析の手法などを、実習を交えて学ぶ。

---
###### 1
## 講師自己紹介
* 野口　淳（54）
* 公立小松大学次世代考古学研究センター特任准教授
* 産業技術研究所外来研究員、日本考古学協会理事、日本文化財保護協会顧問
* 日本とアジアの旧石器時代、3D計測、データベース、GIS、博物館デジタルアーカイブ

[![講師自己紹介1](https://raw.githubusercontent.com/kotdijian/KoukogakuKenkyu9/master/01/figs/Aboutme.png)](https://raw.githubusercontent.com/kotdijian/KoukogakuKenkyu9/master/01/figs/Aboutme.png)
[![講師自己紹介2](https://raw.githubusercontent.com/kotdijian/KoukogakuKenkyu9/master/01/figs/Aboutme2.png)](https://raw.githubusercontent.com/kotdijian/KoukogakuKenkyu9/master/01/figs/Aboutme2.png)

---
layout: true
###### 2

# 早速ですが、GIS知ってますか?
[![GISイメージ](https://raw.githubusercontent.com/kotdijian/KoukogakuKenkyu9/master/01/figs/GISimage01.png)](https://raw.githubusercontent.com/kotdijian/KoukogakuKenkyu9/master/01/figs/GISimage01.png)

---
layout: false
###### 3
## GISとは何か?

> 地理情報システム（GIS：Geographic Infor-mation System）は、地理的位置を手がかりに、位置に関する情報を持ったデータ（空間データ）を総合的に管理・加工し、視覚的に表示し、高度な分析や迅速な判断を可能にする技術である。
　[国土地理院「GISとは」](https://www.gsi.go.jp/GIS/whatisgis.html)

>　GIS（ジー アイ エス）とは（中略）日本語では地理情報システムと訳されます。　地球上に存在する地物や事象はすべて地理情報と言えますが、これらをコンピューターの地図上に可視化して、情報の関係性、パターン、傾向をわかりやすいかたちで導き出すのが GIS の大きな役割です。
　[Esriジャパン「GISをはじめよう　GISとは?」](https://www.esrij.com/getting-started/what-is-gis/)

>　地理情報システム（中略）とは、地理情報および付加情報をコンピュータ上で作成・保存・利用・管理・表示・検索するシステムを言う。
　[Wikipedia日本語版「地理情報システム」](https://ja.wikipedia.org/wiki/%E5%9C%B0%E7%90%86%E6%83%85%E5%A0%B1%E3%82%B7%E3%82%B9%E3%83%86%E3%83%A0)
---

###### 4
## GISの構成要件

> *地理情報システム（GIS：Geographic Infor-mation System）*は、<ins>地理的位置を手がかりに、位置に関する情報を持ったデータ（空間データ）</ins>を総合的に管理・加工し、視覚的に表示し、高度な分析や迅速な判断を可能にする技術である。
> *地理空間情報*とは、<ins>空間上の特定の地点又は区域の位置を示す情報（位置情報）</ins>と<ins>それに関連付けられた様々な事象に関する情報</ins>、もしくは位置情報のみからなる情報をいう。地理空間情報には、地域における自然、災害、社会経済活動など特定のテーマについての状況を表現する土地利用図、地質図、ハザードマップ等の主題図、都市計画図、地形図、地名情報、台帳情報、統計情報、空中写真、衛星画像等の多様な情報がある。
　[国土地理院「GISとは」](https://www.gsi.go.jp/GIS/whatisgis.html)
---

###### 5
## GISの構成要件：位置情報と関連情報    

.left-column[
### 位置情報
* どこにあるのか? 位置、場所、所在、範囲

  → 緯度経度、地理座標、地名、住所、郵便番号、標高、区域範囲、etc.
]
    
.right-column[
### 関連情報
* なにがあるのか?　地物・地形の種類や名称
* どのような状態なのか?
* 付随するもの
* 関連する他の事物・事象
]
    
---
###### 6
## GISの機能

> *地理空間情報*は、その<ins>位置情報をキーにして異なるデータを重ね合わせる</ins>ことで、分析等の活用がなされることから、様々な主体によって整備されるデータ間で位置情報の整合がとれている必要がある。このためには、<ins>地理空間情報を空間上の位置に対応づけるための基準となる基盤地図情報</ins>の整備・更新・提供が必要である。
> 基盤地図情報とは、地理空間情報活用推進基本法第2条第3項において（中略）定義された、電子的な地理空間情報である。地理空間情報の整備に基盤地図情報が活用されることにより、地理空間情報の相互活用が容易になる。
　[国土地理院「GISとは」](https://www.gsi.go.jp/GIS/whatisgis.html)

---
###### 7
## GISの機能を可能にする付加的な要素

.left-column[
### キー：データ管理
* 個々のデータを区別するためのID（UID）・識別子
* データを紐づけるための参照・関係情報
]
    
.right-column[
### 基盤地図情報
* データ・情報の空間的位置・背景を明らかにする
]

---
###### ８
## あらためてGISとは?

.left-column[
1. 位置情報
2. 関連情報
3. キー
4. 基盤地図情報    
]

.right-column[
**GIS＝データ+地図**

データベース＝構造化されたデータが、検索、演算等利用可能な状態で格納されている

それが地図と連動して、地図上で展開する＝GIS

[![GISモデル](https://raw.githubusercontent.com/kotdijian/KoukogakuKenkyu9/master/01/figs/EsriGISmodel.png)](https://raw.githubusercontent.com/kotdijian/KoukogakuKenkyu9/master/01/figs/EsriGISmodel.png)

---
###### 9
## GISソフト
* [QGIS](qgis.org/ja/site/)　(QGIS Develpment Team)　オープンソース、無償
* [ArcGIS](https://www.esrij.com/products/arcgis/) (Esri)　商業ソフト、有償

## WebGIS
#### ウェブブラウザ上で機能するウェブアプリ。インターネット接続が必須
* [地理院地図](https://maps.gsi.go.jp/index.html) (国土地理院)
* [ひなたGIS](https://hgis.pref.miyazaki.lg.jp/hinata/) （宮崎県）
* [open-hinata](https://kenzkenz.xsrv.jp/open-hinata/)　(@kenzkenz)
* [open-hinata3](https://kenzkenz.xsrv.jp/open-hinata3/) (@kenzkenz)
* [Google Earth](https://www.google.co.jp/earth/) (Google LLC/ Alphabet)
* [Googleマイマップ](https://www.google.co.jp/intl/ja/maps/about/mymaps/) (Google LLC/ Alphabet)

#### ウェブ地図サービスとWebGISの違い・接点を考えてみよう

###### 10
## 考古学GISの一般的なデータモデル

* ID：遺跡番号、調査地点・次数、遺構番号等
* 名称：遺跡・遺跡群、調査区・地区、地点・トレンチ、遺構等
* 位置：緯度経度、国土座標、住所等
* 範囲：代表点、または範囲を区切る多角形
* 時代：考古学的時代・時期区分、年代等
* 種別：遺跡・遺構の種別
* その他属性情報：遺物、その他の痕跡、理化学的分析等

---
###### 11
## 考古学GISの一般的な実装＝遺跡地図
#### [東京都遺跡地図情報インターネット提供サービス](https://tokyo-iseki.metro.tokyo.lg.jp/)
* 東京都内の各自治体の遺跡地図・台帳データ
  - 遺跡番号、遺跡名、所在地（住所）、時代、種別（遺跡種別）、主な遺構、主な出土品
  - 属性から検索が可能
* 国土地理院の標準地図を背景とする

[![東京都遺跡地図](https://raw.github.com/kotdijian/KoukogakuKenkyu9/master/01/figs/TokyoMETmap.png)](https://raw.github.com/kotdijian/KoukogakuKenkyu9/master/01/figs/TokyoMETmap.png)   

---
###### 12
## 東京都遺跡地図情報インターネット提供サービスはGISか?
* データベース＝遺跡台帳
* 基盤地図情報＝地理院地図
* 検索が可能
### ただし...
* フロントエンド（利用者から見える部分）では地図サービスのように見える
* バックエンド（裏方）にはデータベースがある＝GIS

## GIS（WebGIS）とは言えないオンライン遺跡地図
* 画像またはPDFファイルでの公開
  - 紙の地図をウェブ上に置いただけ
  - 遺跡位置、名称、内容は目視確認＝検索性がない

#### 考古学の要素が従：「地域史」研究

**地域史とは?**
* 一定の「地域」の歴史、「郷土史」とも <> 「日本史」や「世界史」と対比される  
* 「地域」の範囲は地理的、歴史的、文化的に設定される  
* 設定された範囲における時期・時代を越えた通史的な研究   
* 複数・多数の要素（遺物・遺構等）を取り扱う  

---
###### 8
## 考古学における地域研究2
#### 地域史の例  

**自治体史（都道府県・市町村史）**
* ある自治体の範囲の歴史（および関連分野）を網羅する
    * 例）『新修港区史』[ADEAC デジタル版港区のあゆみ](https://trc-adeac.trc.co.jp/WJ11D0/WJJS05U/1310305100/1310305100100010?dtl=all)  
        * 地形（地質）・環境  
        * 原始・古代（考古学中心）  
        * 中世・近世・近代（文献史学中心）  

---
###### 9
## 考古学における地域研究3
#### 景観論

* 歴史地理学
    * [『地形からみた歴史』](https://bookclub.kodansha.co.jp/product?item=0000211623)  

* 環境考古学  
    * ["Archaeology as Human Ecology"](https://www.cambridge.org/core/books/archaeology-as-human-ecology/C7ED4A520324242015F56A2CA8EF6BB7)  

* 景観考古学
    * [『景観考古学の方法と実践』](http://www.douseisha.co.jp/book/b245310.html)

---
###### 10
## 考古学における地域研究+
#### 理論研究：考古学における地域とはなにか?

* 集団・社会ネットワーク

* 中心と周縁

* 民俗知・民族知と生活空間認識

---
###### 11
## ちょっと休憩
#### どんな地域研究をやってみたいですか?
    ・群馬県の古墳について  
    ・地元青森に関する研究  
    ・災害、戦争の前後と地域形成（広島の復興とか…）  
    ・吉田新田について  
    ・出雲の大和政権と異なる文化の地域史研究  
    ・横浜の地域に関する研究  
    ・小平市周辺、小金井市など大学周辺の地域の遺跡など  
    ・小平市の江戸時代においての開発  
    ・山梨県の古墳の分布  
    ・相模原の江戸時代の地域史、林業など  
    ・文献や言い伝えなどに対して、それらの遺構・遺跡が実際にあるのか、そ　　　　　　の痕跡などはないかの研究  
    ・国分寺崖線近辺の遺跡について  
    ・鹿児島県（薩摩）の地域史／薩摩の近代化遺産  
    ・地域の民族文化  
    ・水戸市に関する研究、とくに江戸時代の土地の変化（埋め立てなど）  
    ・野川周辺と台地上の地域発展の違い（自然環境がどのくらい地域の発展に影響を与えるのか具体的に見てみたい）  
    ・認知地域としての「都市」に関する地域研究　※時間軸は中世に固定  
    ・西多摩の地域史研究／玉川上水が開通したことによる、武蔵野地域の発展について  
    ・現在の世田谷区に住んでいた人々の生活と多摩川との関係  

---
###### 12
## 考古学における地域研究の方法

* テーマの設定：地域、対象資料

* 資料の探索・収集

* 地図・分布図の作成

---
###### 13
## 地域資料の調べ方

* [図書館](http://library.u-gakugei.ac.jp/)
    * [OPAC](https://library.u-gakugei.ac.jp/opac/complexsearch)

* [全国遺跡報告総覧](https://sitereports.nabunken.go.jp/ja)

* [国立情報学研究所 CiNii Books](https://ci.nii.ac.jp/books/)

* [国立国会図書館サーチ](https://iss.ndl.go.jp/)

* [国立科学振興機構 J-STAGE](https://www.jstage.jst.go.jp/browse/-char/ja/)

* [TRC-ADEAC](https://trc-adeac.trc.co.jp/)

* [機関リポジトリ](https://library.u-gakugei.ac.jp/etopia/top.html)

---
###### 14
## 2020年5月「今」の状況を考える
* 調べる対象はどれだけあるのか?
    1. NDL Search：タイトル=考古学 AND 出版地=日本, データベース=国立国会図書館オンライン, 資料種別=本, 所蔵館=国立国会図書館 or 他機関  
    2. CiNii Books, タイトル=考古学, 資料種別=図書・雑誌, 言語種別=日本語  

|年代|NDL Search|CiNii Books|増加率N|増加率C|
|:---------:|----:|----:|-----:|-----:|
|～1950|283|430|---|---|
|1951～1960|148|167|---|---|
|1961～1970|186|250|125.7%|149.7%|
|1971～1980|408|537|219.4%|214.8%|
|1981～1990|631|820|154.7%|152.7%|
|1991～2000|951|1469|150.7%|179.1%|
|2001～2010|1696|1772|178.3%|120.6%|
|2011～2020|1308|1243|77.1%|70.1%|

---
###### 14-2
## 2020年5月「今」の状況を考える2

* [「図書館休館で「論文が間に合わない」 コロナ禍の「若手研究者」に降りかかる困難」弁護士ドットコムニュース(2020/5/14)](https://www.bengo4.com/c_23/n_11216/)  

* [東大図書館休館問題を考える有志ウェブサイト](https://utclosedlib2020.wixsite.com/website)

---
###### 15
## 著作物の利用と著作権法

* [CRIC（公益社団法人著作権情報センター）](https://www.cric.or.jp/index.html)  
    * [著作物が自由に使える場合は?](https://www.cric.or.jp/qa/hajime/hajime7.html)

* [JRRC（公益社団法人日本複製権センター）](https://jrrc.or.jp/)  
    * [13．学校の授業で書籍などから複写して教材として使用することはできますか？](http://www.jbpa.or.jp/pdf/guideline/act_article35_guideline.pdf)  

* 大学学習資源コンソーシアム（ＣＬＲ） 
    * [大学学習資源における著作物の活用と著作権大学学習資源コンソーシアム（ＣＬＲ）](http://clr.jp/servicemenu/guideline_jpn.pdf)

---
###### 16
## 著作権法35条の改正と令和2年度の特例  

* [文化庁　著作権](https://www.bunka.go.jp/seisaku/chosakuken/index.html)
    * [著作権法の一部を改正する法律 概要](https://www.bunka.go.jp/seisaku/chosakuken/hokaisei/h30_hokaisei/pdf/r1406693_01.pdf)

* [著作物の教育利用に関する関係者フォーラム](https://forum.sartras.or.jp/info/004/)
    * 「改正著作権法第３５条運用指針（令和２（2020）年度版）」を公表    
        * https://forum.sartras.or.jp/info/004/
        * https://forum.sartras.or.jp/wp-content/uploads/kongounyo.pdf
        * https://forum.sartras.or.jp/wp-content/uploads/unyoshishin2020.pdf

---
###### 17
## 事後学習課題

1. 地域研究資料をオンラインで検索する
2. Googleスプレッドシートで一覧表を作成する（テンプレートあり）
3. テーマは授業中に考えたものでも良いし、変更しても良い
4. 質問・相談はSlackへ

---
###### 18
## 参考文献

* 小野　昭 1978 「分布論」『日本考古学を学ぶ1』有斐閣    
* 日下雅義 1991 『古代景観の復元』講談社（2012『地形からみた歴史』講談社学術文庫）  
* 佐原　眞 1985 「分布論」『岩波講座日本考古学1』岩波書店    
* 鈴木公雄 1988 『考古学入門』東京大学出版会    
* 太郎良真妃 2019 「多属性の統計解析による土器様式の空間分析」『考古形態測定学ワークショップ#01〈かたち〉を測る・分ける・読み解く－考古学における形態の測定と理解とは何か－』考古形態測定学研究会  
* 戸沢充則 1986a「総論」『岩波講座日本考古学5』岩波書店    
* 戸沢充則 1986b「縄文時代の地域と文化」『岩波講座日本考古学5』岩波書店    
* 横山浩一 1978 「考古学とはどんな学問か」『日本考古学を学ぶ1』有斐閣    

---
###### 19
## ご案内

**[3D写真計測ワークショップ](https://kotdijian.github.io/arch3dphotogrammetry/)をオンラインで開催します。興味のある方はどうぞ**

---
