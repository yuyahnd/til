# git-remote - Manage set of tracked repositories

[Git - git-remote Documentation](https://git-scm.com/docs/git-remote)

## オプション

|オプション|説明|
|:--|:--|
|-v<br>--verbose|もう少し冗長にして、名前の後にリモート URL を表示します。 promisor リモートの場合、構成されているフィルター (blob:none など) も表示します。 注: これは、リモートとサブコマンドの間に配置する必要があります。|

 ## コマンド
|コマンド|説明|
|:--|:--|
|add|\<URL> のリポジトリに \<name> という名前のリモートを追加します。 コマンド git fetch \<name> を使用して、リモート追跡ブランチ \<name>/\<branch> を作成および更新できます。|
|rename|\<old> という名前のリモートの名前を \<new> に変更します。 リモートのすべてのリモート追跡ブランチと構成設定が更新されます。|
|remove<br>rm|\<名前> という名前のリモートを削除します。 リモートのすべてのリモート追跡ブランチと構成設定が削除されます。|
