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
```
