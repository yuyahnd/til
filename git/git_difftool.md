# git-difftool - Show changes using common diff tools

[Git - git-difftool Documentation](https://git-scm.com/docs/git-difftool)

## オプション

|オプション|説明|
|:--|:--|
|-d<br>--dir-diff|変更したファイルを一時的な場所にコピーし、それらに対してディレクトリ diff を実行します。 このモードでは、差分ツールを起動する前にプロンプトが表示されることはありません。|
|-y<br>--no-prompt|差分ツールを起動する前にプロンプトを表示しません。|
|--prompt|差分ツールを呼び出すたびにプロンプトを表示します。 これがデフォルトの動作です。 任意の構成設定をオーバーライドするオプションが提供されています。|
|--rotate-to=\<file>|指定されたパスの差分の表示を開始します。パスが最後に移動して出力される前のパスです。|
|--skip-to=\<file>|指定されたパスの差分の表示を開始し、その前のすべてのパスをスキップします。|
|-t \<tool><br>--tool=\<tool>|\<tool> で指定された差分ツールを使用します。 有効な値には、emerge、kompare、meld、および vimdiff が含まれます。 有効な \<tool> 設定のリストについては、 git difftool --tool-help を実行してください。|
|--tool-help|--tool で使用できる差分ツールのリストを出力します。|
|--[no-]symlinks|git difftool のデフォルトの動作は、 --dir-diff モードで実行すると作業ツリーへのシンボリック リンクを作成することであり、比較の右側は作業ツリー内のファイルと同じ内容になります。<br><br>--no-symlinks を指定すると、代わりにコピーを作成するように git difftool に指示します。 --no-symlinks が Windows のデフォルトです。|
|-x \<command><br>--extcmd=\<command>|差分を表示するためのカスタム コマンドを指定します。 このオプションが指定されている場合、git-difftool は構成されたデフォルトを無視し、$command $LOCAL $REMOTE を実行します。 さらに、環境に $BASE が設定されています。|
|-g<br>--[no-]gui|git-difftool が -g または --gui オプションで呼び出されると、デフォルトの diff ツールは、diff.tool ではなく、構成された diff.guitool 変数から読み取られます。 --no-gui オプションを使用して、この設定をオーバーライドできます。 diff.guitool が設定されていない場合は、ツールが見つかるまで、merge.guitool、diff.tool、merge.tool の順にフォールバックします。|
