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

```
git bisect start --term-old <term-old> --term-new <term-new>
```

例えば、パフォーマンスの低下を引き起こしたコミットを探している場合は、次のようにします。

```
git bisect start --term-old fast --term-new slow
```

あるいはバグを修正したコミットを探している場合は、次のようにします。

```
git bisect start --term-new fixed --term-old broken
```

次に、git bisect good と git bisect bad の代わりに、git bisect \<term-old> と git bisect \<term-new> を使用してコミットをマークします。

## Bisect visualize/view
gitk に現在残っている容疑者を確認するには、二分プロセス中に次のコマンドを発行します (視覚化の代替としてサブコマンド view を使用できます)。

```
$ git bisect visualize
```

Git は、さまざまな環境変数を通じてグラフィカル環境を検出します。DISPLAY は、Unix システムの X Window System 環境で設定されます。SESSIONNAME は、Cygwin の対話型デスクトップ セッションで設定されます。MSYSTEM は、Msys2 および Git for Windows で設定されます。SECURITYSESSIONID は、macOS の対話型デスクトップ セッションで設定される場合があります。

これらの環境変数のいずれも設定されていない場合は、代わりに git log が使用されます。-p や --stat などのコマンドライン オプションを指定することもできます。

```
$ git bisect visualize --stat
```

## Bisect log and bisect replay
リビジョンを良好または不良としてマークした後、これまでに行われた処理を表示するには次のコマンドを実行します。

```
$ git bisect log
```

リビジョンのステータスの指定に誤りがあったことが判明した場合は、このコマンドの出力をファイルに保存し、編集して誤ったエントリを削除してから、次のコマンドを発行して修正された状態に戻すことができます。

```
$ git bisect reset
$ git bisect replay that-file
```

## Avoiding testing a commit
bisect セッションの途中で、提案されたリビジョンがテストに適していないことがわかった場合 (たとえば、ビルドに失敗し、その失敗が追跡しているバグとは何の関係もないことがわかっている場合)、近くのコミットを手動で選択して、代わりにそのコミットをテストできます。

例えば：

```
$ git bisect good/bad			# previous round was good or bad.
Bisecting: 337 revisions left to test after this (roughly 9 steps)
$ git bisect visualize			# oops, that is uninteresting.
$ git reset --hard HEAD~3		# try 3 revisions before what
                                # was suggested
```

次に、選択したリビジョンをコンパイルしてテストし、その後、通常の方法でリビジョンを良好または不良としてマークします。

## Bisect skip
近くのコミットを自分で選択する代わりに、次のコマンドを発行して Git にそれを実行するように依頼できます。

```
$ git bisect skip                 # Current version cannot be tested
```

ただし、探しているコミットに隣接するコミットをスキップすると、Git はそれらのコミットのうちどれが最初の不良コミットであったかを正確に判断できなくなります。

範囲表記を使用すると、1 つのコミットだけではなく、コミットの範囲をスキップすることもできます。例:

```
$ git bisect skip v2.5..v2.6
```

これは、bisect プロセスに、v2.5 以降、v2.6 までのコミットはテストされないことを指示します。

範囲の最初のコミットもスキップしたい場合は、次のコマンドを発行することに注意してください。

```
$ git bisect skip v2.5 v2.5..v2.6
```
これは、bisect プロセスに、v2.5 と v2.6 (含む) の間のコミットをスキップするように指示します。

## Cutting down bisection by giving more parameters to bisect start

追跡している問題にツリーのどの部分が関係しているかがわかっている場合は、bisect start コマンドを発行するときに pathspec パラメータを指定して、試行回数をさらに減らすことができます。

```
$ git bisect start -- arch/i386 include/asm-i386
```

事前に複数の正常なコミットがわかっている場合は、bisect start コマンドを発行するときに、不良コミットの直後にすべての正常なコミットを指定することにより、二分空間を狭めることができます。

```
$ git bisect start v2.6.20-rc6 v2.6.20-rc4 v2.6.20-rc1 --
                   # v2.6.20-rc6 is bad
                   # v2.6.20-rc4 and v2.6.20-rc1 are good
```

## Bisect run

現在のソース コードが適切かどうかを判断できるスクリプトがある場合は、次のコマンドを発行して二分することができます。

