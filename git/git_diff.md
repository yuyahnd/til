# git -diff

[Git - git-diff Documentation](https://git-scm.com/docs/git-diff)

## オプション

|オプション|説明|
|:--|:--|
|-p<br>-bu<br>--patch|パッチを生成します（パッチの生成に関するセクションを参照）。 これがデフォルトです。|
|-s<br>--no-patch|差分出力を抑制します。 デフォルトでパッチを表示するgitshowのようなコマンド、または--patchの効果をキャンセルする場合に便利です。|
|-U\<n\><br>--unified=\<n\>|通常の3行ではなく、\<n\>行のコンテキストで差分を生成します。 --patchを意味します。|
|--output=\<file\>|stdoutではなく特定のファイルに出力します。|
|--output-indicator-new=\<char\><br>--output-indicator-old=\<char\><br>--output-indicator-context=\<char\>|生成されたパッチの新しい行、古い行、またはコンテキスト行を示すために使用される文字を指定します。 通常、それらはそれぞれ+、-、および ''です。|
|--raw|生の形式で差分を生成します。|
|--patch-with-raw|-p --rawの同義語。|
|--indent-heuristic|差分ハンクの境界をシフトするヒューリスティックを有効にして、パッチを読みやすくします。 これがデフォルトです。|
|--no-indent-heuristic|インデントヒューリスティックを無効にします。|
|--minimal|可能な限り最小の差分が生成されるように、余分な時間を費やしてください。|
|--patience|「patience diff」アルゴリズムを使用してdiffを生成します。|
|--histogram|「ヒストグラムdiff」アルゴリズムを使用してdiffを生成します。|
|--anchored=\<text\>|"anchored diff" アルゴリズムを使用してdiffを生成します。<br><br>このオプションは複数回指定できます。<br><br>行がソースと宛先の両方に存在し、1回だけ存在し、このテキストで始まる場合、このアルゴリズムは、その行が出力に削除または追加として表示されないようにします。 内部で「忍耐差分」アルゴリズムを使用します。|
|--diff-algorithm={patience\|minimal\|histogram\|myers}|差分アルゴリズムを選択します。 バリアントは次のとおりです。※1|


※1
* default, myers  
  基本的な貪欲な差分アルゴリズム。 現在、これがデフォルトです。
* minimal  
  可能な限り最小の差分が生成されるように、余分な時間を費やしてください。
* patience  
  パッチを生成するときは、 "patience diff" アルゴリズムを使用してください。
* histogram  
  このアルゴリズムは、patience algorithmを拡張して、「発生率の低い共通要素をサポート」します。