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
|--encoding=\<encoding>|コミット オブジェクトは、ログ メッセージに使用される文字エンコーディングをエンコーディング ヘッダーに記録します。 このオプションを使用して、ユーザーが好むエンコーディングでコミット ログ メッセージを再コード化するようにコマンドに指示できます。 非配管コマンドの場合、これはデフォルトで UTF-8 になります。 オブジェクトが X でエンコードされていると主張し、X で出力している場合、オブジェクトを逐語的に出力することに注意してください。 これは、元のコミットの無効なシーケンスが出力にコピーされる可能性があることを意味します。 同様に、iconv(3) がコミットの変換に失敗した場合、元のオブジェクトを逐語的に静かに出力します。|
|--expand-tabs=\<n><br>--expand-tabs<br>--no-expand-tabs|ログ メッセージを出力に表示する前に、ログ メッセージでタブ展開を実行します (各タブを \<n> の倍数である次の表示列に入力するのに十分なスペースに置き換えます)。 --expand-tabs は --expand-tabs=8 の省略形であり、 --no-expand-tabs は --expand-tabs=0 の省略形であり、タブ展開を無効にします。|
|--notes[=\<ref>]|コミット ログ メッセージを表示するときに、コミットに注釈を付けるメモ (git-notes を参照) を表示します。 これは、コマンド ラインで --pretty、--format、または --oneline オプションが指定されていない場合の git log、git show、および git whatchanged コマンドのデフォルトです。|
|--no-notes|メモを表示しない。 これは、メモが表示されるメモ参照のリストをリセットすることにより、上記の --notes オプションを無効にします。 オプションは、コマンド ラインで指定された順序で解析されます。 「--notes --notes=foo --no-notes --notes=bar」は、「refs/notes/bar」からのメモのみを表示します。|
|--show-notes[=\<ref>]<br>--[no-]standard-notes|これらのオプションは非推奨です。 代わりに上記の --notes/--no-notes オプションを使用してください。|
|--show-signature|署名を gpg --verify に渡して、署名されたコミット オブジェクトの有効性を確認し、出力を表示します。|
