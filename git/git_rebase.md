# git-rebase - Reapply commits on top of another base tip

[Git - git-rebase Documentation](https://git-scm.com/docs/git-rebase)

## オプション

* --onto \<newbase> 
    新しいコミットを作成する開始点。 --onto オプションが指定されていない場合、開始点は <upstream> です。 既存のブランチ名だけでなく、任意の有効なコミットである可能性があります。<br><br>特殊なケースとして、マージ ベースが 1 つしかない場合、A と B のマージ ベースのショートカットとして "A...B" を使用できます。 A と B のいずれかを省略できます。省略した場合、デフォルトで HEAD になります。
