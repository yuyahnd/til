# gitattributes 
gitattributes - Defining attributes per path

# SYNOPSIS
 $GIT_DIR/info/attributes, .gitattributes

# DESCRIPTION
gitattributesファイルは、パス名に属性を割り当てる単純なテキストファイルです。
gitattributes ファイルの各行は、次の形式になっています。

```
pattern attr1 attr2 ...
```

つまり、パターンと属性リストを空白で区切った形式です。行頭や行末の空白は無視されます。# で始まる行は無視されます。二重引用符で始まるパターンは、C言語形式で引用符付きとして扱われます。パターンが対象のパスに一致する場合、その行に記載された属性がそのパスに適用されます。
