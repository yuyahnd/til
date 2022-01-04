# git-branch - List, create, or delete branches

[Git - git-branch Documentation](https://git-scm.com/docs/git-branch)

## オプション

|オプション|説明|
|:--|:--|
|-d<br>--delete|ブランチを削除します。 ブランチは、アップストリームブランチで完全にマージする必要があります。アップストリームが--trackまたは--set-upstream-toで設定されていない場合は、HEADでマージする必要があります。|
|-D|--delete--forceのショートカット。|
|--create-reflog|ブランチのreflogを作成します。 これにより、ブランチrefに加えられたすべての変更の記録がアクティブになり、「<branchname> @ {yesterday}」などの日付ベースのsha1式を使用できるようになります。 非ベアリポジトリでは、通常、reflogはcore.logAllRefUpdates構成オプションによってデフォルトで有効になっていることに注意してください。 否定された形式--no-create-reflogは、以前の--create-reflogをオーバーライドするだけですが、現在、core.logAllRefUpdatesの設定を否定しません。|
|-f<br>--force|\<branchname>がすでに存在する場合でも、\<branchname>を\<startpoint>にリセットします。 -fがないと、gitブランチは既存のブランチの変更を拒否します。 -d（または--delete）と組み合わせて、マージされたステータスに関係なく、または有効なコミットを指しているかどうかに関係なく、ブランチを削除できるようにします。 -m（または--move）と組み合わせて、新しいブランチ名がすでに存在する場合でもブランチの名前を変更できるようにします。同じことが-c（または--copy）にも当てはまります。|
|-m<br>--move|ブランチをそのconfigおよびreflogとともに移動/名前変更します。|
|-M|--move--forceのショートカット。|
|-c<br>--copy|ブランチをそのconfigおよびreflogと一緒にコピーします。|
