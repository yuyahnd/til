# git-show - Show various types of objects

[Git - git-show Documentation](https://git-scm.com/docs/git-show)

## オプション

|オプション|説明|
|:--|:--|
|\<object>…​|表示するオブジェクトの名前 (デフォルトは HEAD)。 オブジェクト名の綴り方の完全なリストについては、gitrevisions の「SPECIFYING REVISIONS」セクションを参照してください。|
|--pretty[=\<format>]<br>--format=\<format>|コミット ログの内容を特定の形式でプリティプリントします。\<format> は、oneline、short、medium、full、fuller、reference、email、raw、format:\<string> および tformat:\<string> のいずれかです。 \<format> が上記のいずれでもなく、%placeholder が含まれている場合、 --pretty=tformat:\<format> が指定されたかのように動作します。|
|--abbrev-commit|完全な 40 バイトの 16 進数のコミット オブジェクト名を表示する代わりに、オブジェクトを一意に指定するプレフィックスを表示します。 「--abbrev=\<n>」(表示されている場合は差分出力も変更します) オプションを使用して、プレフィックスの最小長を指定できます。|
|--no-abbrev-commit|完全な 40 バイトの 16 進数のコミット オブジェクト名を表示します。 これは、「--oneline」などの他のオプションによって明示的または暗示的に --abbrev-commit を無効にします。 また、log.abbrevCommit 変数をオーバーライドします。|
|--oneline|これは、一緒に使用される「--pretty=oneline --abbrev-commit」の省略形です。|
