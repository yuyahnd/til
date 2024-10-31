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

```
$ git bisect reset
```
デフォルトでは、Git Bisectが開始される前にチェックアウトされたコミットにツリーを返します。 （新しいgit bisectスタートも、古い二等分状態をクリーンアップするため、それを行います。）

オプションの引数を使用すると、代わりに別のコミットに戻ることができます。

```
$ git bisect reset <commit>
```
たとえば、git bisect reset bisect/bad は最初の不良リビジョンをチェックアウトしますが、git bisect reset HEAD は現在のバイセクション コミットのままにして、コミットの切り替えをまったく回避します。

## Alternate terms

場合によっては、破損をもたらしたコミットではなく、他の「古い」状態と「新しい」状態の間の変更を引き起こしたコミットを探していることがあります。たとえば、特定の修正を導入したコミットを探している場合があります。または、ソース コードのファイル名が最終的にすべて会社の命名標準に変換された最初のコミットを探している場合もあります。

このような場合、「変更前の状態」と「変更後の状態」を指すのに「良好」と「不良」という用語を使用すると、非常に混乱を招く可能性があります。そのため、「良好」と「不良」の代わりに、それぞれ「古い」と「新しい」という用語を使用できます。(ただし、1 つのセッションで「良好」と「不良」を「古い」と「新しい」と混在させることはできないことに注意してください。)

このより一般的な使用法では、何らかのプロパティを持つ「新しい」コミットと、そのプロパティを持たない「古い」コミットを git bisect に渡します。git bisect がコミットをチェックアウトするたびに、そのコミットにプロパティがあるかどうかをテストします。プロパティがある場合は、コミットを「新しい」としてマークし、ない場合は「古い」としてマークします。二分法が完了すると、git bisect はどのコミットでプロパティが導入されたかを報告します。

「good」と「bad」の代わりに「old」と「new」を使用するには、コミットを引数として指定せずに git bisect start を実行し、次のコマンドを実行してコミットを追加する必要があります。

```
git bisect old [<rev>]
```
コミットが要求された変更の前にあったことを示す、または

```
git bisect new [<rev>...]
```
それ以降であることを示すために使用します。
現在使用されている用語を確認するには、

```
git bisect terms
```

git bisect terms --term-old または git bisect terms --term-good を使用すると、古い用語だけを取得できます。git bisect terms --term-new および git bisect terms --term-bad を使用すると、目的の変更よりも新しいコミットを呼び出す方法を知ることができます。

「悪い」/「良い」や「新しい」/「古い」の代わりに独自の用語を使用したい場合は、任意の名前を選択できます（reset、startなどの既存のbisectサブコマンドを除く）。
