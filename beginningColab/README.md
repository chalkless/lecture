# Google Colaboratory ことはじめ

## そもそもGoogle Colaboratoryとは
* Google Colaboratory は、Googleが提供するちょっとした解析環境です
* 「ちょっとした」というのは使えるのが主にPythonだけだからです。
* 他にもR言語もがんばれば使えます
* 何が便利なのか?
  * 自分のマシン、サーバーに環境構築しなくても解析ができる
  * ブラウザとネットワーク（とGoogleアカウント）があれば環境構築できる
  * コードとともにコメントも豊富に書くことができる
* ちょっと不便なところ
  * Pythonしか使えない
  * しばらくすると時間切れで途中でも接続が切られてしまう（ので長時間に及ぶ計算は有料アカウントが必要）
  * （上の項の続き）なので接続が切られた後は再びアップロードする必要がある（が、Google Driveと接続することはできる）

## とりあえず使ってみる
* https://colab.research.google.com/
* R言語を使いたい時はこちら：https://colab.research.google.com/notebook#create=true&language=r
  * とりあえず開いてみて、画面タイトルの次の行の「ランタイム」から「ランタイムのタイプを変更する」でランタイムのタイプをPython3からRに変更してもよい

## 基本中の基本
* pythonのコード（命令文）を書けるコードエリアと補足のコメント文章を書けるテキストエリアがあります
![コードエリアとテキストエリア](images/colab.preview.png)
* 再編集する時はボックスをダブルクリックします
* コードエリアの内容を実行するには右向き三角をクリックします
* 実行結果はコードエリアの下側に表示されます。
* もしエラーが出た時は右向き三角が赤くなり、エラーが結果として表示されます。ので、それを見て中身を修正します。（コードがおかしいか、読み込むデータがおかしいか）
* 画面上部左側と各エリアの境目にマウスオーバーするとボックスを追加するボタンがあります
![コードエリアとテキストエリア](images/colab.addbox.png)


## 別ページに書いた情報
* [Google Colaboratoryでのファイルのアップロード](./ColabUploadFile.md)
* [はじめてPythonで統計解析をしてみる（Google Colab編）](./startPython_GColab.ipynb)
* [はじめてRを使ってみる：Google Colab編](./startR_GColab.ipynb)
* [Google Colab でバイオインフォマティクス（導入編）](../biopython/arrangeNuc.ipynb)
* [納豆菌の培地の違いによる遺伝子発現比較](../biostats/exp_natto)



