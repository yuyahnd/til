# git-mv - Move or rename a file, a directory, or a symlink

[Git - git-mv Documentation](https://git-scm.com/docs/git-mv)

## オプション

|オプション|説明|
|:--|:--|
|-f<br>--force|ターゲットが存在する場合でも、ファイルの名前変更または移動を強制します|
|-k|エラー状態につながる移動または名前変更アクションをスキップします。 ソースが存在せず、Gitによって制御されていない場合、または-fが指定されていない限り、ソースが既存のファイルを上書きする場合、エラーが発生します。|
|-n<br>--dry-run|何もしない; 何が起こるかを示すだけ|
|-v<br>--verbose|移動するファイルの名前を報告します。|

## サブモジュール

gitfileを使用してサブモジュールを移動すると（つまり、Gitバージョン1.7.8以降で複製された）、gitfileとcore.worktreeの設定が更新され、サブモジュールが新しい場所で機能するようになります。 また、gitmodules [5]ファイルのsubmodule。<name> .path設定を更新し、そのファイルをステージングしようとします（-nが使用されている場合を除く）。
