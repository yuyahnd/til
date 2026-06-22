# git am

git-am - Apply a series of patches from a mailbox

## SYNOPSIS

```bash
git am [--signoff] [--keep] [--[no-]keep-cr] [--[no-]utf8] [--no-verify]
	 [--[no-]3way] [--interactive] [--committer-date-is-author-date]
	 [--ignore-date] [--ignore-space-change | --ignore-whitespace]
	 [--whitespace=<action>] [-C<n>] [-p<n>] [--directory=<dir>]
	 [--exclude=<path>] [--include=<path>] [--reject] [-q | --quiet]
	 [--[no-]scissors] [-S[<keyid>]] [--patch-format=<format>]
	 [--quoted-cr=<action>]
	 [--empty=(stop|drop|keep)]
	 [(<mbox> | <Maildir>)…​]
git am (--continue | --skip | --abort | --quit | --retry | --show-current-patch[=(diff|raw)] | --allow-empty)
```

## DESCRIPTION
メールボックス内のメールメッセージをコミットログメッセージ、作成者情報、パッチに分割し、現在のブランチに適用します。これは、マージのないストレートな履歴を持つブランチで実行されるgit-format-patch の逆の操作と考えることができます。

## OPTIONS

* (\<mbox>|\<Maildir>)…​
パッチを読み込むメールボックスファイルのリスト。この引数を指定しない場合、コマンドは標準入力から読み込みます。ディレクトリを指定した場合、それらはMaildirとして扱われます。

* -s
* --signoff
コミットメッセージに、自分のコミッターIDを使用してSigned-off-byトレーラーを追加します。

* -k
* --keep
-k フラグを git mailinfo に渡します (git-mailinfo を参照)。

* --keep-non-patch
git mailinfo に -b フラグを渡します (git-mailinfo を参照)。

* --keep-cr
* --no-keep-cr
--keep-cr を使用すると、git mailsplit (git-mailsplit を参照) を同じオプションで呼び出し、行末の CR が削除されないようにします。デフォルトの動作を指定するには、am.keepcr 設定変数を使用できます。--no-keep-cr は、am.keepcr を上書きするのに便利です。

* -c
* --scissors
はさみ行より前の本文中のすべてを削除します（git-mailinfo を参照）。mailinfo.scissors設定変数を使用すると、デフォルトで有効にできます。

* --no-scissors
ハサミの線は無視してください（git-mailinfoを参照）。

* --quoted-cr=\<action>
このフラグはgit mailinfoに渡されます（git-mailinfoを参照）。

* --empty=(drop|keep|stop)
パッチが適用されていないメールメッセージの対処方法：
	* drop
	  そのメールメッセージはスキップされます。
	* keep
	  空のコミットが作成され、そのログには電子メールメッセージの内容が記録されます。
	* stop
	  このコマンドは失敗し、現在のamセッションの途中で停止します。これはデフォルトの動作です。

* -m
* --message-id
git mailinfo に -m フラグを渡すと (git-mailinfo[1] を参照)、コミットメッセージに Message-ID ヘッダーが追加されます。デフォルトの動作を指定するには、am.messageid 設定変数を使用できます。

* --no-message-id
コミットメッセージに Message-ID ヘッダーを追加しないでください。no-message-id は am.messageid を上書きするのに便利です。

* -q
* --quiet
静かにしてください。エラーメッセージのみを表示してください。

* -u
* --utf8
git mailinfo に -u フラグを渡してください (git-mailinfo[1] を参照)。メールから取得したコミットログ候補メッセージが UTF-8 エンコーディングに変換されます (プロジェクトの優先エンコーディングが UTF-8 でない場合は、設定変数 i18n.commitEncoding を使用して指定できます)。<br><br>これは以前のバージョンの git ではオプションでしたが、現在はデフォルトです。--no-utf8 を使用すると、この設定を上書きできます。

* --no-utf8
git mailinfo に -n フラグを渡します (git-mailinfo を参照)。

* -3
* --3way
* --no-3way
パッチが正常に適用されない場合、パッチが適用対象のブロブの識別情報を記録し、それらのブロブがローカルで利用可能であれば、3 ウェイ マージにフォールバックします。--no-3way を使用すると、am.threeWay 設定変数を上書きできます。詳細については、git-config の am.threeWay を参照してください。

