# git-show - Show various types of objects

[Git - git-show Documentation](https://git-scm.com/docs/git-show)

## オプション

|オプション|説明|
|:--|:--|
|\<object>…​|表示するオブジェクトの名前 (デフォルトは HEAD)。 オブジェクト名の綴り方の完全なリストについては、gitrevisions の「SPECIFYING REVISIONS」セクションを参照してください。|
|--pretty[=\<format>]<br>--format=\<format>|コミット ログの内容を特定の形式でプリティプリントします。\<format> は、oneline、short、medium、full、fuller、reference、email、raw、format:\<string> および tformat:\<string> のいずれかです。 \<format> が上記のいずれでもなく、%placeholder が含まれている場合、 --pretty=tformat:\<format> が指定されたかのように動作します。|
