# git-pull - Fetch from and integrate with another repository or a local branch

[Git - git-pull Documentation](https://git-scm.com/docs/git-pull)

## オプション

|オプション|説明|
|:--|:--|
|-q<br>--quiet|これは、転送中にレポートをスケルチするための基になる git-fetch と、マージ中に出力をスケルチするための基になる git-merge の両方に渡されます。|
|-v<br>--verbose|--verbose を git-fetch と git-merge に渡します。|
|--[no-]recurse-submodules[=yes\|on-demand\|no]|このオプションは、移入されたサブモジュールの新しいコミットをフェッチするかどうか、およびアクティブなサブモジュールの作業ツリーも更新するかどうかを制御します (git-fetch、git-config、および gitmodules を参照)。<br><br>チェックアウトがリベースによって行われる場合、ローカル サブモジュールのコミットもリベースされます。<br><br>更新がマージによって行われる場合、サブモジュールの競合は解決され、チェックアウトされます。|
|--commit<br>--no-commit|マージを実行し、結果をコミットします。 このオプションは --no-commit をオーバーライドするために使用できます。 マージするときにのみ役立ちます。<br><br>--no-commit を使用してマージを実行し、マージ コミットを作成する直前に停止して、コミットする前にマージ結果を調べてさらに微調整する機会をユーザーに与えます。<br><br>早送り更新ではマージ コミットが作成されないため、これらのマージを --no-commit で停止する方法がないことに注意してください。 したがって、ブランチがマージ コマンドによって変更または更新されないようにする場合は、--no-ff を --no-commit と共に使用します。|
|--edit<br>-e<br>--no-edit|正常な機械的マージをコミットする前にエディターを呼び出して、自動生成されたマージ メッセージをさらに編集し、ユーザーがマージを説明して正当化できるようにします。 --no-edit オプションを使用すると、自動生成されたメッセージを受け入れることができます (これは一般的に推奨されません)。|
|--cleanup=\<mode>|このオプションは、コミット前にマージ メッセージをクリーンアップする方法を決定します。 詳細については、git-commit[1] を参照してください。 さらに、 \<mode> にはさみの値が指定されている場合、マージの競合が発生した場合にコミット機構に渡される前に、はさみが MERGE_MSG に追加されます。|
|--ff-only|分岐したローカル ヒストリがない場合にのみ、新しいヒストリに更新します。 これは、( --rebase=* フラグを介して) 異なる履歴を調整する方法が提供されていない場合のデフォルトです。|
|--ff<br>--no-ff|リベースではなくマージする場合、マージされた履歴がすでに現在の履歴の子孫である場合のマージの処理方法を指定します。 マージが要求された場合、refs/tags/ 階層の本来の場所に格納されていない注釈付き (および場合によっては署名済み) タグをマージしない限り、 --ff がデフォルトです。この場合、 --no-ff が想定されます。|
|-S[\<keyid>]<br>--gpg-sign[=\<keyid>]<br>--no-gpg-sign|結果のマージコミットに GPG 署名します。 keyid 引数はオプションで、デフォルトはコミッター ID です。 指定する場合は、スペースなしでオプションに貼り付ける必要があります。 --no-gpg-sign は、commit.gpgSign 構成変数と以前の --gpg-sign の両方を取り消すのに役立ちます。|
|--log[=\<n>]<br>--no-log|ブランチ名に加えて、マージされている最大 \<n> 個の実際のコミットからの 1 行の説明をログ メッセージに入力します。 git-fmt-merge-msg[1] も参照してください。 マージするときにのみ役立ちます。<br><br>--no-log を使用すると、マージされる実際のコミットからの 1 行の説明を一覧表示しません。|
|--signoff<br>--no-signoff|コミット ログ メッセージの最後に、コミッターによる Signed-off-by トレーラーを追加します。 サインオフの意味は、コミットするプロジェクトによって異なります。 たとえば、コミッターがプロジェクトのライセンスの下で作品を提出する権利を持っていることを証明したり、開発者の原産地証明書などの貢献者の表明に同意したりすることがあります。 (Linux カーネルおよび Git プロジェクトで使用されるものについては、http://developercertificate.org を参照してください。) 貢献しているプロジェクトのドキュメントまたはリーダーシップを調べて、そのプロジェクトでサインオフがどのように使用されているかを理解してください。<br><br>--no-signoff オプションを使用して、コマンド ラインで以前の --signoff オプションを取り消すことができます。|
|--stat<br>-n<br>--no-stat|マージの最後に diffstat を表示します。 diffstat は、構成オプション merge.stat によっても制御されます。<br><br>-n または --no-stat を使用すると、マージの最後に diffstat が表示されません。|
|--squash<br>--no-squash|実際のマージが発生したかのように (マージ情報を除いて) 作業ツリーとインデックスの状態を生成しますが、実際にはコミットを作成したり、HEAD を移動したり、$GIT_DIR/MERGE_HEAD を記録したりしません (次の git commit コマンドで マージコミット)。 これにより、現在のブランチの上に単一のコミットを作成できます。その効果は、別のブランチをマージするのと同じです (タコの場合はそれ以上)。|
|--[no-]verify|デフォルトでは、pre-merge および commit-msg フックが実行されます。 --no-verify が指定されている場合、これらはバイパスされます。 githooksも参照してください。 マージするときにのみ役立ちます。|
|-s \<strategy><br>--strategy=\<strategy>|指定されたマージ戦略を使用します。 試行する順序で指定するために複数回指定できます。 -s オプションがない場合は、組み込みの戦略リストが代わりに使用されます (単一の頭をマージする場合は ort、それ以外の場合は octopus)。|
|-X \<option><br>--strategy-option=\<option>|マージ戦略固有のオプションをマージ戦略に渡します。|
|--verify-signatures<br>--no-verify-signatures|マージされるサイド ブランチのヒント コミットが有効なキー、つまり有効な uid を持つキーで署名されていることを確認します。デフォルトの信頼モデルでは、署名キーが信頼できるキーによって署名されていることを意味します。 サイド ブランチのヒント コミットが有効なキーで署名されていない場合、マージは中止されます。<br><br>マージするときにのみ役立ちます。|
|--summary<br>--no-summary|--stat および --no-stat と同義。 これらは推奨されておらず、将来削除される予定です。|
|--autostash<br>--no-autostash|操作が開始される前に一時的な stash エントリを自動的に作成し、それを特別な参照 MERGE_AUTOSTASH に記録し、操作の終了後に適用します。 これは、ダーティ ワークツリーで操作を実行できることを意味します。 ただし、注意して使用してください。マージが成功した後の最終的な stash アプリケーションは、重要な競合を引き起こす可能性があります。|
|--allow-unrelated-histories|デフォルトでは、git merge コマンドは、共通の祖先を共有しない履歴のマージを拒否します。 このオプションは、独立して開始された 2 つのプロジェクトの履歴をマージするときに、この安全性を無効にするために使用できます。 これは非常にまれなケースであるため、デフォルトでこれを有効にする構成変数は存在せず、追加されません。<br><br>マージするときにのみ役立ちます。|
|-r<br>--rebase[=false\|true\|merges\|interactive]|true の場合、フェッチ後に上流のブランチの上に現在のブランチをリベースします。 アップストリーム ブランチに対応するリモート トラッキング ブランチがあり、アップストリーム ブランチが最後のフェッチ以降にリベースされた場合、リベースはその情報を使用して非ローカル変更のリベースを回避します。<br><br>マージに設定されている場合は、git rebase --rebase-merges を使用してリベースし、ローカル マージ コミットがリベースに含まれるようにします (詳細については、git-rebase を参照してください)。<br><br>false の場合、上流のブランチを現在のブランチにマージします。<br><br>インタラクティブな場合は、rebase のインタラクティブ モードを有効にします。<br><br>git-config の pull.rebase、branch.\<name>.rebase、branch.autoSetupRebase を参照してください。|
|--no-rebase|これは --rebase=false の省略形です。|

## 取得に関するオプション
|オプション|説明|
|:--|:--|
|--all|すべてのリモートを取得します。|
|-a<br>--append|取得した ref の ref 名とオブジェクト名を .git/FETCH_HEAD の既存のコンテンツに追加します。 このオプションがないと、.git/FETCH_HEAD の古いデータが上書きされます。|
|--atomic|アトミック トランザクションを使用して、ローカル参照を更新します。 すべての参照が更新されるか、エラーが発生した場合、参照は更新されません。|
|--depth=\<depth>|各リモート ブランチ履歴の先端から指定された数のコミットにフェッチを制限します。 --depth=\<depth> オプションを使用して git clone によって作成された浅いリポジトリにフェッチする場合 (git-clone を参照)、指定されたコミット数まで履歴を深くするか、短くします。 深化されたコミットのタグは取得されません。|
|--deepen=\<depth>|--depth と同様ですが、各リモート ブランチ履歴の先端からではなく、現在の浅い境界からのコミット数を指定する点が異なります。|
|--shallow-since=\<date>|浅いリポジトリの履歴を深くまたは短くして、\<date> 以降に到達可能なすべてのコミットを含めます。|
|--shallow-exclude=\<revision>|浅いリポジトリの履歴を深くまたは短くして、指定されたリモート ブランチまたはタグから到達可能なコミットを除外します。 このオプションは複数回指定できます。|
|--unshallow|ソース リポジトリが完成したら、浅いリポジトリを完全なリポジトリに変換し、浅いリポジトリによって課されるすべての制限を取り除きます。<br><br>ソース リポジトリが浅い場合は、現在のリポジトリがソース リポジトリと同じ履歴を持つように、可能な限り取得します。|
|--update-shallow|デフォルトでは、浅いリポジトリからフェッチする場合、git fetch は .git/shallow の更新が必要な参照を拒否します。 このオプションは .git/shallow を更新し、そのような参照を受け入れます。|
|--negotiation-tip=\<commit\|glob>|デフォルトでは、Git はすべてのローカル ref から到達可能なコミットをサーバーに報告し、受信するパックファイルのサイズを縮小しようとして、共通のコミットを見つけます。 指定した場合、Git は指定されたヒントから到達可能なコミットのみを報告します。 これは、フェッチされるアップストリーム ref と共通のコミットを持つ可能性が高いローカル ref をユーザーが知っている場合に、フェッチを高速化するのに役立ちます。<br><br>このオプションは複数回指定できます。 その場合、Git は指定されたコミットのいずれかから到達可能なコミットを報告します。<br><br>このオプションの引数は、ref 名のグロブ、ref、またはコミットの (省略されている可能性がある) SHA-1 の場合があります。 グロブを指定することは、このオプションを複数回 (一致する参照名ごとに 1 つずつ) 指定することと同じです。<br><br>git-config[1] に記載されている fetch.negotiationAlgorithm および push.negotiate 構成変数と、以下の --negotiate-only オプションも参照してください。|
|--negotiate-only|サーバーから何も取得せず、代わりに提供された --negotiation-tip=* 引数の祖先を出力します。これはサーバーと共通です。<br><br>これは --recurse-submodules=[yes\|on-demand] と互換性がありません。 内部的には、これは push.negotiate オプションを実装するために使用されます。git-config を参照してください。|
|--dry-run|変更を加えることなく、何が行われるかを示します。|
|-f<br>--force|\<src>:\<dst> refspec で git fetch を使用すると、git-fetch ドキュメントの \<refspec> 部分で説明されているように、ローカル ブランチの更新を拒否する場合があります。 このオプションは、そのチェックをオーバーライドします。|