# 考古地理空間情報分析のためのQGIS操作マニュアル
#### ver.2025.00
 - 本マニュアルはQGIS 3.40 に準拠しています
 - QGISは2025年10月に4.0へのメジャーアップデートが予定されていますがメニューや操作方法に大きな変化はないとのことです
  * 【参考】[MIERUNE QGISLAB](https://qgis.mierune.co.jp/posts/blog_qgis-4-0_qt6)

#### 役にたつリソース
- [公式ユーザーガイド](https://docs.qgis.org/3.40/ja/docs/user_manual/index.html)
- [MIERUNE QGISLAB](https://qgis.mierune.co.jp/)

#### [2025年度授業ページトップに戻る](https://kotdijian.github.io/KoukogakuKenkyu9/)

---
### 1.基本設定
#### QGISのセットアップ

- ダウンロードサイト：https://www.qgis.org/download/
    * LTR (Long Term Release) またはLong Term Versionをインストールする
- 解説：https://qgis.mierune.co.jp/posts/howto_1_install_qgis

#### QGISを起動する

- 起動画面で「新規プロジェクト」を選択する。またはツールバーの「新規プロジェクト」ボタンをクリックするか、メニュー「プロジェクト」から「新規」を選択する
- 解説：https://qgis.mierune.co.jp/posts/howto_1_about_screen

#### プロジェクトのCRSを設定する

- CRS (Coordinates Reference System：座標参照系) は、地図や地物の位置や形状を描画するときの基準
- 球体としての地球の中心を原点として角度（緯度・経度）で位置を示す地理（地心）座標系と、球体の表面の特定の範囲に投影された平面を直角に区分して位置を示す平面直角座標系（投影座標系とも）がある
- CRSはEPSGコードと呼ばれる国際的な標準コードで整理されている
  - EPSG4326 (WGS84)　地球規模の範囲をカバーする地理座標系、GPS/GNSSでも使用される。単位は度
  - EPSG3857 (Webメルカトル）　Web地図などで用いられる投影座標系。地球規模の範囲を正方形で表示。単位はm。
  - EPSG6668 (JGD2011) WGS84に基づき定められたJGD2000を、東日本大震災後に改訂したもの。地理座標系。単位は度。
  - EPSG6669〜6687 (JGD2011平面直角座標系／国土座標） 日本全体をI〜XIXの19の区域に区分した平面直角座標系。単位はm。東京都はIX系 (EPSG6677)に含まれる。
- メニュー「プロジェクト」から「プロパティ」を開き、「CRS（座標参照系）」タブで設定
  - 今回はEPSG3857で


- **オンザフライ**：QGISは異なる座標系のデータも自動的にプロジェクトのCRSで表示する機能を持っている。ただし有効でない場合も。
- 地図や地物がうまく表示されない時はレイヤのプロパティ（またはレイヤのCRS）から修正する

- 国土地理院：日本の測地系　https://www.gsi.go.jp/sokuchikijun/datum-main.html
- 解説：https://qgis.mierune.co.jp/posts/howto_set_crs
- トラブルシューティング：https://qgis.mierune.co.jp/posts/howto_crs_faq

---
### 2. 地図の表示

#### タイル地図を表示する

- ブラウザパネルの"XYZ Tiles"を右クリックして「新規接続」を選択
    - 例）地理院標準地図＝"https://cyberjapandata.gsi.go.jp/xyz/std/{z}/{x}/{y}.png"
- 「名前」にタイル地図の名称、「URL」にタイル地図のURLを入力する
    - 地理院タイル一覧：https://maps.gsi.go.jp/development/ichiran.html
    - すでに目的のタイル地図がブラウザパネルにある場合はダブルクリック
- 国土地理院：地理院タイルについて　https://maps.gsi.go.jp/development/siyou.html
- 解説：https://qgis.mierune.co.jp/posts/howto_1_add_xyztiles

#### ラスタデータを読み込む
1. 位置情報を含むGeoTiffファイル等をマップキャンパス（メインの地図画面）にドラッグ&ドロップする
2. またはメニュー「レイヤ」から「レイヤを追加」>「ラスタレイヤを追加」を選択し、表示されるパネルの「ソース」セクションの「ラスタデータセット」で開くファイルを指定する
   * 複数のファイルに分割されている場合、レイヤをグループ化すると便利

#### ラスタデータを読み込む2:
0. DEM=Digital Elevation Model（数値標高モデル）、指定された区画（メッシュ）内の地表の標高（代表値）データで構成された地理空間情報
1. 基盤地図情報ダウンロードサービスからDEMデータをダウンロードする
     - 基盤地図情報ダウンロードサービス：https://service.gsi.go.jp/kiban/
     - 初回アカウント登録が必要
     - 1m、5m、10mメッシュのデータがある。メッシュが小さいほどモデルは細かいが、同じ面積に対してデータサイズが大きくなる
     - 今回は10mメッシュ(10B)をダウンロード
     - 地図上のグリッドをクリックして範囲を指定、ダウンロード
2. ダウンロードデータを解凍し確認する
     - 拡張子.xmlのファイルでGeoTiffではない！
     - XMLをGeoTiffに変換するプラグイン(QuickDEM4JP)がある！ https://qiita.com/nokonoko_1203/items/b99aa733cb215305f8aa
3. ダウンロードしたXMLをまとめて一つのGeoTiffに変換し、ラスタレイヤに追加する
      - メニュー「ラスタ」から「その他」>「結合(gdal merge)」を選択、結合するレイヤと書き出し先を指定

#### ラスタデータの表示を変える
1. 「レイヤのプロパティ」>「シンボロジ」
2. レンダリングタイプの選択
   - 単バンドグレー
   - 単バンド擬似カラー
   - 陰影図 (hillshade)
   - 投稿線 (contours)
3. 単バンド擬似カラーでカラーランプを選択、編集する

#### 【応用編】 DEMデータの表示を変える
- 陰影図：標高データの場合「バンド1」を選択、照射される光線の高度・方位角を指定、「Z係数」（標高の倍率）を指定
![Hillshade](https://github.com/kotdijian/KoukogakuKenkyu9/blob/main/Figures/Hillshade.png)   

- 等高線：標高データの場合「バンド1」を選択、「等高線（基準等高線）の間隔」（＝等高線の標高値）を指定
![Contour](https://github.com/kotdijian/KoukogakuKenkyu9/blob/main/Figures/Contour.png)   

---
### 3. 地図の表示2： ベクターデータ

#### ベクタデータ（ポイントデータを含む）を読み込む
1. 正しい形式のベクタデータファイルをマップキャンパスにドロップする
2. またはメニュー「レイヤ」から「レイヤを追加」>「ベクタレイヤを追加」を選択し、表示されるパネルの「ソース」セクションの「ベクタデータセット」で開くファイルを指定、「追加」をクリックする
3. CSV形式のポイントデータの場合、 メニュー「レイヤ」から「レイヤを追加」>「CSVテキストレイヤを追加」を選択し、表示されるパネルの「ファイル名」で開くファイルを指定 > 「ジオメトリ定義」で「ポイント座標」を選択しX値・Y値に該当するフィールドを指定し「追加」をクリックする

#### ベクタデータを読み込み結合・表示を変更する（例）
1. 土地分類調査データをダウンロードする
      - 国土数値情報ダウンロードサービス：https://nlftp.mlit.go.jp/kokjo/inspect/landclassification/download.html
      - 東京都・埼玉県・千葉県を選択してダウンロード（他は任意）
2. 地形区分（ポリゴン）.shpをマップキャンパスにドロップ、またはメニュー「レイヤ」から「ベクタレイヤを追加」
      - .shpはシェープファイルの拡張子。.shxや.dbfが必須
      - DEMデータと異なり範囲を多角形（ポリゴン）で区切ったベクタデータ。範囲全体に一意の属性が与えられる
3. 都道府県別データを結合する
      - メニュー「ベクタ」から「データ管理ツール」>「ベクタレイヤを結合」
      - 結合後のデータはあらかじめ.gpkgデータベースとして保存設定するか、一時レイヤとして作成してから保存する
4. 表示の変更
      - レイヤ名をダブルクリックまたは右クリック→プロパティ→シンボロジ
      - 「カテゴリ値による定義」を選択、色分けしたい属性テーブルの項目を値(Value)に設定
      - カラーランプを選択（任意）→「分類」をクリック

#### グリッドを作成する
1. メニュー「ベクタ」から「調査ツール」 >「グリッド」を選択
2. グリッドタイプ：ポイント、ライン、ポリゴン（長方形・菱形・六角形）
3. グリッドの範囲：座標で直接指定 or 「現在のキャンパス領域に設定」ボタンで表示範囲を指定
4. 水平方向／垂直方向の間隔：数値で指定。CRSが平面直角座標ならメートル、地理座標なら「度」
![Grid](https://github.com/kotdijian/KoukogakuKenkyu9/blob/main/Figures/GridSample.png)   

---
### 4. ベクタデータの編集操作

#### ベクタデータ（ポイントデータを含む）をフィルタリングする
1. フィルタリングするレイヤを右クリック > フィルタ > 「クエリビルダ」が開く（SQLベースのクエリビルダ）
2. 「フィールド」欄に属性テーブルのフィールド一覧が表示されるので、フィルタリングしたいフィールドを選択する
3. 「値」欄の下部の「すべて」をクリックすると選択したフィールドに含まれる全ての値が表示される
4. 「フィールド」欄で選択したフィールドをダブルクリックすると下部の「プロバイダ特有のクエリ式」欄にフィールド名が転記される
5. 「演算子」欄からフィルタリング条件式を選択する
   - 等号・不等号："＝" 等しい、"<" より大きい、">" より小さい、"<=" 以上、">=" 以下
   - 論理式："!＝" 以外、"AND" どちらにも一致（論理積）、"OR" どちらかに一致（論理和）、"NOT" ではない（否定）、 
   - 曖昧検索："LIKE"、"!LIKE"、ワイルドカード"%"と一緒に使うことが多い（"SiteName" LIKE '%遺跡'＝SiteNameに~遺跡を含む）
   - 複数条件："IN"、"NOT IN"（"Name" = 'A' OR "Name" = 'B'は"Name" IN ('A', 'B')と等しい）
6. 「値」欄からフィルタリング条件値を選択してダブルクリックするか、または「プロバイダ特有のクエリ式」欄に直接入力する
7. フィルタがかかった状態で、レイヤを右クリック > 「エクスポート」 > 「新規ファイルに地物を保存」でファイル名とファイル形式、保存先を指定するとフィルタされたデータだけを書き出すことができる
8. フィルタの解除：フィルタがかかっているレイヤは、レイヤ名の右にフィルタ（漏斗）のマークが表示されている。フィルタマークをクリック、またはレイヤ名を右クリック > 「フィルタ」で「クエリビルダ」を開き、下部の「クリア」をクリックするとフィルタが解除される（条件式も消える）
9. フィルタ（条件式）の保存：「クエリビルダ」を開き、下部の「保存」をクリックすると条件式を保存できる。繰り返し使用するときに便利

#### 細かく分割されているベクタデータの統合
1. 「ベクタ」メニューの「空間演算ツール」から「融合（dissolve)」を選択 >「ベクタジオメトリ-融合（dissolve）」が開く
2. 「入力レイヤ」で操作するレイヤを選択
3. 「基準となる属性（複数可）」で統合する基準となるフィールドを選ぶ
4. 「融合ポリゴンの出力」でファイル名と形式を指定するか、または一時レイヤを作成する
5. 「ベクタジオメトリ」ウィンドウ下部の「詳細パラメータ」の下向き三角をクリック > 「アルゴリズム設定」を選択 > 「無効地物フィルタ」で「不正なジオメトリの地物を無視」を選択
6. 「ベクタジオメトリ」ウィンドウ右下部の「実行」をクリック
例）行政界データ（区市町村単位）を融合して都道府県全域のデータにする

#### その他の「空間演算ツール」
- バッファ：入力レイヤの地物（ポイントやライン、ポリゴン）の周囲を指定した距離で取り囲むバッファ（余地）を作成する
- 切り抜く：入力レイヤの地物の形状で、オーバーレイレイヤの地物の形状を切り抜く（重なる範囲だけが取り出される）
  （例：埼玉県地形分類ポリゴンを行政界（川越市でフィルタ）で切り抜く）
![Clip](https://github.com/kotdijian/KoukogakuKenkyu9/blob/main/Figures/VectorClip.png)
- 突包：入力レイヤの地物の最外周をつなぐラインポリゴンを作成する。ポイントの場合、最外周に位置するポイントをつなぐ
- 差分：入力レイヤの地物の形状で、オーバーレイレイヤの地物の形状を切り抜く（重ならない範囲が取り出される）
  （例：埼玉県地形分類ポリゴンと行政界（川越市でフィルタ）の差分）
  ![Defference](https://github.com/kotdijian/KoukogakuKenkyu9/blob/main/Figures/VectoreDef.png)
- 交差：入力レイヤの地物の形状で、オーバーレイレイヤの地物の形状を切り抜き、2つのレイヤの属性を保持した新しい地物を作成する（重なる範囲）
- 対称差：入力レイヤとオーバーレイレイヤの地物の重ならない部分が取り出される。それぞれのレイヤの属性が保持される
- 和集合：入力レイヤとオーバーレイやの地物がそれぞれ、重なる部分と重ならない部分に分割される
- 公式マニュアル：https://docs.qgis.org/3.40/ja/docs/user_manual/processing_algs/qgis/vectoroverlay.html

---
### 5.ポイントデータの解析1

#### ジオメトリツール： 「ベクター」 > 「ジオメトリツール」
- 重心：入力レイヤの地物の座標重心をポイントとして出力する。複数の地物がある場合はそれぞれの重心を出力する（例：行政界データを選択すると各区市町村の重心が出力される）
  （例：埼玉県行政界の市町村ポリゴンの重心）
  ![VectorCentroid](https://github.com/kotdijian/KoukogakuKenkyu9/blob/main/Figures/VectorCentroid.png)
- ドロネー三角形分割（三角形網）：ポイントデータから不規則三角形網を作成する。三角形は各ポイントを結ぶ相互に交差しない線分で構成される。空間分割やネットワークの可視化
  （例：埼玉県行政界の市町村ポリゴンの重心にもとづくドロネー三角形網）
  ![PointDelauney](https://github.com/kotdijian/KoukogakuKenkyu9/blob/main/Figures/PointDelauney.png)
- Voronoi Polygons（ボロノイ分割）：各ポイントから等距離の線分で空間を分割する
  （例：埼玉県行政界の市町村ポリゴンの重心にもとづくボロノイ分割）
  ![PointBoronoi](https://github.com/kotdijian/KoukogakuKenkyu9/blob/main/Figures/PointVoronoi.png)
  **ドロネー三角形はポイントを頂点とする <> ボロノイ分割はポイントを中心とする**
  
- **応用編** 埼玉県行政界の市町村ポリゴンの重心にもとづくボロノイ分割 > Buffer region=50 > 埼玉県行政界（県界）ポリゴンで切り抜き
  ![VoronoiBufferClip](https://github.com/kotdijian/KoukogakuKenkyu9/blob/main/Figures/VoronoiBufferClip.png)

#### 解析ツール：「ベクター」 > 「解析ツール」
- ポリゴン内の点の数：「ポリゴン」で指定したレイヤのポリゴン範囲内に含まれる「ポイント」で指定したレイヤのポイントの数をカウントして、ポリゴンの属性に追加する
- （例：埼玉県地形分類ポリゴンで遺跡数を集計する）
  ![PointCount](https://github.com/kotdijian/KoukogakuKenkyu9/blob/main/Figures/PointCount.png)

#### 応用編
1. 埼玉県中世遺跡のCSVをポイントレイヤとして読み込み
2. レイヤを複製 > 'SiteType' LIKE "%城%" でフィルタリング（城跡・城館が抽出される）
3. 城・城館ポイントでボロノイ分割
  ![PointCount](https://github.com/kotdijian/KoukogakuKenkyu9/blob/main/Figures/VoronoiPoint.png)
5. 分割されたエリアに含まれるポイント数をカウント
  ![PointCount](https://github.com/kotdijian/KoukogakuKenkyu9/blob/main/Figures/VoronoiPointNum.png) 

---
### 6.ポイントデータの解析2
- ヒートマップ：レイヤの「シンボロジ」>ヒートマップを選択、半径は画面表示上のサイズなのでズームにより密度分布の計算範囲が変わる
- ポイントにラスタの属性を付加：例）DEMの標高をポイントデータに追加する
   1.

---
### 7.ポイントとポリゴンの作成と編集
1. メニュー「レイヤ」 > 「新規スクラッチレイヤを作成」
2. ジオメトリタイプを選択（ポイントまたはポリゴン）
3. 

---
### 8. ジオリファレンシング
- ジオリファレンシング＝画像・スキャンした図面などに座標を与え、必要に応じて歪み補正（幾何補正）を行うこと
