# Excelで可視化する新型コロナデータ
- 新型コロナのデータを使ってExcelで統計解析の基礎や可視化をやってみようという試み

## データを入手してExcelで開く
- 元データ
  - （内閣官房）新型コロナウイルス感染症対策 https://corona.go.jp/dashboard/
  - ここにある全国の感染者数データ（JSON形式）：https://opendata.corona.go.jp/api/Covid19JapanAll
  - [参考] 最新の都道府県別累積陽性者数：https://data.corona.go.jp/converted-json/covid19japan-all.json
- [参考] データの加工
  - 元のファイルはJSON形式というのですが、Excelだと処理しにくいのでCSVに形式変更している
```
$ cat Covid19JapanAll.json | jq -r '.itemList[]|[.date, .name_jp, .npatients]|@csv'> Covid19JapanAll.csv 
```
  - 変更後のファイル：


