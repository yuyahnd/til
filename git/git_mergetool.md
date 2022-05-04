# git-mergetool - Run merge conflict resolution tools to resolve merge conflicts

[Git - git-mergetool Documentation](https://git-scm.com/docs/git-mergetool)

## オプション

|オプション|説明|
|:--|:--|
|-t \<tool><br>--tool=\<tool>|\<tool>で指定されたマージ解決プログラムを使用します。 有効な値には、emerge、gvimdiff、kdiff3、meld、vimdiff、およびtortoisemergeが含まれます。 有効な\<tool>設定のリストについては、gitmergetool--tool-helpを実行してください。|
|--tool-help|--toolで使用できるマージツールのリストを印刷します。|
|-y<br>--no-prompt|マージ解決プログラムを呼び出す前にプロンプトを表示しないでください。 これは、マージ解決プログラムが--toolオプションまたはmerge.tool構成変数で明示的に指定されている場合のデフォルトです。|
|--prompt|マージ解決プログラムを呼び出す前にプロンプトを表示して、ユーザーにパスをスキップする機会を与えます。|
