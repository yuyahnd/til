# git-cherry-pick - Apply the changes introduced by some existing commits

[Git - cherry-pick Documentation](https://git-scm.com/docs/git-cherry-pick)

## オプション

|オプション|説明|
|:--|:--|
|\<commit>…​|チェリーピックにコミットします。 コミットを綴る方法のより完全なリストについては、gitrevisions を参照してください。 --no-walk オプションが指定されたかのように、一連のコミットを渡すことができますが、トラバーサルはデフォルトで行われません。git-rev-list を参照してください。 範囲を指定すると、すべての \<commit>… 引数が 1 つのリビジョン ウォークに送られることに注意してください (maint master..next を使用する後の例を参照してください)。|
|-e<br>--edit|このオプションを使用すると、コミットする前に git cherry-pick でコミット メッセージを編集できます。|
