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
