# git-checkout - Switch branches or restore working tree files

[Git - git-checkout Documentation](https://git-scm.com/docs/git-checkout)


## オプション

|オプション|説明|
|:--|:--|
|git checkout [\<branch>]|\<branch>での作業の準備をするには、作業ツリーのインデックスとファイルを更新し、ブランチにHEADをポイントして、\<branch>に切り替えます。 \<branch>にコミットできるように、作業ツリー内のファイルに対するローカルの変更は保持されます。<br><br>\<branch>が見つからないが、一致する名前を持つ1つのリモート（\<remote>と呼びます）に追跡ブランチが存在し、-no-guessが指定されていない場合は、次と同等として扱います。|
|git checkout -b|-B \<new-branch> [\<start-point>]|-bを指定すると、git-branch が呼び出されてからチェックアウトされたかのように、新しいブランチが作成されます。 この場合、gitブランチに渡される--trackまたは--no-trackオプションを使用できます。 便宜上、-bなしの--trackはブランチの作成を意味します。 以下の--trackの説明を参照してください。|
|git checkout --detach [\<branch>]<br>git checkout [--detach] \<commit>|\<commit>でHEADをデタッチし（「DETACHEDHEAD」セクションを参照）、作業ツリー内のインデックスとファイルを更新することにより、\<commit>上で作業する準備をします。 作業ツリー内のファイルへのローカル変更は保持されるため、結果の作業ツリーは、コミットに記録された状態とローカル変更になります。|
