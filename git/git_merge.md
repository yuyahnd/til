# git-merge - Join two or more development histories together

[Git - git-merge Documentation](https://git-scm.com/docs/git-merge)

## オプション

|オプション|説明|
|:--|:--|
|--commit<br>--no-commit|マージを実行し、結果をコミットします。 このオプションは、-no-commitをオーバーライドするために使用できます。<br><br>--no-commitを使用すると、マージを実行し、マージコミットを作成する直前に停止して、コミットする前にマージ結果を検査し、さらに微調整する機会をユーザーに提供します。<br><br>早送り更新はマージコミットを作成しないため、-no-commitを使用してこれらのマージを停止する方法はないことに注意してください。 したがって、mergeコマンドによってブランチが変更または更新されないようにする場合は、-no-ffと--no-commitを使用します。|
|--edit<br>-e<br>--no-edit|機械的マージを成功させる前にエディターを呼び出して、自動生成されたマージメッセージをさらに編集し、ユーザーがマージについて説明して正当化できるようにします。 --no-editオプションを使用して、自動生成されたメッセージを受け入れることができます（これは一般的に推奨されていません）。 --edit（または-e）オプションは、コマンドラインから-mオプションを使用してドラフトメッセージを表示し、エディターで編集する場合にも役立ちます。<br><br>古いスクリプトは、ユーザーがマージログメッセージを編集できないようにするという過去の動作に依存している可能性があります。 git mergeを実行すると、エディターが開きます。 このようなスクリプトを更新された動作に合わせて調整しやすくするために、環境変数GIT_MERGE_AUTOEDITをスクリプトの先頭でnoに設定できます。|
|--cleanup=\<mode>|このオプションは、コミットする前にマージメッセージをクリーンアップする方法を決定します。 詳細については、git-commitを参照してください。 さらに、\<mode>にはさみの値が指定されている場合、マージの競合が発生した場合、はさみがMERGE_MSGに追加されてから、コミット機構に渡されます。|
|--ff<br>--no-ff<br>--ff-only|マージされた履歴がすでに現在の履歴の子孫である場合に、マージがどのように処理されるかを指定します。 --ffは、refs / tags /階層の自然な場所に格納されていない注釈付き（および場合によっては署名済み）タグをマージしない限り、デフォルトです。この場合、-no-ffが想定されます。<br><br>--ffを使用すると、可能な場合はマージを早送りとして解決します（マージされたブランチに一致するようにブランチポインターを更新するだけです。マージコミットは作成しないでください）。 不可能な場合（マージされた履歴が現在の履歴の子孫でない場合）、マージコミットを作成します。<br><br>--no-ffを使用すると、マージを早送りとして解決できる場合でも、すべての場合にマージコミットを作成します。<br><br>--ff-onlyを使用して、可能な場合はマージを早送りとして解決します。 不可能な場合は、マージを拒否し、ゼロ以外のステータスで終了します。|
|-S[\<keyid>]<br>--gpg-sign[=\<keyid>]<br>--no-gpg-sign|GPG-結果のマージコミットに署名します。 keyid引数はオプションであり、デフォルトはコミッターIDです。 指定する場合は、スペースなしでオプションに固定する必要があります。 --no-gpg-signは、commit.gpgSign構成変数と以前の--gpg-signの両方を打ち消すのに役立ちます。|
|--log[=\<n>]<br>--no-log|ブランチ名に加えて、マージされている最大<n>個の実際のコミットからの1行の説明をログメッセージに入力します。 git-fmt-merge-msg[1]も参照してください。<br><br>--no-logを使用すると、マージされる実際のコミットからの1行の説明が一覧表示されません。|
|--signoff<br>--no-signoff|コミットログメッセージの最後に、コミッターによるサインオフバイトレーラーを追加します。 サインオフの意味は、コミットしているプロジェクトによって異なります。 たとえば、コミッターがプロジェクトのライセンスに基づいて作品を提出する権利を持っていることを証明したり、開発者の原産地証明書などの寄稿者の代表に同意したりする場合があります。 （LinuxカーネルおよびGitプロジェクトで使用されるものについては、http：//developercertificate.orgを参照してください。）プロジェクトでサインオフがどのように使用されるかを理解するには、貢献しているプロジェクトのドキュメントまたはリーダーシップを参照してください。<br><br>--no-signoffオプションを使用すると、コマンドラインで以前の--signoffオプションを無効にすることができます。|
|--stat<br>-n<bt>--no-stat|マージの最後にdiffstatを表示します。 diffstatは、構成オプションmerge.statによっても制御されます。<br><br>-nまたは--no-statを使用すると、マージの最後にdiffstatが表示されません。|
|--squash<br>--no-squash|実際のマージが発生したかのように作業ツリーとインデックスの状態を生成します（マージ情報を除く）が、実際にコミットしたり、HEADを移動したり、$ GIT_DIR / MERGE_HEADを記録したりしないでください（次のgitcommitコマンドで マージコミット）。 これにより、現在のブランチの上に単一のコミットを作成できます。その効果は、別のブランチ（タコの場合はそれ以上）をマージするのと同じです。<br><br>--no-squashを使用してマージを実行し、結果をコミットします。 このオプションは、-squashをオーバーライドするために使用できます。<br><br>--squashを使用すると、-commitは許可されず、失敗します。|
|--[no-]verify|デフォルトでは、pre-merge フックと commit-msg フックが実行されます。 --no-verify を指定すると、これらはバイパスされます。 githooks も参照してください。|
|-s \<strategy><br>--strategy=\<strategy>|指定されたマージ戦略を使用します。 試行する順序で指定するために、複数回指定できます。 -sオプションがない場合は、代わりに組み込みの戦略リストが使用されます（単一のヘッドをマージする場合はort、それ以外の場合はタコ）。|
|-X \<option><br>--strategy-option=\<option>|マージ戦略固有のオプションをマージ戦略に渡します。|
|--verify-signatures<br>--no-verify-signatures|マージされるサイドブランチのチップコミットが有効なキー、つまり有効なuidを持つキーで署名されていることを確認します。デフォルトの信頼モデルでは、これは署名キーが信頼できるキーによって署名されていることを意味します。 サイドブランチのチップコミットが有効なキーで署名されていない場合、マージは中止されます。|
|--summary<br>--no-summary|--statおよび--no-statの同義語。 これらは非推奨であり、将来削除される予定です。|
|-q<br>--quiet|静かに操作してください。 --no-progressを意味します。|
|-v<br>--verbose|冗長になります。|
|--progress<br>--no-progress|進行状況を明示的にオン/オフにします。 どちらも指定されていない場合、標準エラーが端末に接続されていれば進行状況が表示されます。 すべてのマージ戦略が進捗レポートをサポートしているわけではないことに注意してください。|
|--autostash<br>--no-autostash|操作を開始する前に一時的なスタッシュエントリを自動的に作成し、それを特別な参照MERGE_AUTOSTASHに記録して、操作の終了後に適用します。 これは、ダーティワークツリーで操作を実行できることを意味します。 ただし、注意して使用してください。マージが成功した後の最後のstashアプリケーションは、重要な競合を引き起こす可能性があります。|
|--allow-unrelated-histories|デフォルトでは、git mergeコマンドは、共通の祖先を共有しない履歴のマージを拒否します。 このオプションは、独立して生活を始めた2つのプロジェクトの履歴をマージするときにこの安全性を無効にするために使用できます。 これは非常にまれなケースであるため、これをデフォルトで有効にする構成変数は存在せず、追加されません。|
|-m \<msg>|マージコミットに使用するコミットメッセージを設定します（マージコミットが作成された場合）。<br><br>--logが指定されている場合、マージされるコミットのショートログが指定されたメッセージに追加されます。<br><br>git fmt-merge-msgコマンドを使用すると、自動化されたgitマージ呼び出しに適切なデフォルトを設定できます。 自動メッセージには、ブランチの説明を含めることができます。|
|--into-name \<branch>|デフォルトでは、git mergeコマンドは、共通の祖先を共有しない履歴のマージを拒否します。 このオプションは、独立して生活を始めた2つのプロジェクトの履歴をマージするときにこの安全性を無効にするために使用できます。 これは非常にまれなケースであるため、これをデフォルトで有効にする構成変数は存在せず、追加されません。|
|-F \<file>--file=\<file>|マージコミットに使用されるコミットメッセージを読みます（マージコミットが作成された場合）。<br><br>--logが指定されている場合、マージされるコミットのショートログが指定されたメッセージに追加されます。|
|--rerere-autoupdate<br>--no-rerere-autoupdate|可能であれば、rerereメカニズムが自動競合解決の結果でインデックスを更新できるようにします。|