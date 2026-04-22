name: white
layout: true
class: center, middle, white
---
# 整然データ・データベース・データリポジトリ

## 考古学研究9
#### 第2回目(2025/4/23)

[授業ページトップに戻る](https://kotdijian.github.io/KoukogakuKenkyu9/)
---
layout: false

###### 1
# GitHubについて



* GitHubは「バージョン管理システム」Gitを用いたウェブリポジトリです。
* [GitHub: Wikipedia](https://ja.wikipedia.org/wiki/GitHub)
* おもにプログラムの共同開発のプラットフォームとしえ使用されますが、データサイエンス分野ではデータの公開・共有にも使用されます。
* GitHub Inc.が開発し、現在はMicrosoftの傘下にあります。
* バージョン管理：異なる作業結果を照合し差分を提示、分岐や統合を管理します。

---
###### 2
# GitHubリポジトリを見てみよう
* [本授業の公開リポジトリ](https://github.com/kotdijian/KoukogakuKenkyu9)
* [リポジトリをWebページにできます](https://kotdijian.github.io/KoukogakuKenkyu9/)

---
###### 3
# GitHubアカウントの取得

* [公式ドキュメント](https://docs.github.com/ja/get-started/start-your-journey/creating-an-account-on-github)
* 2要素認証を設定しましょう

---
###### 4
# GitHubリポジトリの作成
* [公式ドキュメント](https://docs.github.com/ja/repositories/creating-and-managing-repositories/creating-a-new-repository)
* "test"または任意の名前で新しいリポジトリを作成してください
* リポジトリの名称は基本的に半角英数字のみ
* 公開リポジトリとして運用する場合は個人情報・機微情報を掲載しないこと

---
###### 5
# GitHub Desktopのインストール
* GitHub Desktopはボタンと簡単な入力（GUI）でGitHubを操作することができるデスクトップアプリです。
* GitHub Desktopを使うと、ローカルリポジトリ＝ウェブ上ではなく手元のPCに作成されたリポジトリを常に同じ状況に保つことができます。
* [公式ドキュメント](https://docs.github.com/ja/desktop/installing-and-authenticating-to-github-desktop/installing-github-desktop)
* [GitHub Desktopの使い方](https://qiita.com/yasu_qita/items/3a24322f0ebdd443ba7e)

---
###### 6
# GitHubリポジトリからファイルを取得する
1. 該当するリポジトリを開きます
2. ファイルを選択します
3. Preview画面の右上のダウンロードボタンをクリックする。フォルダ、ファイル名を指定して実行する。
[![GithubButton](https://raw.github.com/kotdijian/KoukogakuKenkyu9/master/02/figs/GithubButton.png)](https://raw.github.com/kotdijian/KoukogakuKenkyu9/master/02/figs/GithubButton.png)  

---
###### 7
# GitHub Desktopの使い方
1. 基本操作
	* Fetch: リモート(Origin)とローカルを同期する
	* Pull: リモート上の変更をローカルに反映させる
	* Push: ローカル上の変更をリモートに反映させる

2. クローンの作成
	* GitHub Desktopの**File** > **Clone Repository** を選択
	* GitHub.comの**your repository** から作成済みのリポジトリを選択する

3. ローカルリポジトリの確認
	* ローカルリポジトリが作成されたフォルダを開く

4. 変更とプッシュ
	* リポジトリ内のファイルを変更、または新しいファイルを作成
	* 左側 **Changes** パネル下方の**Commit ## file to main** をクリック
	* 上方の **Push Origin** をクリック
	* リモートリポジトリ側で変更を確認（必要に応じてページを再読み込み）

---
###### 8
# 整然データ
1. 基本原則
	* データを処理するのは機械（コンピューター・ソフトウェア）です
	* 機械が読み取れる型式・内容・構造にする必要があります
	
2. 自然言語と機械語
	* 私たちが情報の伝達と理解に使用するのは**自然言語**です
	* **自然言語**はそれぞれ意味をもつ単語と、その組み合わせを規定する文法からなります
	* 機械が情報の伝達と処理に使用するのは**機械語**です
	* **機械語**は0と1の2進数の符号で構成されます
	
3. プログラミング言語
	* 私たちは**機械語**を直接読み書きすることができません（非常に困難です）
	* **機械語**は一種類に統一されておらずコンピューターのプロセッサー(CPU)ごとに異なります
	* 人間にもわかりやすい形式で機械語に変換可能な**プログラミング言語**が用意されています
	
---
###### 9
# 整然データ（続）
4. 人間可読 (Human readable)、機械可読 (Machine readable)
	* 一般的な文書や表は人間が読むことに適したかたちになっていますが機械には適していません
	* 機械に読み込み・処理させるためにはプログラミング言語に適した形式にする必要があります
	* そのようなデータを**整然データ(tidy data)**と呼びます
#### [整然データとは何か](https://id.fnshr.info/2017/01/09/tidy-data-intro/#toc-heading-0)
	
---
###### 10
# 整然データの基本
* ひとつながりのデータは1行におさめられている
* 各行の中の項目の順序は定められている
* 各行には他と区別されるインデックス(UID)が付される
* 各行の関係は並び順またはインデックスによる昇順

### 重要!!
**クロス集計表は整然データではない!**
**集計は原データではなく、計算(集計)結果であり出力です**

---
###### 11
# データの型
### 数値型
* 整数型、固定小数点型、浮動小数点型（単精度・倍精度）
**有効桁数に注意**
### 文字型
### その他の特定データ型
**日付型**