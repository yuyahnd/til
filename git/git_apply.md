# git apply

## NAME
git-apply - Apply a patch to files and/or to the index

## DESCRIPTION 
提供された diff 出力 (つまり「パッチ」) を読み取り、ファイルに適用します。リポジトリ内のサブディレクトリから実行する場合、ディレクトリ外のパッチ パスは無視されます。--index オプションを使用すると、パッチはインデックスにも適用され、--cached オプションを使用すると、パッチはインデックスにのみ適用されます。これらのオプションがない場合、コマンドはファイルにのみパッチを適用し、ファイルが Git リポジトリ内にある必要はありません。

このコマンドはパッチを適用しますが、コミットは作成しません。git-format-patch[1]によって生成されたパッチや電子メールで受信したパッチからコミットを作成するには、git-am[1]を使用します。

## OPTIONS

* \<patch>…​  
パッチを読み込むファイル。- は標準入力から読み取るために使用できます。

* --stat  
パッチを適用する代わりに、入力の diffstat を出力します。「apply」をオフにします。

* --numstat  
--stat に似ていますが、マシンフレンドリーになるように、追加および削除された行数を 10 進表記で表示し、パス名を省略せずに表示します。バイナリ ファイルの場合、0 0 ではなく 2 つの - を出力します。「適用」をオフにします。

* --summary  
パッチを適用する代わりに、作成、名前の変更、モードの変更など、git diff 拡張ヘッダーから取得した情報の要約を出力します。「適用」をオフにします。

* --check  
パッチを適用する代わりに、パッチが現在の作業ツリーやインデックス ファイルに適用可能かどうかを確認し、エラーを検出します。「適用」をオフにします。

* --index  
パッチをインデックスと作業ツリーの両方に適用します (または、--check が有効な場合は、両方にパッチが適切に適用されるかどうかを確認します)。--index は、関連するパスのインデックス エントリと作業ツリーのコピーが同一である (その内容とファイル モードなどのメタデータが一致している必要がある) ことを想定しており、パッチがインデックスと作業ツリーの両方に個別に適切に適用される場合でも、同一でない場合はエラーが発生することに注意してください。

* --cached  
作業ツリーには触れずに、インデックスのみにパッチを適用します。--check が有効な場合は、インデックス エントリにパッチが適切に適用されるかどうかのみをチェックします。

* --intent-to-add  
パッチを作業ツリーにのみ適用する場合、後でインデックスに追加される新しいファイルをマークします (git-add[1] の --intent-to-add オプションを参照)。このオプションは、Git リポジトリで実行され、--index が指定されていない場合を除き、無視されます。--index は、--cached や --3way などの他のオプションによって暗示される可能性があることに注意してください。
