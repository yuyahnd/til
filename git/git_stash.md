# git-stash - Stash the changes in a dirty working directory away

[Git - git-stash Documentation](https://git-scm.com/docs/git-stash)

## オプション

|オプション|説明|
|:--|:--|
|-a<br>--all|このオプションは、プッシュおよび保存コマンドに対してのみ有効です。<br><br>無視され追跡されていないファイルもすべて隠しておき、git clean でクリーンアップします。|
|-u<br>--include-untracked<br>--no-include-untracked|push および save コマンドで使用すると、追跡されていないすべてのファイルも隠され、git clean でクリーンアップされます。<br><br>show コマンドで使用すると、スタッシュ エントリ内の追跡されていないファイルが diff の一部として表示されます。|
|--only-untracked|このオプションは、show コマンドに対してのみ有効です。<br><br>差分の一部として stash エントリ内の追跡されていないファイルのみを表示します。|
