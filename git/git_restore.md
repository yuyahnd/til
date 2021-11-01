# git-restore - Restore working tree files

[Git - git-restore Documentation](https://git-scm.com/docs/git-restore)

## オプション

|オプション|説明|
|:--|:--|
|-s \<tree><br>--source=\<tree>|指定されたツリーのコンテンツを使用して、作業ツリーファイルを復元します。 ソースツリーに関連付けられているコミット、ブランチ、またはタグに名前を付けてソースツリーを指定するのが一般的です。<br>指定しない場合、-stagedが指定されている場合はHEADから、それ以外の場合はインデックスから内容が復元されます。<br>特別な場合として、マージベースが1つしかない場合は、AとBのマージベースのショートカットとして「A ... B」を使用できます。 AとBの最大1つを省略できます。その場合、デフォルトでHEADになります。|
