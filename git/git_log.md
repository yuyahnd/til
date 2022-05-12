# git-log - Show commit logs

[Git - git-log Documentation](https://git-scm.com/docs/git-log)

## オプション

|オプション|説明|
|:--|:--|
|--follow|名前の変更を超えてファイルの履歴を一覧表示し続けます（単一のファイルに対してのみ機能します）。|
|--no-decorate<br>--decorate[=short\|full\|auto\|no]|表示されているコミットの参照名を出力します。 shortが指定されている場合、ref名のプレフィックスrefs / heads /、refs / tags /、およびrefs /remotes/は出力されません。 fullを指定すると、完全な参照名（プレフィックスを含む）が出力されます。 autoが指定されている場合、出力が端末に送られる場合、参照名はshortが指定されているかのように表示されます。それ以外の場合、参照名は表示されません。 オプション--decorateは、-decorate=shortの省略形です。 デフォルトはlog.decorateの構成値で、構成されている場合はautoです。|
|--decorate-refs=\<pattern><br>--decorate-refs-exclude=\<pattern>|--decorate-refsが指定されていない場合は、すべてのrefが含まれているように見せかけます。 候補ごとに、-decorate-refs-excludeに指定されたパターンと一致する場合、または--decorate-refsに指定されたパターンのいずれとも一致しない場合は、装飾に使用しないでください。 log.excludeDecoration構成オプションを使用すると、装飾からrefを除外できますが、明示的な--decorate-refsパターンは、log.excludeDecorationの一致をオーバーライドします。|
|--source|各コミットに到達したコマンドラインで指定された参照名を出力します。|
