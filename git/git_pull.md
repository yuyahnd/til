# git-pull - Fetch from and integrate with another repository or a local branch

[Git - git-pull Documentation](https://git-scm.com/docs/git-pull)

## オプション

|オプション|説明|
|:--|:--|
|-q<br>--quiet|これは、転送中にレポートをスケルチするための基になる git-fetch と、マージ中に出力をスケルチするための基になる git-merge の両方に渡されます。|
|-v<br>--verbose|--verbose を git-fetch と git-merge に渡します。|
|--[no-]recurse-submodules[=yes\|on-demand\|no]|このオプションは、移入されたサブモジュールの新しいコミットをフェッチするかどうか、およびアクティブなサブモジュールの作業ツリーも更新するかどうかを制御します (git-fetch、git-config、および gitmodules を参照)。<br><br>チェックアウトがリベースによって行われる場合、ローカル サブモジュールのコミットもリベースされます。<br><br>更新がマージによって行われる場合、サブモジュールの競合は解決され、チェックアウトされます。|
