# Google Colaboratoryでのファイルのアップロード
Goole Golaboratory （通称：Google Colab）での（主にデータの）ファイルのアップロードはなかなかの鬼門でハマったりするので、ここで改めてまとめてみた。

## 以前に使ったGoogle Colabのファイル自体を開く
- 「colab」などでググったりすると、Google Colabのページが開くので前に使ったファイルを選択して開く。（もしくは ファイル ＞ ノートブックを開く）
- 仮に複数のGoogleアカウントを持っていたりすると、別のアカウントでGoogle Colabを開こうとしている可能性もある。その場合、別アカウントのGoogle Colabのファイルは参照できない。
  - この場合は、一度、キャンセルなどしてファイルの選択画面を終了させた後、右上の自分のアイコンをクリックして適切なアカウントに切り替える。
- 画面左端のフォルダアイコンをクリックすると、アップロードされたファイルリストが見られる画面になる。
- たとえ前回に（データなどの）ファイルをアップロードしたとしても通常はここで sample_data しかリストされない。
  - Google Colabで、ディスクリソースを有効活用するため、自分がアップしたファイルはしばらくアクセスがなかったり時間のたったものはGoogle Colab上のスペースからファイルが消えてしまう。
  - ということで、ファイルの再アップロードから毎回スタートさせる。