name: inverse
layout: true
class: center, middle, inverse
---
# ガイダンス・考古地理空間情報の基礎

## 考古学研究9
#### 第1回目

[授業ページトップに戻る](https://kotdijian.github.io/KoukogakuKenkyu9/)
---

name: white
layout: true
class: center, middle, white
---
###### 0
# 考古学研究9

## GISを利用した考古地理空間情報の解析

考古学研究において、地理空間情報は分布や地域性などの把握に不可欠なものであり、時間（時代・年代）情報と並び重要なデータである。この授業ではGIS（地理情報システム）の利用を前提として、考古地理空間情報データの取得・作成と各種分析方法、さらに統計解析用プログラミング言語であるRを用いた空間分析の手法などを、実習を交えて学ぶ。

---
layout: false

###### 1
## 講師自己紹介
* 野口　淳（54）
* 公立小松大学次世代考古学研究センター特任准教授
* 産業技術研究所外来研究員、日本考古学協会理事、日本文化財保護協会顧問
* 日本とアジアの旧石器時代、3D計測、データベース、GIS、博物館デジタルアーカイブ

[![講師自己紹介1](https://raw.githubusercontent.com/kotdijian/KoukogakuKenkyu9/master/01/figs/Aboutme.png)](https://raw.githubusercontent.com/kotdijian/KoukogakuKenkyu9/master/01/figs/Aboutme.png)
[![講師自己紹介2](https://raw.githubusercontent.com/kotdijian/KoukogakuKenkyu9/master/01/figs/Aboutme2.png)](https://raw.githubusercontent.com/kotdijian/KoukogakuKenkyu9/master/01/figs/Aboutme2.png)

* 受講生の皆さんについて教えてください
  - お名前・学年・専門・この授業に期待すること
---
name: inverse
layout: true
class: center, middle, inverse###### 2
---

###### 2
# 早速ですが、GIS知ってますか?
[![GISイメージ](https://raw.githubusercontent.com/kotdijian/KoukogakuKenkyu9/master/01/figs/GISimage01.png)](https://raw.githubusercontent.com/kotdijian/KoukogakuKenkyu9/master/01/figs/GISimage01.png)

* GISについて知っていることを教えてください

---
layout: false
###### 3
## GISとは何か?

> 地理情報システム（GIS：Geographic Infor-mation System）は、地理的位置を手がかりに、位置に関する情報を持ったデータ（空間データ）を総合的に管理・加工し、視覚的に表示し、高度な分析や迅速な判断を可能にする技術である。
<div style="text-align: right;"> 
  <a href="https://www.gsi.go.jp/GIS/whatisgis.html">国土地理院「GISとは</a>
</div>


>　GIS（ジー アイ エス）とは（中略）日本語では地理情報システムと訳されます。　地球上に存在する地物や事象はすべて地理情報と言えますが、これらをコンピューターの地図上に可視化して、情報の関係性、パターン、傾向をわかりやすいかたちで導き出すのが GIS の大きな役割です。
<div style="text-align: right;">
  <a href="https://www.esrij.com/getting-started/what-is-gis/">Esriジャパン「GISをはじめよう　GISとは?」</a>
</div>


>　地理情報システム（中略）とは、地理情報および付加情報をコンピュータ上で作成・保存・利用・管理・表示・検索するシステムを言う。
<div style="text-align: right;">
  <a href="https://ja.wikipedia.org/wiki/%E5%9C%B0%E7%90%86%E6%83%85%E5%A0%B1%E3%82%B7%E3%82%B9%E3%83%86%E3%83%A0">Wikipedia日本語版「地理情報システム」</a>
</div>

---
###### 4
## GISの構成要件

> *地理情報システム（GIS：Geographic Infor-mation System）*は、<ins>地理的位置を手がかりに、位置に関する情報を持ったデータ（空間データ）</ins>を総合的に管理・加工し、視覚的に表示し、高度な分析や迅速な判断を可能にする技術である。
> *地理空間情報*とは、<ins>空間上の特定の地点又は区域の位置を示す情報（位置情報）</ins>と<ins>それに関連付けられた様々な事象に関する情報</ins>、もしくは位置情報のみからなる情報をいう。地理空間情報には、地域における自然、災害、社会経済活動など特定のテーマについての状況を表現する土地利用図、地質図、ハザードマップ等の主題図、都市計画図、地形図、地名情報、台帳情報、統計情報、空中写真、衛星画像等の多様な情報がある。
<div style="text-align: right;"> 
  <a href="https://www.gsi.go.jp/GIS/whatisgis.html">国土地理院「GISとは</a>
</div>


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
<div style="text-align: right;"> 
  <a href="https://www.gsi.go.jp/GIS/whatisgis.html">国土地理院「GISとは</a>
</div>


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
<div style="text-align: right;">
  (c)Esri Japan 
  <a href="https://www.esrij.com/getting-started/what-is-gis/">Esriジャパン「GISをはじめよう　GISとは?」</a>
</div>


---
###### 9
## GISソフト
* [QGIS](qgis.org/ja/site/)　(QGIS Develpment Team)　オープンソース、無償
* [ArcGIS](https://www.esrij.com/products/arcgis/) (Esri)　商業ソフト、有償

<details>
<summary>

## WebGIS
</summary>

#### ウェブブラウザ上で機能するウェブアプリ。インターネット接続が必須
* [地理院地図](https://maps.gsi.go.jp/index.html) (国土地理院)
* [ひなたGIS](https://hgis.pref.miyazaki.lg.jp/hinata/) （宮崎県）
* [open-hinata](https://kenzkenz.xsrv.jp/open-hinata/)　(@kenzkenz)
* [open-hinata3](https://kenzkenz.xsrv.jp/open-hinata3/) (@kenzkenz)
* [Google Earth](https://www.google.co.jp/earth/) (Google LLC/ Alphabet)
* [Googleマイマップ](https://www.google.co.jp/intl/ja/maps/about/mymaps/) (Google LLC/ Alphabet)

#### ウェブ地図サービスとWebGISの違い・接点を考えてみよう
</details>

---
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
## 東京都遺跡地図情報インターネット提供サービスはGIS?
* データベース＝遺跡台帳
* 基盤地図情報＝地理院地図
* 検索が可能
### ただし...
* フロントエンド（利用者から見える部分）では地図サービスのように見える
* バックエンド（裏方）にはデータベースがある＝GIS

---
###### 13
## GIS（WebGIS）とは言えないオンライン遺跡地図
* 画像またはPDFファイルでの公開
  - 紙の地図をウェブ上に置いただけ
  - 遺跡位置、名称、内容は目視確認＝検索性がない

## 全国の遺跡地図を探してみよう

---
###### 14
## 遺跡地図のデジタル化について
* [板倉有大(2019)「福岡市埋蔵文化財課のGISとその活用」『デジタル技術による文化財情報の記録と利活用1』奈良文化財研究所研究報告21](http://doi.org/10.24484/sitereports.33189-11946)
* [高田祐一・武内樹治(2021)「刊行物およびGISによる遺跡地図の公開状況」『デジタル技術による文化財情報の記録と利活用3』奈良文化財研究所研究報告27](http://doi.org/10.24484/sitereports.90271-15019)
* [中居和志(2019)「京都府・市町村共同統合型地理情報システム（GIS）における遺跡マップの活用について」 『デジタル技術による文化財情報の記録と利活用』奈良文化財研究所研究報告21](http://doi.org/10.24484/sitereports.33189-11945)
* [奈良文化財研究所文化財情報研究室(2021)『全国遺跡地図総目録』](http://doi.org/10.24484/sitereports.90060)
* [野口　淳(2021)「考古学・文化財地理空間情報のオープンデータ化、整備と活用」 『デジタル技術による文化財情報の記録と利活用3』奈良文化財研究所研究報告27](http://doi.org/10.24484/sitereports.90271-15056)
* [野口　淳(2022)「考古学・埋蔵文化財GISデータの標準化、ファイルフォーマット、オープン化」 『デジタル技術による文化財情報の記録と利活用4』奈良文化財研究所研究報告33](http://doi.org/10.24484/sitereports.115736-63532)
* [藤井幸司(2022)「遺跡地図の行政的な位置づけとデジタル化動向等について」 『デジタル技術による文化財情報の記録と利活用4』奈良文化財研究所研究報告33](http://doi.org/10.24484/sitereports.115736-63529)
---
###### 15
## 全国文化財総覧（旧・全国遺跡報告総覧）と[文化財総覧WebGIS](https://heritagemap.nabunken.go.jp/)

[![総覧WebGIS](https://raw.github.com/kotdijian/KoukogakuKenkyu9/master/01/figs/SORAN.png)](https://raw.github.com/kotdijian/KoukogakuKenkyu9/master/01/figs/SORAN.png)   
