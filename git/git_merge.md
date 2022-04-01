# git-merge - Join two or more development histories together

[Git - git-merge Documentation](https://git-scm.com/docs/git-merge)

## オプション

|オプション|説明|
|:--|:--|
|--commit<br>--no-commit|マージを実行し、結果をコミットします。 このオプションは、-no-commitをオーバーライドするために使用できます。<br><br>--no-commitを使用すると、マージを実行し、マージコミットを作成する直前に停止して、コミットする前にマージ結果を検査し、さらに微調整する機会をユーザーに提供します。<br><br>早送り更新はマージコミットを作成しないため、-no-commitを使用してこれらのマージを停止する方法はないことに注意してください。 したがって、mergeコマンドによってブランチが変更または更新されないようにする場合は、-no-ffと--no-commitを使用します。|
