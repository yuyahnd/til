# git-stash - Stash the changes in a dirty working directory away

[Git - git-stash Documentation](https://git-scm.com/docs/git-stash)

## オプション

|オプション|説明|
|:--|:--|
|-a<br>--all|このオプションは、プッシュおよび保存コマンドに対してのみ有効です。<br><br>無視され追跡されていないファイルもすべて隠しておき、git clean でクリーンアップします。|
|-u<br>--include-untracked<br>--no-include-untracked|push および save コマンドで使用すると、追跡されていないすべてのファイルも隠され、git clean でクリーンアップされます。<br><br>show コマンドで使用すると、スタッシュ エントリ内の追跡されていないファイルが diff の一部として表示されます。|
|--only-untracked|このオプションは、show コマンドに対してのみ有効です。<br><br>差分の一部として stash エントリ内の追跡されていないファイルのみを表示します。|
|--index|このオプションは、pop および apply コマンドに対してのみ有効です。<br><br>作業ツリーの変更だけでなく、インデックスの変更も復元しようとします。 ただし、これは競合がある場合に失敗する可能性があります (競合はインデックスに格納されているため、変更を元のように適用できなくなります)。|
|-k<br>--keep-index<br>--no-keep-index|このオプションは、プッシュおよび保存コマンドに対してのみ有効です。<br><br>インデックスに既に追加されているすべての変更はそのまま残ります。|
