# git blame

## DESCRIPTION

指定されたファイルの各行に、その行を最後に変更したリビジョンの情報を注釈として付けます。 必要に応じて、指定されたリビジョンから注釈付けを開始します。

-L を 1 回以上指定すると、要求された行への注釈が制限されます。

ファイル全体の名前変更では、行の起点が自動的に追跡されます (現在、名前変更の追跡をオフにするオプションはありません)。 あるファイルから別のファイルに移動した行をたどる場合、または別のファイルからコピーして貼り付けた行をたどる場合などは、-C および -M オプションを参照してください。

このレポートでは、削除または置換された行については何も示されません。 git diff や、次の段落で簡単に説明する「pickaxe」インターフェイスなどのツールを使用する必要があります。

ファイル注釈のサポートとは別に、Git は変更時にコード スニペットが発生したときの開発履歴の検索もサポートします。 これにより、コード スニペットがファイルに追加されたとき、ファイル間で移動またはコピーされたとき、そして最終的に削除または置換されたときを追跡することが可能になります。 これは、diff 内のテキスト文字列を検索することで機能します。 blame_usage を検索するつるはしインターフェイスの小さな例:

```bash
$ git log --pretty=oneline -S'blame_usage'
5040f17eba15504bad66b14a645bddd9b015ebb7 blame -S <ancestry-file>
ea4c7f9bf69e781dd0cd88d2bccb2bf5cc15c9a7 git-blame: Make the output
```


## OPTIONS

* -b  
境界コミットには空の SHA-1 を表示します。 これは、blame.blankBoundary 設定オプションを介して制御することもできます。

* --root  
ルートコミットを境界として扱わないでください。 これは、blame.showroot configオプションを介して制御することもできます。

* --show-stats
非難出力の最後に追加の統計を含めます。

* -L \<start>,\<end>
* -L :\<funcname>
\<start>、\<end>、または関数名正規表現 \<funcname> で指定された行範囲のみに注釈を付けます。 複数回指定することも可能です。 重複する範囲は許可されます。

\<start> and \<end> are optional. -L \<start> or -L \<start>, spans from \<start> to end of file. -L ,\<end> spans from start of file to \<end>.

\<start> and <end> can take one of these forms:

* number
