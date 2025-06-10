# R ことはじめ
## そもそもRとは
- 統計用のソフトです
- R自体はコマンド（命令文。通称：呪文）を打ち込んで使います
  - インストールのしかたによりますが、Rのウインドウが出る場合もあるし、Macの場合などはターミナル上で動く場合もあります
- コマンドだけだとそっけないしコメントも本気で書けないので、より使いやすくする方法があります。それがRStudioを導入してR Markdownで書くものです
  - RStudioを使うと、同じ画面でグラフを描いたりファイルを選択したりなどより統合的な環境が得られます
  - R markdownで記載するとコメントが書けたり、一連の操作をファイルとして保存することができます
 
## 導入編
- 2025年版

- 前は rstudio.com にアクセスしていたのだが、いつのまにか変わっていて https://posit.co/download/rstudio-desktop/#download からダウンロードするようになった（Posit softwareが面倒を見ることになった）

### Rのインストール
- ここにRのインストールサイトへのリンクもあるのでここからアクセスしてしまう。
  - https://cran.rstudio.com/ にアクセスする（上記のサイトからリンクがある）
  - 使いたい環境（Windows/Linux/Mac）を選んでファイルをダウンロードしインストールする

### RStudioのインストール
- https://posit.co/download/rstudio-desktop/#download のページに戻ってくる
- RStudioのインストールのボタンを押してダウンロードする

### 補足
- Homebrew や Miniconda からRStudioを入れることもできる
```
# Homebrewの場合
$ brew install rstudio

# プログラム自体はアプリケーションフォルダに入るので、デスクトップアプリの要領で立ち上げる
```
```
# Minicondaの場合
$ conda install rstudio
```

## 導入しない編
### Google Colaboratory
- Google Colab自体はPython用だが、Rも動かすことができる（Pythonコードとの混在はできない、と思う）
- https://colab.research.google.com/notebook#create=true&language=r から開く
- もしくは、Google Colabを開いて、画面タイトルの次の行の「ランタイム」から「ランタイムのタイプを変更する」でランタイムのタイプをPython3からRに変更してもよい

### Posit Cloud
- RStudioを提供するposit softwareがクラウド環境を提供していて、ここでRStudioを動かせる
- 昔はRStudio.cloudだったのだが、こちらも名前など変わった模様
- https://posit.cloud/ にアクセスする。
  - フリーのプランがある。がつがつ使うには有料。Academic discountもある

## 実践編
- [はじめてRをさわってみる](../learningR.Rmd)：R Markdownを使って、クリックするだけでRの動きを確認できるようにしてみた（RStudioで開いてください）
- [はじめてRを使ってみる：Google Colab編](../startR_GColab.ipynb)
- [生物統計](../)：ここにもいくつかRで書いたものがあるので参考のこと
