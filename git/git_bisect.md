# git bisect

git-bisect - Use binary search to find the commit that introduced a bug

# SYNOPSIS

```
git bisect <subcommand> <options>
```

# DESCRIPTION
このコマンドはさまざまなサブコマンドを取り、サブコマンドに応じて異なるオプションを取ります。

```
git bisect start [--term-(bad|new)=<term-new> --term-(good|old)=<term-old>]
	  [--no-checkout] [--first-parent] [<bad> [<good>...]] [--] [<pathspec>...]
git bisect (bad|new|<term-new>) [<rev>]
git bisect (good|old|<term-old>) [<rev>...]
git bisect terms [--term-(good|old) | --term-(bad|new)]
git bisect skip [(<rev>|<range>)...]
git bisect reset [<commit>]
git bisect (visualize|view)
git bisect replay <logfile>
git bisect log
git bisect run <cmd> [<arg>...]
git bisect help
```

このコマンドは、バイナリ検索アルゴリズムを使用して、プロジェクトの履歴にどのコミットがバグを導入したかを見つけます。最初に、バグを含むことが知られている「悪い」コミットと、バグが導入される前に知られている「良い」コミットを伝えることで使用します。次に、git bisectはこれらの2つのエンドポイントの間にコミットを選択し、選択したコミットが「良い」か「悪い」かどうかを尋ねます。変更を導入した正確なコミットが見つかるまで、範囲を絞り続けます。
