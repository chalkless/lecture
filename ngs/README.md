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




### データのダウンロードと展開

* シングルエンドとペアエンド



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