```
$ git bisect run my_script arguments
```

スクリプト (上記の例では my_script) は、現在のソース コードが適切/古い場合はコード 0 で終了し、現在のソース コードが不適切/新しい場合は 1 から 127 (両端を含む) のコード (125 を除く) で終了することに注意してください。

その他の終了コードは、bisect プロセスを中止します。exit(-1) で終了するプログラムは、値が & 0377 で切り詰められるため、$? = 255 のままになることに注意してください (exit(3) のマニュアル ページを参照)。

現在のソース コードをテストできない場合は、特別な終了コード 125 を使用する必要があります。スクリプトがこのコードで終了すると、現在のリビジョンはスキップされます (上記の git bisect skip を参照)。125 は、この目的に使用する最も妥当な値として選択されました。これは、126 と 127 が POSIX シェルによって特定のエラー ステータスを通知するために使用されるためです (127 はコマンドが見つからない場合、126 はコマンドが見つかったが実行可能でない場合です。これらの詳細は、bisect run に関する限り、スクリプト内の通常のエラーであるため重要ではありません)。

bisect セッション中に、テスト対象のリビジョンに一時的な変更 (例: ヘッダー ファイルの s/#define DEBUG 0/#define DEBUG 1/、または「このコミットがないリビジョンには、この bisection の対象ではない別の問題を回避するためにこのパッチを適用する必要がある」) を適用したいことがよくあるかもしれません。

このような状況に対処するには、内部の git bisect がテストする次のリビジョンを見つけた後、スクリプトはコンパイル前にパッチを適用し、実際のテストを実行し、その後、リビジョン (必要なパッチを含む可能性あり) がテストに合格したかどうかを判断し、ツリーを元の状態に戻します。最後に、スクリプトは実際のテストのステータスで終了し、git bisect run コマンド ループが bisect セッションの最終的な結果を判断できるようにします。

## OPTIONS

* --no-checkout  
二分プロセスの各反復で新しい作業ツリーをチェックアウトしないでください。代わりに、BISECT_HEAD という名前の参照を更新して、テストする必要があるコミットを指すようにします。<br><br>このオプションは、各ステップで実行するテストでチェックアウトされたツリーが必要ない場合に役立ちます。<br><br>リポジトリが bare の場合、--no-checkout が想定されます。

* --first-parent  
マージコミットが表示されたら、最初の親コミットのみに従います。<br><br>ブランチのマージによって導入された回帰を検出する場合、マージ コミットはバグの導入として識別され、その祖先は無視されます。<br><br>このオプションは、マージされたブランチに壊れたコミットやビルドできないコミットが含まれていても、マージ自体は正常である場合に、誤検知を回避するのに特に役立ちます。

## EXAMPLES

* 壊れたビルドを v1.2 と HEAD の間で自動的に二分します。  

```
$ git bisect start HEAD v1.2 --      # HEAD is bad, v1.2 is good
$ git bisect run make                # "make" builds the app
$ git bisect reset                   # quit the bisect session
```

* テストの失敗を origin と HEAD の間で自動的に二分します。  

```
$ git bisect start HEAD origin --    # HEAD is bad, origin is good
$ git bisect run make test           # "make test" builds and tests
$ git bisect reset                   # quit the bisect session
```

* 壊れたテストケースを自動的に二分する:  

```
$ cat ~/test.sh
#!/bin/sh
make || exit 125                     # this skips broken builds
~/check_test_case.sh                 # does the test case pass?
$ git bisect start HEAD HEAD~10 --   # culprit is among the last 10
$ git bisect run ~/test.sh
$ git bisect reset                   # quit the bisect session
```

ここでは、test.sh カスタム スクリプトを使用します。このスクリプトでは、make が失敗した場合、現在のコミットをスキップします。check_test_case.sh は、テスト ケースが成功した場合は 0 で終了し、そうでない場合は 1 で終了する必要があります。

bisect、make、test プロセスとスクリプト間の相互作用を防ぐために、test.sh と check_test_case.sh の両方をリポジトリの外部に配置する方が安全です。

* 一時的な変更を加えて自動的に二分する (ホットフィックス):  

```
$ cat ~/test.sh
#!/bin/sh

# tweak the working tree by merging the hot-fix branch
```
