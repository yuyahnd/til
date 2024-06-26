# git blame

## DESCRIPTION

指定されたファイルの各行に、その行を最後に変更したリビジョンの情報を注釈として付けます。 必要に応じて、指定されたリビジョンから注釈付けを開始します。

-L を 1 回以上指定すると、要求された行への注釈が制限されます。

ファイル全体の名前変更では、行の起点が自動的に追跡されます (現在、名前変更の追跡をオフにするオプションはありません)。 あるファイルから別のファイルに移動した行をたどる場合、または別のファイルからコピーして貼り付けた行をたどる場合などは、-C および -M オプションを参照してください。

このレポートでは、削除または置換された行については何も示されません。 git diff や、次の段落で簡単に説明する「pickaxe」インターフェイスなどのツールを使用する必要があります。

ファイル注釈のサポートとは別に、Git は変更時にコード スニペットが発生したときの開発履歴の検索もサポートします。 これにより、コード スニペットがファイルに追加されたとき、ファイル間で移動またはコピーされたとき、そして最終的に削除または置換されたときを追跡することが可能になります。 これは、diff 内のテキスト文字列を検索することで機能します。 blame_usage を検索するつるはしインターフェイスの小さな例:

```bash
$ git log --pretty=oneline -S'blame_usage'
5040f17eba15504bad66b14a645bddd9b015ebb7 blame -S <ancestry-file>
ea4c7f9bf69e781dd0cd88d2bccb2bf5cc15c9a7 git-blame: Make the output
```


## OPTIONS

* -b  
境界コミットには空の SHA-1 を表示します。 これは、blame.blankBoundary 設定オプションを介して制御することもできます。

* --root  
ルートコミットを境界として扱わないでください。 これは、blame.showroot configオプションを介して制御することもできます。

* --show-stats
非難出力の最後に追加の統計を含めます。

* -L \<start>,\<end>
* -L :\<funcname>
\<start>、\<end>、または関数名正規表現 \<funcname> で指定された行範囲のみに注釈を付けます。 複数回指定することも可能です。 重複する範囲は許可されます。

\<start> and \<end> are optional. -L \<start> or -L \<start>, spans from \<start> to end of file. -L ,\<end> spans from start of file to \<end>.

\<start> and <end> can take one of these forms:

* number  
\<start> または \<end> が数値の場合、絶対行番号 (行は 1 からカウントされます) を指定します。

* /regex/  
このフォームは、指定された POSIX 正規表現に一致する最初の行を使用します。 \<start> が正規表現の場合、前の -L 範囲があればその末尾から検索し、それ以外の場合はファイルの先頭から検索します。 \<start> が ^/regex/ の場合、ファイルの先頭から検索します。 \<end> が正規表現の場合、\<start> で指定された行から検索を開始します。

* +offset or -offset  
これは \<end> に対してのみ有効で、\<start> で指定された行の前後の行数を指定します。


\<start> と \<end> の代わりに :\<funcname> を指定すると、\<funcname> に一致する最初の funcname 行から次の funcname 行までの範囲を示す正規表現になります。 :\<funcname> は、前の -L 範囲があればその末尾から検索し、それ以外の場合はファイルの先頭から検索します。 ^:\<関数名> はファイルの先頭から検索します。 関数名は、git diff がパッチのハンク ヘッダーを処理するのと同じ方法で決定されます (gitattributes のカスタム ハンク ヘッダーの定義を参照)。

* -l  
長い回転を表示します (デフォルト: オフ)。

* -t  
生のタイムスタンプを表示します (デフォルト: オフ)。

* -S \<revs-file>  
git-rev-list を呼び出す代わりに、revs-file のリビジョンを使用します。

* --reverse \<rev>..\<rev>  
歴史を後戻りではなく前に進めます。 線が出現したリビジョンを表示する代わりに、線が存在した最後のリビジョンが表示されます。 これには、非難するパスが START に存在する START..END のような範囲のリビジョンが必要です。 便宜上、 gitblame --reverse START は gitblame --reverse START..HEAD として扱われます。

* --first-parent  
マージ コミットを確認したら、最初の親コミットのみをたどります。 このオプションを使用すると、行が履歴全体にいつ導入されたかではなく、特定の統合ブランチにいつ導入されたかを判断できます。

* -p  
* --porcelain  
マシンで使用できるように設計された形式で表示します。

* --line-porcelain  
磁器形式を表示しますが、コミットが最初に参照されたときだけでなく、各行のコミット情報を出力します。 --磁器を意味します。

* --incremental  
マシンで使用できるように設計された形式で結果を段階的に表示します。

* --encoding=\<encoding>  
著者名とコミット概要の出力に使用されるエンコーディングを指定します。 none に設定すると、blame は変換されていないデータを出力します。 詳細については、git-log マニュアル ページのエンコーディングに関する説明を参照してください。

* --contents \<file>  
指定されたファイルの内容を使用して注釈を付けます。指定されている場合は <rev> から始まり、それ以外の場合は HEAD から始まります。 - を指定すると、コマンドがファイルの内容を標準入力から読み取るようになります。

