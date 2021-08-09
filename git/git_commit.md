# git commit

[Git - git-commit Documentation](https://git-scm.com/docs/git-commit)

## オプション

|オプション|説明|
|:--|:--|
|-a<br>--all|変更および削除されたファイルを自動的にステージングするようにコマンドに指示しますが、Gitに通知していない新しいファイルは影響を受けません。|
|-p<br>--patch|インタラクティブなパッチ選択インターフェイスを使用して、コミットする変更を選択します。 詳細については、git-add [1]を参照してください。|
|-C \<commit\><br>--reuse-message=\<commit\>|既存のコミットオブジェクトを取得し、コミットを作成するときにログメッセージと作成者情報（タイムスタンプを含む）を再利用します|
|-c \<commit\><br>--reedit-message=\<commit\>|-Cと同様ですが、-cを使用するとエディターが呼び出されるため、ユーザーはコミットメッセージをさらに編集できます。|
|--fixup=[(amend\|reword):]\<commit\>|git rebase --autosquashを適用すると、\<commit\>を「修正」する新しいコミットを作成します。 プレーン--fixup = \<commit\>は「fixup！」を作成します \<commit\>の内容を変更するが、ログメッセージは変更されないままにするcommit。 --fixup = amend：\<commit\>も同様ですが、「amend！」を作成します。 \<commit\>のログメッセージを「amend！」のログメッセージに置き換えるcommit。 専念。 --fixup = reword：\<commit\>は「修正」を作成します！ \<commit\>のログメッセージを独自のログメッセージに置き換えるが、\<commit\>の内容は変更しないcommit。<br><br>プレーン--fixup = \<commit\>によって作成されたコミットには、「fixup！」で構成されるサブジェクトがあります。 \<commit\>の件名が続き、git rebase--autosquashによって特別に認識されます。 -mオプションは、作成されたコミットのログメッセージを補足するために使用できますが、「修正」が完了すると、追加のコメントは破棄されます。 commitは、git rebase--autosquashによって\<commit\>に押しつぶされます。|