* --rerere-autoupdate
* --no-rerere-autoupdate
rerere メカニズムが現在の競合に対する記録された解決策を再利用して作業ツリー内のファイルを更新した後、解決結果でインデックスも更新できるようにします。 --no-rerere-autoupdate は、結果を別の git add でインデックスにコミットする前に、rerere が何をしたかを再確認し、潜在的なマージミスを検出するのに適した方法です。

* --ignore-space-change
* --ignore-whitespace
* --whitespace=\<action>
* -C\<n>
* -p\<n>
* --directory=\<dir>
* --exclude=\<path>
* --include=\<path>
* --reject
これらのフラグは、パッチを適用するgit applyプログラム（git-apply[1]を参照）に渡されます<br><br>--whitespaceオプションに指定できる有効な\<action>は、nowarn、warn、fix、error、error-allです。

* --patch-format
デフォルトでは、コマンドはパッチ形式を自動的に検出しようとします。このオプションを使用すると、自動検出をスキップして、パッチを解釈するパッチ形式を指定できます。有効な形式は、mbox、mboxrd、stgit、stgit-series、およびhgです。

* -i
* --interactive
対話形式で実行します。

* -n
* --no-verify
デフォルトでは、pre-applypatch と applypatch-msg フックが実行されます。--no-verify または -n のいずれかが指定されている場合は、これらのフックはスキップされます。githooks も参照してください。

* --committer-date-is-author-date
デフォルトでは、このコマンドは電子メールメッセージの日付をコミット作成者日付として記録し、コミット作成時刻をコミッター日付として使用します。このため、ユーザーは作成者日付と同じ値を使用することで、コミッター日付について虚偽の情報を入力することが可能になります。

* --ignore-date
デフォルトでは、このコマンドは電子メールメッセージの日付をコミット作成者日付として記録し、コミット作成時刻をコミッター日付として使用します。このため、ユーザーはコミッター日付に同じ値を使用することで、作成者日付について虚偽の情報を入力することが可能になります。

* --skip
現在のパッチをスキップします。これは、中断されたパッチを再開する場合にのみ有効です。

* -S[\<keyid>]
* --gpg-sign[=\<keyid>]
* --no-gpg-sign
GPG署名コミット。keyid引数はオプションで、デフォルトではコミッターIDになります。指定する場合は、スペースを入れずにオプションに連結する必要があります。--no-gpg-signは、commit.gpgSign設定変数と以前の--gpg-signの両方を無効にするのに役立ちます。

* --continue
* -r
* --resolved
パッチが失敗した後 (競合するパッチを適用しようとした場合など)、ユーザーは手動でパッチを適用し、適用結果はインデックス ファイルに保存されます。電子メール メッセージと現在のインデックス ファイルから抽出された作成者とコミット ログを使用してコミットを行い、続行します。

* --resolvemsg=\<msg>
パッチ適用に失敗すると、終了前に画面に\<msg>が表示されます。これは、エラー処理に--continueまたは--skipを使用するよう促す標準メッセージを上書きします。これはgit rebaseとgit am間の内部使用のみを目的としています。

* --abort
元のブランチを復元し、パッチ適用操作を中止します。am操作に関係するファイルの内容を、am操作前の状態に戻します。

* --quit
パッチ適用操作を中止するが、HEADとインデックスは変更しない。

* --retry
最後に適用した競合パッチを再度適用してみてください。これは通常、再試行時に追加のオプション（例：--3way）を渡す場合にのみ有効です。そうでない場合は、同じエラーが再び発生するだけです。

* --show-current-patch[=(diff|raw)]
git am が競合のために停止したメッセージを表示します。raw が指定されている場合は、電子メールメッセージの生のコンテンツを表示します。diff が指定されている場合は、差分部分のみを表示します。デフォルトは raw です。

* --allow-empty
パッチが適用されていない入力メールメッセージに対してパッチ適用が失敗した場合、そのメールメッセージの内容をログメッセージとして含む空のコミットを作成します。


## DISCUSSION

コミットの作成者名はメッセージの「From:」行から、コミットの作成日はメッセージの「Date:」行から取得されます。「Subject:」行は、共通接頭辞「"[PATCH <anything>]」を削除した後、コミットのタイトルとして使用されます。「Subject:」行には、コミットの内容を1行で簡潔に記述する必要があります。
