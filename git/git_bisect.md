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

実際、git bisect を使用すると、プロジェクトのプロパティを変更したコミットを見つけることができます。たとえば、バグを修正したコミットや、ベンチマークのパフォーマンスを向上させたコミットなどです。このより一般的な使用法をサポートするために、「良い」と「悪い」の代わりに「古い」と「新しい」という用語を使用したり、独自の用語を選択したりできます。詳細については、以下の「代替用語」セクションを参照してください。

### Basic bisect commands: start, bad, good

たとえば、プロジェクトのバージョン v2.6.13-rc2 で動作することがわかっている機能を壊したコミットを見つけようとしているとします。次のようにして bisect セッションを開始します。

```
$ git bisect start
$ git bisect bad                 # Current version is bad
$ git bisect good v2.6.13-rc2    # v2.6.13-rc2 is known to be good
```
少なくとも 1 つの不良コミットと 1 つの正常なコミットを指定すると、git bisect はその履歴の範囲の中央にあるコミットを選択し、それをチェックアウトして、次のような出力を行います。

```
Bisecting: 675 revisions left to test after this (roughly 10 steps)
```

チェックアウトしたバージョンをコンパイルしてテストします。そのバージョンが正しく動作する場合は、次のように入力します。

```
$ git bisect good
```

そのバージョンが壊れている場合は、
```
$ git bisect bad
```
するとgit bisectは次のような応答を返す。
```
Bisecting: 337 revisions left to test after this (roughly 9 steps)
```
このプロセスを繰り返します。ツリーをコンパイルし、テストし、それが良いか悪いかに応じて、git bisect good または git bisect bad を実行して、テストが必要な次のコミットを要求します。

最終的に検査するリビジョンがなくなり、コマンドは最初の不良コミットの説明を出力します。参照 refs/bisect/bad はそのコミットを指すままになります。

## Bisect reset
二分セッションの後、二分状態をクリーンアップして元の HEAD に戻すには、次のコマンドを発行します。
