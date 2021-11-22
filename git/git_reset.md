# git-reset - Reset current HEAD to the specified state

[Git - git-reset Documentation](https://git-scm.com/docs/git-reset)

## 説明
最初の3つの形式で、エントリを\<tree-ish>からインデックスにコピーします。
最後の形式で、現在のブランチヘッド（HEAD）を\<commit>に設定し、
オプションでインデックスと作業ツリーを一致するように変更します。 
\<tree-ish> / \<commit>は、すべての形式でデフォルトでHEADになります。

* git reset [-q] [\<tree-ish>] [--] \<pathspec>…​
* git reset [-q] [--pathspec-from-file=\<file> [--pathspec-file-nul]] [\<tree-ish>]  
これらのフォームは、<pathspec>に一致するすべてのパスのインデックスエントリを<tree-ish>の状態にリセットします。 （作業ツリーや現在のブランチには影響しません。）<br><br>これは、git reset <pathspec>がgitadd <pathspec>の反対であることを意味します。 このコマンドは、git restore [--source = <tree-ish>] --staged <pathspec> ...と同等です。
