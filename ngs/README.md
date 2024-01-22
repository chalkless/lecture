# NGS解析

## NGSデータの入手
### 主要な流れ
* データベースでデータを検索
* データのアクセッション番号を控える
* サイトからデータをダウンロード後にfasterq-dumpで展開 or　データのアクセッション番号からfasterq-dumpで入手して展開

### fasterq-dump のインストール
* fastq-dumpやそれを高速化したfasterq-dumpはsra-toolkitとして配布されている
* Ubuntuの場合
```
$ sudo apt install sra-toolkit
$ fasterq-dump

Usage:
  fasterq-dump <path> [options]
  fasterq-dump <accession> [options]

Options:
  -F|--format                      format (special, fastq, default=fastq) 
  -o|--outfile                     output-file 
  -O|--outdir                      output-dir
  ...
（fasterq-dumpを実行して説明が表示されれば成功）
```
* Homebrewの場合
```
$ brew -v install sratoolkit
```

### NGSデータの配布形式
* NGSの（シーケンサーの出力する）生リード（raw read）のファイルの流通にはFASTQ形式のデータが使われる
```
@SRR6504026.1 MG00HS13:1487:H27KFBCX2:1:1101:1410:2249 length=101
CTCCGATATATAGGTCCCTCTGCCCCGCAGCGTTTCAATAATCCCCTCTCGCTCAAGCTCTTTATACGCTTTGCTGACAGTGTTCGGATTCGCAATAATGA
+SRR6504026.1 MG00HS13:1487:H27KFBCX2:1:1101:1410:2249 length=101
DDDDDIIIIHIIIHIIIIIGIIIIIIIIIIIIHHIIIIHIIIIIIHIIIIIIIIIHIGHIIHHIIIIIIIIIIIIIEHHIIIHIHHG=HHHEHHHIHIIHH
```

```
1行目：タイトル（@マークから始まる）
2行目：リードのシーケンス（塩基配列）
3行目：特に気にしなくていい（+マークから始まる）
4行目：リードのクオリティ
```

  * リードのシーケンスに対してクオリティがつくので、２行目と４行目が同じ長さになる
  * クオリティ：エラー率=10^(-Q/10)
    * Q=２0で1/100のエラー率で９９%のクオリティ。Q=30で1/1000のエラー率で９９．９％のクオリティ。
    * クオリティの値は2桁なので、それを文字に当てはめている。アルファベットだと32〜なので安心。
    * このあたりをビジュアル的に表す [fastqe](https://github.com/fastqe/fastqe) (fastq with emoji) というサービスもある。クオリティが悪いと渋い顔だったり火がついてたりする


* 下にあるようにファイルが数GBになるので、メタデータ（実験の説明データ）も含めて圧縮したSRA形式で配布もされる。最近はデータベースにはこちらの形式で置かれることが多い。


### データのダウンロードと展開

* シングルエンドとペアエンド

* fasterq-dump でファイルのダウンロードや展開（SRA形式→FASTQ形式）を行う
```
# ファイルのダウンロード
$ fasterq-dump SRR6504026
（データのダウンロードとSRA→FASTQの変換を一度に行う）

# ローカルにあるファイルの展開
$ fasterq-dump SRR6504026.sra
（データベースから自身でSRA形式ファイルをダウンロードして、それをfasterq-dumpの引数として指定）
（ダウンロードから行うと時間がかかったりするので、こちらの方が早いは早い）
```

### 実際のNGSデータを眺めてみる
```
$ ls -alFh        ←　hオプションをつけるとGB、MBのように人間が認識しやすいサイズで表示してくれる
合計 14G
drwxrwxr-x 2 chalkless chalkless 4.0K  1月 15 01:11 ./
drwxrwxr-x 3 chalkless chalkless 4.0K  1月 15 01:15 ../
-rw-rw-r-- 1 chalkless chalkless 1.9G 11月  4  2020 SRR6504026.sra         ←　展開前
-rw-rw-r-- 1 chalkless chalkless 5.9G  1月 15 01:11 SRR6504026_1.fastq     ←　展開後。サイズがかなり大きくなっている
-rw-rw-r-- 1 chalkless chalkless 5.9G  1月 15 01:11 SRR6504026_2.fastq     ←　ペアエンドなので_1 と _2　ができる。

$ wc -l SRR6504026_1.fastq 
71605624 SRR6504026_1.fastq      ←　7,160万行。実際のリード数はFASTQが4行で１セットなので 71605624/4 =　17901406 （1790万リード）
```

## クオリティチェック (optional)
* fastqcでチェックする
* この後の足切りプログラムをかける際に、クオリティチェックも同時にやってしまうソフトが多々あるので、ここでかける必要はない場合がある（が、ソフトはfastqcを使うのでインストールは必要）

### fastqcのインストール
```
# Homebrewの場合
$ brew -v install fastqc
```

```
$ fastqc
```



## 足切り

```
$ trimgalore
```


## その後の処理
* NGS実験を行った目的によって処理が変わっていく
  * RNA-Seq（発現解析）：ゲノムやcDNAにマッピングする
  * SNP解析：ゲノムに精度良くマッピングして１塩基単位での変異を検出
  * ゲノム解析：つないでいく。Long readのデータとShort readのデータを組み合わせるのがトレンド
  * メタゲノム：つないでいく。株レベルの差異は無視して（バーチャルな）ゲノムに組み上げていくMAG(Metagenome Assembled Genome)がトレンド



