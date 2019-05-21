# NGS解析：FASTQファイルからtranscriptまで

## この前のFASTQファイルからtranscriptまで

[read2transcript.md][6fa7bc54]

  [6fa7bc54]: ./read2transcript.md "FASTQファイルからtranscriptまで"

# NGS解析：transcriptの機能アノテーション

## 概要
- ドメイン解析：HMMER
- BLAST・その1：配列セットから自分の興味あるサブセットを作る
- BLAST・その2：既知の遺伝子との類似性検索

## HMMER

### indexをはっておく

```
$ hmmpress Sod_Cu.hmm
Working...    done.
Pressed and indexed 1 HMMs (1 names and 1 accessions).
Models pressed into binary file:   Sod_Cu.hmm.h3m
SSI index for binary model file:   Sod_Cu.hmm.h3i
Profiles (MSV part) pressed into:  Sod_Cu.hmm.h3f
Profiles (remainder) pressed into: Sod_Cu.hmm.h3p
```

### ドメインを持つものをピックアップ

```
$ hmmsearch --domtblout P-1.SOD_Cu.out SOD_Cu.hmm px.proteins.fasta.gz --cpu 12 | tee P-1.Cu_SOD.log
```

- --domtblout をつけることによって、ドメインごとにテーブル形式のファイルがつくられる
  - テーブル形式だけれどもタブ区切りではないようだ（メンドイ）
- | tee の部分は、> でよいのだが、ログが表示されるのでこうしている。
- 結果
```
#                                                                               
# target name               accession   tlen query name           accession   ql
#       ------------------- ---------- ----- -------------------- ---------- ---
TRINITY_DN19683_c0_g1_i1.p1 -            154 Sod_Cu               PF00080.20   1
TRINITY_DN106_c0_g1_i1.p1   -            171 Sod_Cu               PF00080.20   1
TRINITY_DN106_c0_g1_i4.p1   -            191 Sod_Cu               PF00080.20   1
TRINITY_DN106_c0_g1_i2.p1   -            232 Sod_Cu               PF00080.20   1
TRINITY_DN289_c0_g1_i3.p1   -           1133 Sod_Cu               PF00080.20   1
...
TRINITY_DN289_c0_g1_i1.p1   -           1133 Sod_Cu               PF00080.20   1
TRINITY_DN4859_c0_g1_i1.p1  -            187 Sod_Cu               PF00080.20   1
#
# Program:         hmmsearch
# Version:         3.2.1 (June 2018)
# Pipeline mode:   SEARCH
# Query file:      /Users/nakazato/bio/data/hmmer/Sod_Cu.hmm
# Target file:     ../00_rslt_trinity/Trinity.fasta.transdecoder_dir/longest_orf
# Option settings: hmmsearch --domtblout Trinity.SOD_Cu.out --cpu 12 /Users/naka
# Current dir:     /Users/nakazato/bio/work/ngsbon2/12_hmmer
# Date:            Thu Feb 14 15:59:47 2019
# [ok]
```
ここから、SOD_CuドメインをもつtranscriptのID（例：TRINITY_DN19683_c0_g1_i1.p1）だけを抽出するには以下のワンライナーを実行する。
```
$ perl -F"\s+" -lane 'print $F[0] if $_ !~ /^\#/' longest_orfs.SOD_Cu.out > longest_orfs.SOD_Cu.ids
$ cat longest_orfs.SOD_Cu.ids
TRINITY_DN19683_c0_g1_i1.p1
TRINITY_DN106_c0_g1_i1.p1
TRINITY_DN106_c0_g1_i4.p1
TRINITY_DN106_c0_g1_i2.p1
TRINITY_DN289_c0_g1_i3.p1
TRINITY_DN289_c0_g1_i3.p1
(以下略)
```

- if $_ !~ /^\#/：もしも各行の先頭が # で始まらないならば
- -F"\s+"：空白で各行を区切ったもののうち
- print $F[0]：（0からカウントして）0番目を出力せよ


## BLAST

まずは本来の使い方でない、配列のサブセットを作成する方法

Trinityや*-base（公共DB中のtranscriptセット）をBLAST DB化し、HMMERで作成した「あるドメインをもつtranscriptの配列サブセット」を作る（そして、そのあとで、それらを公共データベースに対してBLASTし、遺伝子名をつける）

```
$ makeblastdb -in longest_orfs.pep -out trinity_rslt -dbtype prot -hash_index -parse_seqids
```
- -in: BLASTをかける対象となる配列セット（普通はFASTA形式）のファイル
- -out: BLASTをかける際の対象データベース名
- −dbtype: 塩基配列の場合はnucl、アミノ酸配列の場合はprot
- -hash_index: 高速化のためにindexをつける
- -parse_seqids: これをつけると配列名で検索できるようになる



（あとで適当な位置に移動）
BLASTのデータベースを利用して配列のサブセットをとってくるやり方
```
$ blastdbcmd -db pbase_pxut -entry PxuthusGene0000002\|PxuthusGene0000002.mrna1
>PxuthusGene0000002|PxuthusGene0000002.mrna1
MKIRIRISFYSRRINRSLSINPYLLKIQFFTIFFGVNLTFFPQHFLGLAGIPRRYSDYPDNFIS
```
- ...複数の場合はIDをファイルに書き出しておいて
```
... -entry_batch filename
```

blastpでの検索
```
$ blastp -query … -db … -num_threads 12 -max_target_seqs 1 -outfmt 6 > blast.result.tab
```




## 結果の比較など

- 発現値とドメイン（HMMERの結果）と遺伝子名（BLASTの結果）とがっちゃんこする
- joinはsortしてから
