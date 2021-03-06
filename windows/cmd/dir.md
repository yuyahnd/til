# dir

フォルダ内のファイルやサブフォルダを表示

## 書式

```
dir [ファイル名] [オプション]
```

## オプション

|オプション|説明|
|:--|:--|
|ファイル名[...]|内容を表示するドライブ、フォルダ名、ファイル名を１つ以上指定する。フォルダ名とファイル名には、ワイルドカード「*」「?」を使用できる|
|/a[[:]属性リスト]|属性リストを指定しない場合、すべてのファイルを抽出する。|
|/b|名前のみを表示する。/wスイッチは無効になる。|
|/c|ファイルサイズを桁区切り表示する|
|/-c|ファイルサイズを桁区切り表示しない|
|/d|名前を縦方向に整列して一覧表示する|
|/l|名前をすべて小文字で表示する|
|/n|長い名前を右端に表示する|
|/o[[:]整列項目]|指定した項目で名前を整列して表示する。/o スイッチとソート順の間にコロンを挟んでも省略してもよい。|
|/p|１画面ごとに画面を停止する|
|/q|ファイルやフォルダの所有者を表示する。|
|/r|NTFSファイルシステムで、ファイルの代替データストリーム名とサイズを表示する|
|/s|指定したフォルダをすべてのサブフォルダにある、条件に一致するファイルとフォルダを表示する|
|/f[[:]タイムフィールド]|表示または整列に仕様する日時フィールドを指定する。|
|/w|名前を横方向に整列して一覧表示する。|
|/x|長い名前の左に8.3形式の短い名前を表示する|
|/4|西暦年を4桁の数字で表示する|
|-(ハイフン)|ハイフンは[/-c]のように他のスイッチと併用して、そのスイッチの動作を否定する|


## 属性リスト

|属性|説明|
|:--|:--|
|D|フォルダ（ディレクトリ）|
|R|読み取り専用|
|H|隠しファイル|
|A|アーカイブ（未バックアップ）|
|S|ファイルシステム|
|I|非インデックス対象ファイル|
|L|再解析ポイント|
|- 属性|その属性以外|

## 整列

|整列項目|説明|
|:--|:--|
|N|名前順(アルファベット昇順)|
|S|サイズ順(昇順)|
|E|拡張子順(アルファベット昇順)|
|D|日時順(古い方から)|
|G|グループ（ディレクトリから）|
