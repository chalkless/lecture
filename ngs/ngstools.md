# NGS関連ツール
## fastq-dump/fasterq-dump
- NCBI/EBI/DDBJからリードデータをダウンロードするツール＋ダウンロードしたsra形式のファイルをFASTQ形式に変換するツール
- https://github.com/ncbi/sra-tools/wiki
- 元々はfastq-dumpだったが（多分、並列化して）より早く動くようにしたのがfasterq-dump
### インストール
- aptの場合 （Ubuntuなど）
```
sudo apt install sra-toolkit
```
- condaの場合
```
conda install sra-tools
```
- Homebrewの場合
```
brew -v install sratoolkit
```
- バイナリ、ソースからなど（オフィシャルサイトのGitHubから入手）：https://github.com/ncbi/sra-tools/wiki/01.-Downloading-SRA-Toolkit
### 使い方
- データのダウンロード ＋ sra→FASTQ形式に変換
```
fasterq-dump SRR6504026
```
- ダウンロード済のsraファイルをFASTQ形式に変換
```
fasterq-dump SRR6504026.sra
```
  - NCBIにダウンロードしに行くので、あらかじめDDBJからsra形式でダウンロードして形式変換したほうが早い

## fastqc
- リードデータのクオリティチェックをしてくれるツール
- https://www.bioinformatics.babraham.ac.uk/projects/fastqc/
- 後述するトリミング（足切り）ツールである`trim-galore`を用いるとクオリティチェックもしてくれるので（その後、自動的にトリミングまで行う）、単独で用いなくてもよい
- `trim-galore`をインストールすると自動でfastqcもインストールされる
### インストール
- aptの場合 （Ubuntuなど）
```
sudo apt install fastqc
```
- condaの場合
```
conda install fastqc
```
- Homebrewの場合
```
brew -v install fastqc
```
- バイナリ、ソースコードなど：https://www.bioinformatics.babraham.ac.uk/projects/download.html#fastqc
### 使い方
```
fastqc --nogroup -o DRR1234567.fastq
```
- `--nogroup`をつけるとより細かく結果を出してくれる

## trim-galore
- NGSリードをトリミングするツール
- https://github.com/FelixKrueger/TrimGalore
- 中身はクオリティチェックをする`fastqc`とトリミングする`cutadapt`をまとめて行っているだけ
### インストール
- aptの場合 （Ubuntuなど）
```
sudo apt install trim-galore
```
- condaの場合
```
conda install trim-galore
```
- ソースコード：https://github.com/FelixKrueger/TrimGalore
### 使い方
```
trim_galore --paired --illumina --fastqc -o trimmed/ DRR1234567.R1.fastq DRR1234567.R2.fastq
```
- `--paired`：ペアエンド
- `--illumina`：Illuminaのデータを表す（シーケンサーによりアダプター配列が決まっているのでそれを除去するため）
- `--fastqc`：fastqcによりクオリティチェックもする
- `-o directory`：結果を出力するディレクトリの指定
- fastq形式のファイルを指定する





