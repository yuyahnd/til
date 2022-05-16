# git-log - Show commit logs

[Git - git-log Documentation](https://git-scm.com/docs/git-log)

## オプション

|オプション|説明|
|:--|:--|
|--follow|名前の変更を超えてファイルの履歴を一覧表示し続けます（単一のファイルに対してのみ機能します）。|
|--no-decorate<br>--decorate[=short\|full\|auto\|no]|表示されているコミットの参照名を出力します。 shortが指定されている場合、ref名のプレフィックスrefs / heads /、refs / tags /、およびrefs /remotes/は出力されません。 fullを指定すると、完全な参照名（プレフィックスを含む）が出力されます。 autoが指定されている場合、出力が端末に送られる場合、参照名はshortが指定されているかのように表示されます。それ以外の場合、参照名は表示されません。 オプション--decorateは、-decorate=shortの省略形です。 デフォルトはlog.decorateの構成値で、構成されている場合はautoです。|
|--decorate-refs=\<pattern><br>--decorate-refs-exclude=\<pattern>|--decorate-refsが指定されていない場合は、すべてのrefが含まれているように見せかけます。 候補ごとに、-decorate-refs-excludeに指定されたパターンと一致する場合、または--decorate-refsに指定されたパターンのいずれとも一致しない場合は、装飾に使用しないでください。 log.excludeDecoration構成オプションを使用すると、装飾からrefを除外できますが、明示的な--decorate-refsパターンは、log.excludeDecorationの一致をオーバーライドします。|
|--source|各コミットに到達したコマンドラインで指定された参照名を出力します。|
|--[no-]mailmap<br>--[no-]use-mailmap|メールマップファイルを使用して、作成者とコミッターの名前と電子メールアドレスを正規の実名と電子メールアドレスにマップします。 git-shortlog を参照してください。|
|--full-diff|このフラグがない場合、git log -p <path> ...は、指定されたパスに接触するコミットを示し、同じ指定されたパスについて差分を取ります。 これにより、指定されたパスに接触するコミットの完全な差分が表示されます。 これは、「<path>…」がコミットのみを制限し、それらのコミットの差分を制限しないことを意味します。<br><br>これは、すべての差分ベースの出力タイプに影響することに注意してください。 --statなどによって生成されたもの。|
|--log-size|各コミットの出力に「logsize<number>」という行を含めます。ここで、<number>は、そのコミットのメッセージの長さ（バイト単位）です。 事前にスペースを割り当てることができるようにすることで、gitログ出力からログメッセージを読み取るツールを高速化することを目的としています。|
|-L\<start>,\<end>:\<file><br>-L:\<funcname>:\<file>|\<file>内で、\<start>、\<end>、または関数名regex\<funcname>で指定された行範囲の変化をトレースします。 パススペックリミッターを指定することはできません。 これは現在、単一のリビジョンから開始するウォークに制限されています。つまり、ゼロまたは1つの正のリビジョン引数のみを指定でき、開始リビジョンには\<start>と\<end>（または\<funcname>）が存在する必要があります。 このオプションは複数回指定できます。 --patchを意味します。 パッチ出力は--no-patchを使用して抑制できますが、他のdiff形式（つまり、-raw、-numstat、-shortstat、-dirstat、-summary、-name-only、-name-status、 --check）は現在実装されていません。|
|\<revision-range>|指定されたリビジョン範囲のコミットのみを表示します。 <revision-range>が指定されていない場合、デフォルトでHEAD（つまり、現在のコミットにつながる履歴全体）になります。 origin..HEADは、現在のコミット（つまり、HEAD）から到達可能なすべてのコミットを指定しますが、originからは到達できません。 <revision-range>のスペルの完全なリストについては、gitrevisions の「範囲の指定」セクションを参照してください。|
