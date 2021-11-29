# git-reset - Reset current HEAD to the specified state

[Git - git-reset Documentation](https://git-scm.com/docs/git-reset)

## 説明
最初の3つの形式で、エントリを\<tree-ish>からインデックスにコピーします。
最後の形式で、現在のブランチヘッド（HEAD）を\<commit>に設定し、
オプションでインデックスと作業ツリーを一致するように変更します。 
\<tree-ish> / \<commit>は、すべての形式でデフォルトでHEADになります。

* git reset [-q] [\<tree-ish>] [--] \<pathspec>…​
* git reset [-q] [--pathspec-from-file=\<file> [--pathspec-file-nul]] [\<tree-ish>]  
これらのフォームは、\<pathspec>に一致するすべてのパスのインデックスエントリを\<tree-ish>の状態にリセットします。 （作業ツリーや現在のブランチには影響しません。）<br><br>これは、git reset \<pathspec>がgitadd \<pathspec>の反対であることを意味します。 このコマンドは、git restore [--source = \<tree-ish>] --staged \<pathspec> ...と同等です。<br>git reset \<pathspec>を実行してインデックスエントリを更新した後、git-restore を使用して、インデックスの内容を作業ツリーにチェックアウトできます。 または、git-restore を使用し、-sourceを使用してコミットを指定すると、コミットからのパスの内容をインデックスと作業ツリーに一度にコピーできます。

* git reset (--patch | -p) [\<tree-ish>] [--] [\<pathspec>…​]  
インデックスと\<tree-ish>（デフォルトはHEAD）の違いでハンクをインタラクティブに選択します。 選択したハンクは、インデックスとは逆に適用されます。<br><br>これは、git reset-pがgitadd -pの反対であることを意味します。つまり、これを使用してハンクを選択的にリセットできます。 --patchモードの操作方法については、git-add の「インタラクティブモード」セクションを参照してください。

* git reset [\<mode>] [\<commit>]  
このフォームは、現在のブランチヘッドを\<commit>にリセットし、\<mode>に応じて、インデックス（\<commit>のツリーにリセット）と作業ツリーを更新する可能性があります。 \<mode>を省略すると、デフォルトで--mixedになります。 \<mode>は、次のいずれかである必要があります。

  * --soft  
  インデックスファイルまたは作業ツリーにはまったく触れません（ただし、すべてのモードと同様に、ヘッドを\<commit>にリセットします）。 これにより、git statusが示すように、変更されたすべてのファイルが「変更がコミットされます」のままになります。
  * --mixed  
インデックスをリセットしますが、作業ツリーはリセットしません（つまり、変更されたファイルは保持されますが、コミットのマークは付けられません）。更新されていないものを報告します。 これがデフォルトのアクションです。<br><br>-Nが指定されている場合、削除されたパスは追加する意図としてマークされます（git-add を参照）。  
