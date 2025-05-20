# git submodule

git-submodule - Initialize, update or inspect submodules

## SYNOPSIS

```
git submodule [--quiet] [--cached]
git submodule [--quiet] add [<options>] [--] <repository> [<path>]
git submodule [--quiet] status [--cached] [--recursive] [--] [<path>…​]
git submodule [--quiet] init [--] [<path>…​]
git submodule [--quiet] deinit [-f|--force] (--all|[--] <path>…​)
git submodule [--quiet] update [<options>] [--] [<path>…​]
git submodule [--quiet] set-branch [<options>] [--] <path>
git submodule [--quiet] set-url [--] <path> <newurl>
git submodule [--quiet] summary [<options>] [--] [<path>…​]
git submodule [--quiet] foreach [--recursive] <command>
git submodule [--quiet] sync [--recursive] [--] [<path>…​]
git submodule [--quiet] absorbgitdirs [--] [<path>…​]
```

## DESCRIPTION
サブモジュールを検査、更新、管理します。
サブモジュールの詳細についてはgitsubmodulesを参照してください。

## COMMANDS
引数を指定しない場合は、既存のサブモジュールのステータスを表示します。サブモジュールに対して操作を実行するためのサブコマンドがいくつかあります。

* add [-b \<branch>] [-f|--force] [--name \<name>] [--reference \<repository>] [--ref-format \<format>] [--depth \<depth>] [--] \<repository> [\<path>]

指定されたリポジトリを、現在のプロジェクトの次にコミットされる変更セットへの指定されたパスのサブモジュールとして追加します。現在のプロジェクトは「スーパープロジェクト」と呼ばれます。

\<repository> は、新しいサブモジュールの元のリポジトリの URL です。これは絶対 URL か、（./ または ../ で始まる場合は）スーパープロジェクトのデフォルトのリモートリポジトリからの相対パスで指定します（スーパープロジェクト bar.git のすぐ隣にあるリポジトリ foo.git を指定する場合は、./foo.git ではなく ../foo.git を使用する必要があります。これは、相対 URL のルールに従うと当然のことですが、Git における相対 URL の評価は相対ディレクトリの評価と同じであるためです）。

デフォルトのリモートは、現在のブランチのリモート追跡ブランチのリモートです。そのようなリモート追跡ブランチが存在しない場合、またはHEADがデタッチされている場合は、「origin」がデフォルトのリモートとみなされます。スーパープロジェクトにデフォルトのリモートが設定されていない場合、スーパープロジェクトは独自の権限のあるアップストリームとなり、代わりに現在の作業ディレクトリが使用されます。

オプションの引数 \<path> は、クローンされたサブモジュールがスーパープロジェクト内に存在する相対的な場所です。\<path> が指定されていない場合は、ソース リポジトリの正規部分が使用されます (「/path/to/repo.git」の場合は「repo」、 「host.xz:foo/.git」の場合は「foo」)。\<path> が存在し、既に有効な Git リポジトリである場合、クローンせずにコミットのためにステージングされます。\<path> は、--name を使用して論理名を指定しない限り、サブモジュールの設定エントリ内での論理名としても使用されます。

指定された URL は、スーパープロジェクトを複製する後続のユーザーが使用できるように .gitmodules に記録されます。URL がスーパープロジェクトのリポジトリからの相対パスで指定されている場合、スーパープロジェクトとサブモジュールのリポジトリは同じ相対パスに一緒に保存されるものとみなされ、スーパープロジェクトの URL のみを指定する必要があります。git-submodule は、.gitmodules 内の相対 URL を使用してサブモジュールを正しく見つけます。

--ref-format \<format> が指定されている場合、新しく複製されたサブモジュールの ref ストレージ形式がそれに応じて設定されます。

* status [--cached] [--recursive] [--] [\<path>…​]  
サブモジュールのステータスを表示します。これにより、各サブモジュールについて、現在チェックアウトされているコミットのSHA-1、サブモジュールのパス、およびSHA-1のgit describeの出力が表示されます。各SHA-1には、サブモジュールが初期化されていない場合は「-」、現在チェックアウトされているサブモジュールのコミットが、そのサブモジュールを含むリポジトリのインデックスにあるSHA-1と一致しない場合は「+」、サブモジュールにマージ競合がある場合は「U」がプレフィックスとして付加される可能性があります。  
--cached が指定されている場合、このコマンドは代わりに各サブモジュールのスーパープロジェクトに記録された SHA-1 を出力します。<br><br>--recursive が指定されている場合、このコマンドはネストされたサブモジュールを再帰的に実行し、それらのステータスも表示します。<br><br>インデックスまたはHEADに記録されたコミットに関して、現在初期化されているサブモジュールの変更のみに興味がある場合は、git-statusと git-diff でもその情報を提供します（サブモジュールの作業ツリーへの変更も報告できます）。

* init [--] [\<path>…​]
インデックスに記録されているサブモジュール（他の場所で追加およびコミットされたもの）を初期化するために、.git/config に submodule.$name.url を設定します。この設定は、.gitmodules と同じ設定をテンプレートとして使用します。URL が相対パスの場合、デフォルトのリモートリポジトリを使用して解決されます。デフォルトのリモートリポジトリが存在しない場合は、現在のリポジトリが上流リポジトリであるとみなされます。<br><br>オプションの\<path>引数は、初期化するサブモジュールを制限します。パスが指定されておらず、submodule.activeが設定されている場合は、アクティブに設定されているサブモジュールが初期化されます。それ以外の場合は、すべてのサブモジュールが初期化されます。<br><br>また、.gitmodules ファイルに submodule.$name.update の値が存在する場合は .git/config にコピーされますが、(1) このコマンドは .git/config 内の既存の情報を変更せず、(2) カスタム コマンドに設定されている submodule.$name.update はセキュリティ上の理由からコピーされません。<br><br>次に、ローカル セットアップの .git/config 内のサブモジュール クローン URL をカスタマイズし、git submodule update に進みます。サブモジュールの場所をカスタマイズするつもりがない場合は、明示的な init ステップなしで git submodule update --init を使用することもできます。
