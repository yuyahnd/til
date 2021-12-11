# git-rm - Remove files from the working tree and from the index

[Git - git-rm Documentation](https://git-scm.com/docs/git-rm)

## オプション

|オプション|説明|
|:--|:--|
|\<pathspec>…​|削除するファイル。 先頭のディレクトリ名（たとえば、dir / file1およびdir / file2を削除するdir）を指定して、ディレクトリ内のすべてのファイル、および再帰的にすべてのサブディレクトリを削除できますが、これには-rオプションを明示的に指定する必要があります。<br><br>このコマンドは、Gitに認識されているパスのみを削除します。<br><br>ファイルグロブはディレクトリの境界を越えて一致します。 したがって、2つのディレクトリdとd2が与えられた場合、前者はディレクトリd2もすべて削除するため、git rm'd * 'とgitrm'd / *'の使用には違いがあります。<br><br>詳細については、gitglossary [7]のpathspecエントリを参照してください。|
