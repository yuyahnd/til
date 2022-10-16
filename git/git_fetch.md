# git-fetch - Download objects and refs from another repository

[Git - git-fetch Documentation](https://git-scm.com/docs/git-fetch)

## オプション

|オプション|説明|
|:--|:--|
|--all|すべてのリモートを取得します。|
|-a<br>--append|取得した ref の ref 名とオブジェクト名を .git/FETCH_HEAD の既存のコンテンツに追加します。 このオプションがないと、.git/FETCH_HEAD の古いデータが上書きされます。|
|--atomic|アトミック トランザクションを使用して、ローカル参照を更新します。 すべての参照が更新されるか、エラーが発生した場合、参照は更新されません。|
|--depth=\<depth>|各リモート ブランチ履歴の先端から指定された数のコミットにフェッチを制限します。 --depth=\<depth> オプションを使用して git clone によって作成された浅いリポジトリにフェッチする場合 (git-clone[1] を参照)、指定されたコミット数まで履歴を深くするか、短くします。 深化されたコミットのタグは取得されません。|