* --date \<format>  
日付の出力に使用する形式を指定します。 --date が指定されていない場合は、blame.date 構成変数の値が使用されます。 blame.date 構成変数も設定されていない場合は、iso 形式が使用されます。 サポートされている値については、git-log の --date オプションの説明を参照してください。

* --[no-]progress
進行状況は、端末に接続されている場合、デフォルトで標準エラー ストリームで報告されます。 このフラグにより、端末に接続されていない場合でも進捗レポートが可能になります。 --progress を --porcelain または --incremental と一緒に使用することはできません。

* -M[\<num>]  
ファイル内で移動またはコピーされた行を検出します。 コミットによって行のブロックが移動またはコピーされる場合 (たとえば、元のファイルには A があり、次に B があり、コミットによってそれが B、次に A に変更される)、従来の非難アルゴリズムは移動の半分だけを認識し、通常は移動された行を非難します。 上に移動した行 (つまり B) を親に移動し、下に移動した行 (つまり A) を子コミットに割り当てます。 このオプションを使用すると、追加の検査パスを実行することにより、両方の行グループが親のせいになります。<br><br>\<num> はオプションですが、Git がこれらの行を親コミットに関連付けるために、ファイル内の移動/コピーを検出する必要がある英数字の数の下限です。 デフォルト値は 20 です。

* -C[\<num>]  
-M に加えて、同じコミットで変更された他のファイルから移動またはコピーされた行を検出します。 これは、プログラムを再編成し、ファイル間でコードを移動する場合に便利です。 このオプションを 2 回指定すると、コマンドはファイルを作成するコミット内の他のファイルからのコピーをさらに検索します。 このオプションを 3 回指定すると、コマンドはさらに、コミット内の他のファイルからのコピーを検索します。<br><br>\<num> はオプションですが、Git がこれらの行を親コミットに関連付けるために、ファイル間の移動/コピーとして検出する必要がある英数字の数の下限です。 デフォルト値は 40 です。複数の -C オプションが指定されている場合は、最後の -C の \<num> 引数が有効になります。

* --ignore-rev \<rev>  
責任を割り当てるときは、変更がまったく起こらなかったかのように、リビジョンによって加えられた変更を無視します。 無視されたコミットによって変更または追加された行は、その行または近くの行を変更した前のコミットのせいになります。 このオプションを複数回指定すると、複数のリビジョンを無視できます。 blame.markIgnoredLines 構成オプションが設定されている場合、無視されたコミットによって変更され、別のコミットに起因する行には ? マークが付けられます。 非難出力で。 blame.markUnblamableLines 構成オプションが設定されている場合、無視されたコミットによって触れられ、別のリビジョンに帰することができなかった行には * のマークが付けられます。

* --ignore-revs-file \<file>
ファイルにリストされているリビジョンは無視します。このリビジョンは fsck.skipList と同じ形式である必要があります。 このオプションは繰り返すことができ、これらのファイルは、blame.ignoreRevsFile 構成オプションで指定されたファイルの後に処理されます。 空のファイル名「」を指定すると、以前に処理されたファイルのリビジョンのリストがクリアされます。

* --color-lines  
デフォルト形式の行注釈が前の行と同じコミットからのものである場合、行注釈の色が異なります。 これにより、さまざまなコミットによって導入されたコード ブロックを区別しやすくなります。 色はデフォルトでシアンですが、color.blame.repeatLines 構成オプションを使用して調整できます。

* --color-by-age  
デフォルト形式での線の経過時間に応じて、線の注釈を色付けします。 color.blame.highlightRecent 構成オプションは、年齢の範囲ごとに使用される色を制御します。

* -h  
ヘルプメッセージを表示します。

* -c  
git-annotate と同じ出力モードを使用します (デフォルト: オフ)。

* --score-debug  
ファイル間の行の移動 (-C を参照) およびファイル内で移動された行 (-M を参照) に関連するデバッグ情報を含めます。 リストされている最初の数字はスコアです。 これは、ファイル間またはファイル内で移動されたとして検出された英数字の数です。 gitblame がこれらのコード行が移動されたとみなすには、これが特定のしきい値を超えている必要があります。

* -f  
* --show-name  
元のコミットのファイル名を表示します。デフォルトでは、名前の変更検出により、異なる名前のファイルから取得した行がある場合にファイル名が表示されます。

* -n  
* --show-number  
元のコミットの行番号を表示します (デフォルト: オフ)。

* -s  
出力から著者名とタイムスタンプを抑制します。

* -e  
* --show-email  
著者名の代わりに著者のメール アドレスを表示します (デフォルト: オフ)。これは、blame.showEmail 構成オプションを介して制御することもできます。

* -w  
親バージョンと子バージョンを比較して行の出所を見つけるときは、空白を無視します。

* --abbrev=\<n>  
省略されたオブジェクト名としてデフォルトの 7+1 16 進数を使用する代わりに、\<m>+1 桁を使用します。ここで、\<m> は少なくとも \<n> ですが、コミット オブジェクト名が一意であることを保証します。境界コミットをマークするためのキャレットに 1 列が使用されることに注意してください。
