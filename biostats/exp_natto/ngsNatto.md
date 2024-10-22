# 遺伝子発現解析（納豆菌編）のためのNGS解析

## このページは...
- Python (Google Colab.) やExcelで遺伝子発現解析をする方法
  - [Python（on Google Colab）で遺伝子発現解析（納豆菌編）](./expNattoByPythonOnColab.ipynb)：Google Colabバージョン。（ipynbファイル）
  - [Excel でなぞる遺伝子発現解析（納豆菌編）](./expNattoByExcel.md)：Excel版
- このデータはGEOの元データで配布されている、すでに発現データにされたものを加工して用いている
- このページは別に登録されたNGSデータ（readデータ）から発現データまでをNGS解析としてなぞったときにどうなるかを解説している
- そのため、このページで得られた結果の発現量データと、GEOで配布された発現量データが同じである保証はない。

## そもそもNGSとは
- [NGS解析解説](../../ngs/README.md)

- データの検索
  - DDBJ Search
  - Sequence Read Archive と BioProject
  - データ構造について
  - DDBJ Searchをいくつかの切り口で検索してみる
    - NBRC
    - 生物種
- 今回 用いるデータ
  - Transcriptome analysis of Bacillus subtilis NBRC 16449 grown on surface of boiled soybeans under the similar condition to production of Japanese traditional soybean-fermented food "natto"
  - https://ddbj.nig.ac.jp/search/entry/bioproject/PRJNA431298
- データの見方：データ構造にしたがって確認する
  - この場合、3実験している：3つのexperiment/sampleペア
  - 何が違うのか（〜を見る、とあるが、実際はすべて確認してどこが違うかを確認する。概要はBioProjectやsra-studyでのタイトルや実験のdescription（説明）から読み解ける）
    - サンプルそのものが違う場合：野生株とノックアウト株、 → サンプル情報（BioSample）を見る
    - 同じサンプルに異なる処理をした場合：無処理と薬剤処理 → 実験情報（sra-experiment）を見る
    - この場合は、experimentを見ると、同じ納豆菌を液体培地、寒天培地、茹で大豆の表面の3つの条件で培養しているのがわかる。
- 実験データのダウンロード
  - fastqファイル：シーケンスとそのクオリティ（品質）について記載されたファイル（DDBJからは取得できる）
  - sraファイル：fastqファイルと実験情報をまとめて圧縮したファイル（NCBIはこの形式のみ配布）
  - experiment/sampleに紐づいたrunのページからダウンロードできる
  - 自分でダウンロードしなくてもプログラムでIDを指定することでダウンロードから処理してくれる
- ゲノム、cDNAデータのダウンロード
  - Ensemblから
    - 今回は微生物なのでページ末尾のEnsembl Bacteriaへ。Species listを表示して生物種を検索。Bacillus subtilis、nattoなど。
    - cDNAやゲノムをダウンロード
  - NCBI Datasets（旧：NCBI Genome）から
    - 生物種名を入力。スペルをミスったりするので、NCBI Taxonomyで検索してGenomeに飛んでもいい。が、いろいろ出てくるので、どれを選んでいいのかわからないところはある。CompletenessやContig数で判断したりする。
  - 専門のデータベース


