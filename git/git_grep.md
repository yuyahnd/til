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
