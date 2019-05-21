# NGS解析：FASTQファイルからtranscriptまで

## 概要
- いわゆるRNA-Seq解析
- 世の中の研究の進み具合によって3つのやり方がある
  - ゲノムにマッピング
    - いわゆるモデル生物の場合
    - ただこういう場合は、すでにtranscriptのセットがわかっていたりするので、後述のtranscriptセットにマッピングの方が速い
    - HISAT2+stringtie
  - transcriptセットにマッピング
    - 以前はなかった新しい方法
    - salmon とか kallisto とか
  - de novo assemble
    - ゲノムもtranscriptセットもないような場合
    - いわゆる「下絵なしジグソーパズル」
    - Trinity


## Trinity

### インストール

### FASTQからtranscriptへ

```
Trinity --seqType fq --left P-1_1.fastq.gz --right P-1_2.fastq.gz --max_memory 16G --CPU 12 --output trinity_out
```

- --output で指定する出力先には、安全のためにtrinityの文字列を含まねばならない（というようにプログラムから怒られる）
  - 特に何もしないと Trinity.fasta というファイルができる
- 念のための注意点
  - 数日から1週間かかる計算のため、計算専用にマシンを使う方が早く終わる。その際は screen とか byobu を使ってログアウトしても計算が続くようにしておく
  - 出力先のディレクトリはつどつど名前を変えるとかプロジェクトごとにディレクトリを作ってそこで作業する。前のがあるのに計算すると（怒ってくれるかもしれないが）静かにせっかく時間をかけてやった前の（時には他の人の）データを消してしまうかもしれない。



### 発現定量

### アミノ酸配列への変換（この後の機能解析に向けて）

```
TransDecoder.LongOrfs -t Trinity.fasta -m 30
```

- -t 対象ファイル名。gzip 圧縮されていても通る。
- -m アミノ酸配列の最小値。初期値は100。これを下回ると出力されない
- -O 出力先（Ver.5.5.0以降）。初期値は 配列ファイル名.transdecoder_dir/ 。この中に longest_orfs.pep ができる

## salmon
### 概要
- https://combine-lab.github.io/salmon/

### インストール
```
$ conda install salmon
```
もしくは
```
$ brew install salmon
```

### reference の配列を取ってくる
- Ensembl から
- XXXbaseから

### referenceに対してindexをつくる
- indexをつくる

```
$ salmon index -t ~/bio/data/px/px.transcript.fasta.gz -i px_idx
$ salmon index -t [CDSセットのファイル名] -i [インデックス名]
```

### referenceに対してmapping＋定量する

```
$ salmon quant -i px_idx/ -l A -1 P-1_1.fastq.gz -2 P-1_2.fastq.gz -p 8 -o output/ --validateMappings
```
- -l A ：おまじない（ファイルの中身を自動判別だったかな）
- --validateMappings：おまじない（よっぽどでなければつけておけ、と怒られる）



計算結果として、出力先として指定したoutputディレクトリ内にquant.sfファイルができている。

```
Name    Length  EffectiveLength TPM     NumReads
KPJ20932.1      711     559.556 0.044363        1.000
KPJ21050.1      189     50.772  26.890816       55.000
KPJ21177.1      723     571.553 0.086862        2.000
KPJ21437.1      273     123.872 0.000000        0.000
KPJ21572.1      288     138.239 0.000000        0.000
...
```
ログを見てマップ率くらいは確認しておく
```
$ less output/logs/salmon_quant.log
...
[2019-02-01 14:29:44.644] [jointLog] [info] Counted 47,109,324 total reads in the equivalence classes
[2019-02-01 14:29:44.651] [jointLog] [info] Mapping rate = 86.3888%

[2019-02-01 14:29:44.651] [jointLog] [info] finished quantifyLibrary()
...
```

## この先の機能アノテーション

[function4NGS.md][e6dee8e8]

  [e6dee8e8]: ./function4NGS.md "NGS解析：transcriptの機能アノテーション"

- ドメイン解析：HMMER
- BLAST・その1：配列セットから自分の興味あるサブセットを作る
- BLAST・その2：既知の遺伝子との類似性検索
