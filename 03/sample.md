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
*　"13Tokyo"フォルダには、[東京都遺跡地図情報インターネット提供サービス](https://tokyo-iseki.metro.tokyo.lg.jp/)から作成した東京都遺跡一覧データがあります（島嶼部除く）
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

###### 3
# GitHubリポジトリの作成
* [公式ドキュメント](https://docs.github.com/ja/repositories/creating-and-managing-repositories/creating-a-new-repository)
* "test"または任意の名前で新しいリポジトリを作成してください
* リポジトリの名称は基本的に半角英数字のみ
* 公開リポジトリとして運用する場合は個人情報・機微情報を掲載しないこと

---

###### 4
# GitHub Desktopのインストール
* [公式ドキュメント](https://docs.github.com/ja/desktop/installing-and-authenticating-to-github-desktop/installing-github-desktop)
* [GitHub Desktopの使い方](https://qiita.com/yasu_qita/items/3a24322f0ebdd443ba7e)

