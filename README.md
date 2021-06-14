# lecture

## メモ書き

ディレクトリ（フォルダ）の中身を見る
```
$ ls
```
場所を指定して中身を見る
```
$ ls /Volumes/TUAT4T/data/DS_2018
PM-A-FB_1.fastq.gz	PM-S-FB_1.fastq.gz	PX-M-FB_1.fastq.gz
PM-A-FB_2.fastq.gz	PM-S-FB_2.fastq.gz	PX-M-FB_2.fastq.gz
PM-A-MG_1.fastq.gz	PM-S-MG_1.fastq.gz	PX-M-MG_1.fastq.gz
PM-A-MG_2.fastq.gz	PM-S-MG_2.fastq.gz	PX-M-MG_2.fastq.gz
```

Macだと外付けディスクとかは /Volumes の下にある
```
$ ls /Volumes/
```
まで打ってTABを何回か打つとその下にぶらさがっているのが補完されて出る
```
$ ls -alF /Volumes/    ←ここでTABを何回か打つ
Macintosh HD/ TUAT4T/       TUATbackup/   nakazato/     timemachine/
$ ls -alF /Volumes/    ←で、どうしますか?　で待ちの状態
```

ファイルのコピー
```
$ cd Documents/ngs/
$ cp /Volumes/XXX/PM-A-FB_1.fasta.gz ./
$ cp /Volumes/XXX/PM-A-FB_2.fasta.gz ./
```
- ./ ：現在地

ちょっと進んだコピー（ワイルドカード）
```
$ cd Documents/ngs/
$ cp /Volumes/XXX/PM-A-MG_?.fasta.gz ./
$ cp /Volumes/XXX/PM-F-*_?.fasta.gz ./
（てかこの場合は下のように書けばよいのだが）
$ cp /Volumes/XXX/PM-F-*.fasta.gz ./
```
- ? ：任意の一文字。この場合は1と2
- \* ：任意の何文字か。この場合はFBとMG。（下の行だとFB_1とFB_2と...）


ファイルの中身を確認する
```
$ less ファイル名
```
- <：一番上へ
- \>：一番下へ

```
とりあえず一番上の方を見る
$ head ファイル名

一番下の方を見る
$ tail ファイル名
```

```
行数を確認
$ wc -l ファイル名
```

## Google Colaboratory
- 通称：Google Colab
- 参考サイト
- やり方
  - Google Colabでググる
  - 直接だと https://colab.research.google.com/
  - バックエンドをRにするのに https://colab.research.google.com/notebook#create=true&language=r にアクセスするのが一番手っ取り早い
  - ノートブックを新規作成（メニューのファイルからなど）
  - Untitled0.ipynb のようなファイルができる
  - ファイル名を変える
  - 一旦ファイルをファイル > ダウンロード > .ipynbをダウンロード
  - ファイルを書き換える
  ```
  ### 変更前
      "kernelspec": {
        "name": "python3",
	"display_name": "Python 3"
      },
      ...
  ```
  ```
  ### 変更後
      "kernelspec": {
        "name": "ir",
	"display_name": "R"
      },
      ...
  ```
  - Google Colabに戻って今のファイルをアップロード
  - ランタイム > ランタイムのタイプを変更でRになっていればOK
  - 画面左のフォルダマークからデータをアップロード(GSE18226.for_exercise.slim.tsv)
  - 




