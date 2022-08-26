# git-tag - Create, list, delete or verify a tag object signed with GPG

[Git - git-tag Documentation](https://git-scm.com/docs/git-tag)


## オプション

|オプション|説明|
|:--|:--|
|-a<br>--annotate|署名なしの注釈付きタグ オブジェクトを作成する|
|-s<br>--sign|デフォルトの電子メール アドレスのキーを使用して、GPG 署名付きタグを作成します。 タグ GPG 署名のデフォルトの動作は、tag.gpgSign 構成変数が存在する場合はそれによって制御され、存在しない場合は無効になります。 git-config を参照してください。|
|--no-sign|すべてのタグを強制的に署名するように設定されている tag.gpgSign 構成変数をオーバーライドします。|
|-u \<keyid><br>--local-user=\<keyid>|指定されたキーを使用して、GPG 署名付きタグを作成します。|
|-f<br>--force|既存のタグを指定された名前に置き換えます (失敗する代わりに)|
|-d<br>--delete|指定された名前の既存のタグを削除します。|
