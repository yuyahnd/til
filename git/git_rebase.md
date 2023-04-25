# git-rebase - Reapply commits on top of another base tip

[Git - git-rebase Documentation](https://git-scm.com/docs/git-rebase)

## オプション

* --onto \<newbase> 
    新しいコミットを作成する開始点。 --onto オプションが指定されていない場合、開始点は <upstream> です。 既存のブランチ名だけでなく、任意の有効なコミットである可能性があります。<br><br>特殊なケースとして、マージ ベースが 1 つしかない場合、A と B のマージ ベースのショートカットとして "A...B" を使用できます。 A と B のいずれかを省略できます。省略した場合、デフォルトで HEAD になります。
* --keep-base
    \<upstream> と \<branch> のマージ ベースに新しいコミットを作成する開始点を設定します。 git rebase --keep-base \<upstream> \<branch> を実行することは、 git rebase --reapply-cherry-picks --no-fork-point --onto \<upstream>...\<branch> \<upstream> < を実行することと同等です<br><br>このオプションは、アップストリーム ブランチ上で機能を開発している場合に役立ちます。 機能の作業中は、上流のブランチが前進する可能性があり、上流の上でリベースを続けるのは最善の考えではなく、ベース コミットをそのままにしておくのが最善の方法ではない可能性があります。 基本コミットは変更されていないため、このオプションは --reapply-cherry-picks を意味し、コミットが失われないようにします。<br><br>このオプションと --fork-point の両方が \<upstream> と \<branch> の間のマージ ベースを見つけますが、このオプションは新しいコミットが作成される開始点としてマージ ベースを使用しますが、 --fork-point はマージを使用します。 base を使用して、リベースされるコミットのセットを決定します。<br><br>以下の INCOMPATIBLE OPTIONS も参照してください。
* \<upstream>
    比較する上流ブランチ。 既存のブランチ名だけでなく、任意の有効なコミットである可能性があります。 デフォルトは、現在のブランチ用に構成されたアップストリームです。
