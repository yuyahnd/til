# git-difftool - Show changes using common diff tools

[Git - git-difftool Documentation](https://git-scm.com/docs/git-difftool)

## オプション

|オプション|説明|
|:--|:--|
|-d<br>--dir-diff|変更したファイルを一時的な場所にコピーし、それらに対してディレクトリ diff を実行します。 このモードでは、差分ツールを起動する前にプロンプトが表示されることはありません。|
|-y<br>--no-prompt|差分ツールを起動する前にプロンプトを表示しません。|
|--prompt|差分ツールを呼び出すたびにプロンプトを表示します。 これがデフォルトの動作です。 任意の構成設定をオーバーライドするオプションが提供されています。|
|--rotate-to=\<file>|指定されたパスの差分の表示を開始します。パスが最後に移動して出力される前のパスです。|
