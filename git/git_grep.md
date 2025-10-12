# git grep

git-grep - Print lines matching a pattern

# SYNOPSIS

```bash
git grep [-a | --text] [-I] [--textconv] [-i | --ignore-case] [-w | --word-regexp]
	   [-v | --invert-match] [-h|-H] [--full-name]
	   [-E | --extended-regexp] [-G | --basic-regexp]
          [-P | --perl-regexp]
          [-F | --fixed-strings] [-n | --line-number] [--column]
          [-l | --files-with-matches] [-L | --files-without-match]
          [(-O | --open-files-in-pager) [<pager>]]
          [-z | --null]
          [ -o | --only-matching ] [-c | --count] [--all-match] [-q | --quiet]
          [--max-depth <depth>] [--[no-]recursive]
          [--color[=<when>] | --no-color]
          [--break] [--heading] [-p | --show-function]
          [-A <post-context>] [-B <pre-context>] [-C <context>]
          [-W | --function-context]
          [(-m | --max-count) <num>]
          [--threads <num>]
          [-f <file>] [-e] <pattern>
          [--and|--or|--not|(|)|-e <pattern>…​]
          [--recurse-submodules] [--parent-basename <basename>]
          [ [--[no-]exclude-standard] [--cached | --untracked | --no-index] | <tree>…​]
          [--] [<pathspec>…​]
```

# DESCRIPTION
作業ツリー内の追跡対象ファイル、インデックスファイルに登録されたBLOB、または指定されたツリーオブジェクト内のBLOBにおいて、指定されたパターンを検索します。パターンは、改行文字で区切られた1つ以上の検索式のリストです。検索式として空文字列を指定すると、すべての行に一致します。

# OPTIONS

* --cached 
作業ツリー内の追跡対象ファイルを検索する代わりに、インデックス ファイルに登録されている BLOB を検索します。

* --untracked
作業ツリー内の追跡されたファイルだけでなく、追跡されていないファイルも検索します。

* --no-index
現在のディレクトリ内でGitによって管理されていないファイル、または現在のディレクトリがGitによって管理されていることを無視してファイルを検索します。これは、通常のgrep(1)ユーティリティに-rオプションを指定して実行するのと似ていますが、pathspecパターンを使用してパスを制限するなど、いくつかの追加の利点があります。詳細については、gitglossary のpathspecの項目を参照してください。<br><br>このオプションは --cached または --untracked と同時に使用することはできません。以下の CONFIGURATION の grep.fallbackToNoIndex も参照してください。

* --no-exclude-standard
.gitignore メカニズムを無視することで、無視されたファイルも検索します。--untracked と併用した場合のみ有効です。

* --exclude-standard
.gitignore メカニズムで指定された無視対象ファイルには注意を払いません。--no-index で現在のディレクトリ内のファイルを検索する場合にのみ有効です。

* --recurse-submodules
リポジトリ内でアクティブかつチェックアウトされている各サブモジュールを再帰的に検索します。\<tree> オプションと組み合わせて使用​​した場合、すべてのサブモジュール出力のプレフィックスは親プロジェクトの \<tree> オブジェクトの名前になります。このオプションは --untracked と同時に使用することはできず、--no-index が指定されている場合は効果がありません。

* -a
* --text
バイナリ ファイルをテキストのように処理します。

* --textconv
textconv フィルター設定を尊重します。

* --no-textconv
textconvフィルタの設定を無視します。これがデフォルトです。

* -i
* --ignore-case
