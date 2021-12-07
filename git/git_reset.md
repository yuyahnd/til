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

  * --hard  
  インデックスと作業ツリーをリセットします。 \<commit>以降の作業ツリー内の追跡ファイルへの変更はすべて破棄されます。 追跡されたファイルを書き込む方法で追跡されていないファイルまたはディレクトリは、単に削除されます。

  * --merg  
  インデックスをリセットし、\<commit>とHEADの間で異なる作業ツリー内のファイルを更新しますが、インデックスと作業ツリー間で異なるファイル（つまり、変更が追加されていないファイル）は保持します。 \<commit>とインデックスの間で異なるファイルにステージングされていない変更がある場合、リセットは中止されます。<br><br>つまり、-mergeはgit read-tree -u -m \<commit>のようなことをしますが、マージされていないインデックスエントリを繰り越します。
  
  * --keep  
  インデックスエントリをリセットし、\<commit>とHEADで異なる作業ツリー内のファイルを更新します。 \<commit>とHEADで異なるファイルにローカル変更がある場合、リセットは中止されます。

  * --[no-]recurse-submodules  
  作業ツリーが更新されると、-recurse-submodulesを使用すると、スーパープロジェクトに記録されたコミットに従ってすべてのアクティブなサブモジュールの作業ツリーが再帰的にリセットされ、そのコミット時にサブモジュールのHEADが切り離されるように設定されます。

## オプション

|オプション|説明|
|:--|:--|
|-q<br>--quiet<br>--no-quiet|静かにして、エラーのみを報告してください。 デフォルトの動作は、reset.quietconfigオプションによって設定されます。 --quietおよび--no-quietは、デフォルトの動作をオーバーライドします。|
|--pathspec-from-file=\<file>|Pathspecは、コマンドライン引数の代わりに\<file>で渡されます。 \<file>が正確に-の場合、標準入力が使用されます。 Pathspec要素は、LFまたはCR / LFで区切られます。 Pathspec要素は、構成変数core.quotePathで説明されているように引用できます（git-config を参照）。 --pathspec-file-nulおよびglobal--literal-pathspecsも参照してください。|
|--pathspec-file-nul|--pathspec-from-fileでのみ意味があります。 Pathspec要素はNUL文字で区切られ、他のすべての文字は文字通りに解釈されます（改行と引用符を含む）。|
