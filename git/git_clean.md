# git clean

git-clean - Remove untracked files from the working tree

# SYNOPSIS

```
git clean [-d] [-f] [-i] [-n] [-q] [-e <pattern>] [-x | -X] [--] [<pathspec>…​]
```

# 説明

現在のディレクトリから始めて、バージョン管理下にないファイルを再帰的に削除して、作業ツリーをクリーンアップします。

通常、Git に不明なファイルのみが削除されますが、-x オプションが指定されている場合は、無視されるファイルも削除されます。これは、たとえば、すべてのビルド製品を削除する場合に役立ちます。
オプションの <pathspec>... 引数が指定されている場合は、pathspec に一致するパスのみが影響を受けます。

# OPTIONS
