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
パターンとファイル間の大文字と小文字の違いを無視します。

* -I
バイナリ ファイル内のパターンを一致させないでください。

* --max-depth \<depth>
コマンドラインで指定された各\<pathspec>について、最大\<depth>階層のディレクトリまで探索します。-1を指定すると、無制限となります。\<pathspec>に有効なワイルドカードが含まれている場合、このオプションは無視されます。つまり、「a*」が「a*」という名前のディレクトリに一致する場合、「*」は文字通り一致するため、--max-depthは依然として有効です。

* -r
* --recursive
--max-depth=-1 と同じです。これがデフォルトです。

* --no-recursive
--max-depth=0 と同じです。

* -w
* --word-regexp
パターンは単語境界でのみ一致します (行の先頭で始まるか、単語以外の文字が先行するか、行の末尾で終わるか、単語以外の文字が後続します)。

* -v
* --invert-match
一致しない行を選択します。

* -h
* -H
デフォルトでは、コマンドは一致するファイル名を表示します。この出力を抑制するには、-h オプションを使用します。-H は完全性のために用意されており、コマンドラインで先に指定した -h を上書きする以外は何も行いません。

* --full-name
サブディレクトリから実行した場合、コマンドは通常、現在のディレクトリを基準とした相対パスを出力します。このオプションは、プロジェクトのトップディレクトリを基準とした相対パスを強制的に出力します。

* -E
* --extended-regexp
* -G
* --basic-regexp
パターンにはPOSIX拡張/基本正規表現を使用します。デフォルトでは基本正規表現を使用します。

* -P
* --perl-regexp
パターンには Perl 互換の正規表現を使用します。<br><br>これらの正規表現のサポートは、コンパイル時のオプション依存関係です。Git がこれらの正規表現のサポートなしでコンパイルされている場合、このオプションを指定すると Git が動作しなくなります。

* -F
* --fixed-strings
パターンには固定文字列を使用します (パターンを正規表現として解釈しないでください)。

* -n
* --line-number
一致する行の前に行番号を付けます。

* --column
一致する行の先頭から最初の一致の 1 インデックス バイト オフセットをプレフィックスとして付加します。

* -l
* --files-with-matches
* --name-only
* -L
* --files-without-match
一致したすべての行を表示する代わりに、一致を含む（または含まない）ファイル名のみを表示します。git diffとの互換性を高めるため、--name-onlyは--files-with-matchesの同義語です。

* -O[\<pager>]
* --open-files-in-pager[=\<pager>]
一致するファイルをページャ（grepの出力ではありません）で開きます。ページャが「less」または「vi」で、ユーザーがパターンを1つしか指定していない場合、最初のファイルは自動的に最初の一致箇所に配置されます。ページャ引数はオプションです。指定する場合は、スペースを入れずにオプションに続けて指定する必要があります。ページャが指定されていない場合は、デフォルトのページャが使用されます（git-config[1]のcore.pagerを参照）。

* -z
* --null
出力においてパス名の区切り文字として \0 を使用し、そのまま出力します。このオプションを指定しない場合、「通常とは異なる」文字を含むパス名は、設定変数 core.quotePath の説明に従って引用符で囲まれます（git-config を参照）。

* -o
* --only-matching
一致する行の一致した部分 (空でない部分) のみを、各部分を別々の出力行に出力します。

* -c
* --count
一致した行をすべて表示するのではなく、一致する行の数を表示します。

* --color[=\<when>]
色分けされた一致を表示します。値は always（デフォルト）、never、または auto のいずれかにする必要があります。

* --no-color
設定ファイルでデフォルトでカラー出力が指定されている場合でも、一致の強調表示をオフにします。--color=never と同じです。

* --break
異なるファイルからの一致の間に空行を出力します。

* --heading
表示される各行の先頭ではなく、そのファイル内の一致の上にファイル名を表示します。

* -p
* --show-function
一致した行が関数名自体でない限り、一致した関数名を含む前の行を表示します。関数名は、git diffがパッチのハンクヘッダーを決定するのと同じ方法で決定されます（gitattributes のカスタムハンクヘッダーの定義を参照）。

* -\<num>
