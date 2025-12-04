# 生物統計学

もともと講義で話す用。講義に出ない（多学科の）人も見たいそうだから、せっかくなので一般公開しておく。

## 納豆菌の培地の違いによる遺伝子発現比較
### （optional） 生物統計部分で処理するデータをNGS解析で作成する
- [遺伝子発現解析（納豆菌編）のためのNGS解析](https://github.com/chalkless/lecture/blob/master/biostats/exp_natto/ngsNatto.md)：以下の納豆菌の発現データ解析は論文の著者が途中まで解析したものを用いているが、それを最初のNGSリードから解析した時の方法

### 納豆菌の遺伝子発現解析：発現データ → 発現の増えた/減った遺伝子セットの作成 → 遺伝子の発現変動のあった遺伝子群の機能解析
- [Excel でなぞる遺伝子発現解析（納豆菌編）](exp_natto/expNattoByExcel.md)：Excel版
- [Python（on Google Colab）で遺伝子発現解析（納豆菌編）](exp_natto/expNattoByPythonOnColab.ipynb)：Google Colabでやってみる用。（ipynbファイル）


## シロイヌナズナの分化/未分化細胞での遺伝子発現比較
- [Excelでなぞる遺伝子発現解析](exp/expByExcel.md)：普通はプログラミングかR言語でするような遺伝子発現解析を、Excelで試しに（できる部分だけ）やってみようという試み
- [R言語で遺伝子発現解析](exp/expByR.Rmd)：マイクロアレイデータを例にRで遺伝子発現解析をしてみた（内容は上のExcelでなぞる遺伝子発現解析と同じ）。RStudioで開く用（Rmarkdownで記述）
- [R言語で遺伝子発現解析(Google Colab編)](exp/expByROnGColab.ipynb)：上のR言語で遺伝子発現解析と中身は同様。RStudioでなくGoogle Colaboratory (Google Colab)で開く用。ipynbファイル。（作成中）


## はじめて統計処理をする人向け
- [Google Colab](../beginningColab/)
- [R](./beginningR/)

## 他
- [Excelで可視化する新型コロナデータ](covid19/Covid19ByExcel.md)：Covid-19の患者数の推移をExcelで取り込んである都道府県の患者数の推移を折れ線グラフにしてみたり、ある日の患者数を都道府県別に棒グラフや円グラフ、日本地図にマップする
- Rで可視化する新型コロナデータ：上のR版。作成中

- [はじめてRをさわってみる](learningR.Rmd)：R Markdownを使って、クリックするだけでRの動きを確認できるようにしてみた（RStudioで開いてください）
- R言語で...（予定）


