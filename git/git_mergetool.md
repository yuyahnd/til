# git-mergetool - Run merge conflict resolution tools to resolve merge conflicts

[Git - git-mergetool Documentation](https://git-scm.com/docs/git-mergetool)

## オプション

|オプション|説明|
|:--|:--|
|-t \<tool><br>--tool=\<tool>|\<tool>で指定されたマージ解決プログラムを使用します。 有効な値には、emerge、gvimdiff、kdiff3、meld、vimdiff、およびtortoisemergeが含まれます。 有効な\<tool>設定のリストについては、gitmergetool--tool-helpを実行してください。|
|--tool-help|--toolで使用できるマージツールのリストを印刷します。|
|-y<br>--no-prompt|マージ解決プログラムを呼び出す前にプロンプトを表示しないでください。 これは、マージ解決プログラムが--toolオプションまたはmerge.tool構成変数で明示的に指定されている場合のデフォルトです。|
|--prompt|マージ解決プログラムを呼び出す前にプロンプトを表示して、ユーザーにパスをスキップする機会を与えます。|
|-g<br>--gui|-gまたは--guiオプションを指定してgit-mergetoolを呼び出すと、デフォルトのマージツールがmerge.toolではなく構成済みのmerge.guitool変数から読み取られます。 merge.guitoolが設定されていない場合、merge.toolで構成されたツールにフォールバックします。|
|--no-gui|これにより、以前の-gまたは--gui設定が上書きされ、デフォルトのマージツールが設定されたmerge.tool変数から読み取られます。|
|-O\<orderfile>|<orderfile>で指定された順序でファイルを処理します。これには、1行に1つのシェルグロブパターンがあります。 これは、diff.orderFile構成変数をオーバーライドします（git-config を参照）。 diff.orderFileをキャンセルするには、-O / dev/nullを使用します。|
