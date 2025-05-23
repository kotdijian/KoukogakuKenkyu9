name: white
layout: true
class: center, middle, white
---
# WebGISの利用
# （地理院地図、ひなたGIS）

## 考古学研究9
#### 第3回目(2025/5/1)

[授業ページトップに戻る](https://kotdijian.github.io/KoukogakuKenkyu9/)
---
layout: false

###### 1
# GitHubの使い方

### リポジトリのフォーク
* [公式ドキュメント](https://ja.wikipedia.org/wiki/GitHub)

* 自分のものではない、第三者の公開リポジトリをローカルにクローンすることができる
* しかし変更をコミットすると大元のリポジトリに反映されてしまう
* 自分だけの作業用のリポジトリとしたい時はFolk（フォーク）を使う
* 大元のリポジトリに統合（Merge: マージ）することもできる

---

###### 2
### リポジトリのフォークを試してみよう
* [JASOSR:日本考古のための空間データ基盤（公開リポジトリ）](https://github.com/kotdijian/JASOSR)
* リポジトリの概要欄の上にある"folk"をクリックして自分のアカウントにフォークする
* 自分のアカウントにJASOSRリポジトリが生成されたのを確認したら、Github Desktopでローカルにクローンする
* 当面は"13Tokyo"だけを使うので他のフォルダは削除してもOK

---

###### 3
### フォークしたリポジトリで作業してみよう
* "13Tokyo"フォルダには、[東京都遺跡地図情報インターネット提供サービス](https://tokyo-iseki.metro.tokyo.lg.jp/)から作成した東京都遺跡一覧データがあります（島嶼部除く）
* 基本的な内容：JASID+自治体コード+東京都遺跡地図収録8項目（遺跡番号、ふりがな、遺跡名、所在地、時代、種別、主な遺構／概要、主な出土品）+位置座標
* 13Tokyo_total.csv　東京都遺跡地図搭載全テータ（抹消含む）
* 13Tokyo.csv　整備済みデータ（抹消等問題データ除去）
* 'byAge'　時代別データ

### 分布図用データの作成
* csvファイルをExcel, Numbers, スプレッドシートで開き、フィルターなどを用いて編集する 
* 時代、遺跡種別、主な遺構、主な出土品...
* csvファイルを別名で保存→自分のリポジトリにプッシュ
* リモートリポジトリに反映されていることを確認
* ローカルリポジトリ＝自分専用、リモートリポジトリ＝公開共有可能

---

###### 4
### 地理院地図
* 「地形図、写真、標高、地形分類、災害情報など、日本の国土の様子を発信するウェブ地図です。地形図や写真の3D表示も可能。」
* 2013年に運用開始
* 多彩な地図を利用できる
* 画像やPDFに出力できる
* 自分自身でデータを作成、保存できる

---

###### 5
### 地理院地図を操作してみよう
#### [地理院地図](https://maps.gsi.go.jp) の画面構成と機能

#### 自分のデータを読み込む
* マーカーの種類、色とサイズを変更する
* レイヤーを作成する
* ポイントを追加する
* ポイントの情報を修正する
* データを書き出す

---

###### 6
### 地理情報データの種類
##### .csv (.tsv, .txt)：カンマ区切りテキスト
* 属性データをカンマ（またはタブ等の区切り記号）で連記する
* 最もシンプル、編集が容易 < > ライン、ポリゴンデータの記述は困難
* 多くアプリケーションで利用可能

##### .geojson：ジオジェイソン
* [JSON (JavaScript Object Notation)](https://ja.wikipedia.org/wiki/JavaScript_Object_Notation)
* ウェブにおけるデータ交換形式として発展
* ライン、ポリゴンデータの記述が可能 < > 記述が複雑、専用エディタがないと編集は困難

##### .kml：ケーエムエル
* GoogleEarthの前進"Keyhole"のデータフォーマットとして開発、現在はオープンソース
* XMLベース
* ライン、ポリゴンデータの記述が可能 < > 記述が複雑、専用エディタがないと編集は困難

---

###### 7
###### .csv

```
"JASID","自治体コード","遺跡番号",,"経度","緯度",
13101000100,13101,"1",139.757489,35.68619003
```


###### .geojson

```
{"type": "FeatureCollection","features": [
     {"type": "Feature","geometry":
       {"type": "Point","coordinates": [139.757489, 35.68619]},
      "properties": {"JASID": "13101000100", "自治体コード": "13101", "遺跡番号": "1",
                     "経度": "139.757489", "緯度": "35.68619003",
                     "_markerType": "Icon",
                     "_iconUrl": "https://maps.gsi.go.jp/portal/sys/v4/symbols/081.png",
                     "_iconSize": [10, 10], "_iconAnchor": [5, 5]}
       }
```


###### .kml
```
<Placemark>
<description><![CDATA[ <table><tr><td>JASID</td><td>13101000100</td></tr>
<tr><td>自治体コード</td><td>13101</td></tr><tr><td>遺跡番号</td><td>1</td></tr>
<tr><td>経度</td><td>139.757489</td></tr><tr><td>緯度</td><td>35.68619003</td></tr>
</table> ]]></description>
<styleUrl>#PolyStyle1</styleUrl>
<Point>
<coordinates>139.757489,35.68619003</coordinates>
</Point>
</Placemark> 
```

---

###### 8
### データ形式の比較（続）　第2回を思い出して
##### 人間可読（Human-readable）か、機械可読（Machine-readable）か
* .csv＝項目数が増えると人間による読み取りは困難

  **>> Excel、スプレッドシートなど広く使われているエディタで編集や整形が容易**

  < > 複雑な構造を記述できない（多数の点と辺で構成されるラインやポリゴンなど）


* .geojson, .kml＝ぱっと見で読めない、テキストエディタや表計算ソフトでの編集も困難

　**>> ラインやポリゴンなど、ポイントだけでない地物の表現が可能**

  > > JSONやxmlによる構造化（入れ子）のデータ記述が可能

  < > .csvは１項目ずつ区切らなければならない＝点・辺の数だけ区切られた項目が発生

---

###### 9
### 地理院地図の**PROS and CONS**
.left-column[
#### PROS
* 背景地図が豊富
* データ読み取りが直感的に行える
* 画像出力や印刷が容易
* 複数のデータセットをレイヤー状に扱える
]

.right-column[
#### CONS
* データ書き出しが.geojsonと.kmlのみ

** >>　地理院地図外での再編集・操作が困難**
]

---

###### 10
### [ひなたGIS](https://hgis.pref.miyazaki.lg.jp/hinata/)
* 宮崎県職員の落合謙次氏（@kenzkenz）が開発、宮崎県が運用している
* 地理院地図にはない背景地図も利用できる
* 地理院地図にはないGIS機能を持つ
* **データ読み込みは
  ***シフトJIS***
  という文字エンコードでなければならない**

---

###### 11
### エンコードってなに?
* コンピューターは文字や数字をそのまま読み込めない >> 16進数のコード（機械語）に翻訳する
* 英数字はユニコード（Unicode）という統一的なエンコードが整備されている（現在主流はUTF-8）
* Microsoft OSは独自のエンコードを使ってきた。日本語環境はシフトJIS（CP932）

### シフトJISデータの作成（変換）
* テキストエディタ等でエンコードを指定することで変換して保存ができる
* JASOSRリポジトリの"13Tokyo"フォルダには、サブフォルダ"SJS"にシフトJIS変換データを保存している


---

###### 12
### [ひなたGIS](https://hgis.pref.miyazaki.lg.jp/hinata/)を使ってみよう
1. シフトJISデータを用意する
2. シフトJISデータをドラッグ&ドロップする、または画面上を右クリック > ファイル読み込み
3. 位置座標の入っていない行があると読み込みを停止するので注意!
4. マーカーの色やサイズは外部で修正する必要

---

###### 13
### 地理院地図とひなたGISの比較（当社比） 用途によって使い分けよう
.left-column[
#### 地理院地図は地図作成と出力に適した機能が多い
]

.right-column[
#### ひなたGISはデータの外部書き出しと編集に便利
]

---


###### 14
### 次回予告：地理院地図またはひなたGISで自分のテーマの分布図を作成する

#### 基本的に [「もくもく会」](https://ja.wikipedia.org/wiki/%E3%82%82%E3%81%8F%E3%82%82%E3%81%8F%E4%BC%9A_(%E9%9B%86%E4%BC%9A) 形式で行います。
#### 授業時間内に操作方法等の質問を受け付けます
#### 成果物は成績評価の対象として提出してもらいます
#### 詳細は次回説明します
