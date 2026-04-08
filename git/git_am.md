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
