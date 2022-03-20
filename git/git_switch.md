# git-switch - Switch branches

[Git - git-switch Documentation](https://git-scm.com/docs/git-switch)

## オプション

|オプション|説明|
|:--|:--|
|\<branch>|切り替えるブランチ。|
|\<new-branch>|新しいブランチの名前。|
|\<start-point>|新しいブランチの開始点。 <start-point>を指定すると、HEADが現在ポイントしている場所以外の履歴内のポイントに基づいてブランチを作成できます。 （または、-detachの場合、他のポイントを検査してデタッチすることができます。）<br><br>@ {-N}構文を使用して、「gitswitch」または「gitcheckout」操作を使用して切り替えられたN番目の最後のブランチ/コミットを参照できます。 @{-1}と同義の--を指定することもできます。 これは、2つのブランチをすばやく切り替えたり、誤ってブランチの切り替えを元に戻したりするためによく使用されます。<br><br>特別な場合として、マージベースが1つしかない場合は、AとBのマージベースのショートカットとしてA...Bを使用できます。 最大でAとBのいずれかを省略できます。その場合、デフォルトでHEADになります。|
|-c \<new-branch><br>--create \<new-branch>|ブランチに切り替える前に、<start-point>から始まる<new-branch>という名前の新しいブランチを作成します。 これは、次の便利なショートカットです。|
|-C \<new-branch><br>--force-create \<new-branch>|--createと似ていますが、\<new-branch>がすでに存在する場合は、\<start-point>にリセットされる点が異なります。|
|-d<br>--detach|検査と破棄可能な実験のためにコミットに切り替えます。 詳細については、git-checkoutの「DETACHEDHEAD」セクションを参照してください。|
|--guess<br>--no-guess|\<branch>が見つからないが、名前が一致する1つのリモート（\<remote>と呼びます）に追跡ブランチが存在する場合は、次のように扱います。`$ git switch -c <branch> --track <remote>/<branch>`|
|-f<br>--force|--discard-changesのエイリアス。|
