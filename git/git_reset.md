# git-reset - Reset current HEAD to the specified state

[Git - git-reset Documentation](https://git-scm.com/docs/git-reset)

## 説明
最初の3つの形式で、エントリを\<tree-ish>からインデックスにコピーします。
最後の形式で、現在のブランチヘッド（HEAD）を\<commit>に設定し、
オプションでインデックスと作業ツリーを一致するように変更します。 
\<tree-ish> / \<commit>は、すべての形式でデフォルトでHEADになります。

* git reset [-q] [\<tree-ish>] [--] \<pathspec>…​
* git reset [-q] [--pathspec-from-file=\<file> [--pathspec-file-nul]] [\<tree-ish>]
