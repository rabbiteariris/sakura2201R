サクラエディタ 改良版  

<br>

**Introduction**  

Sublime Text や Atom を参考にモダンな感じにしているつもりです.  
方針としては改造ではなく改良になるような修正を心がけています.  
また, 修正があまり意味のないものだった場合は削除するようにしています.  

また、MacTypeと併用していて画面崩れがひどかったので対応をしています.  
高速にスクロールとかすると前の描画が残ってしまって見苦しい状態になることが多かったので, 同じような状態に陥っている人には効果があるかもしれません.  
サクラエディタのソースが初見殺しな感じでカオスなので一時しのぎな対応ですが…  


<br>

**Download**  

変更内容はコミットログを参照してください.  
細かい内容は [my_config.h](https://github.com/mimix33/sakura_2201/raw/master/sakura_core/my_config.h) を見るとわかるかと思います.  

+ [sakura-mix-2.19-x64.zip](http://mimix.sakura.ne.jp/release/sakura-mix-2.19-x64.zip) (1.08MB)  

動作には[Visual Studio 2017 Microsoft Visual C++ 再頒布可能パッケージ](https://www.visualstudio.com/ja/downloads/#other-ja)が必要です.  

<br>

**Setup**  

ダウンロードしたファイルをすでに使用しているサクラエディタに上書きコピーしてください.  
`sakura.default.ini`と`sakura.keywordset.json`は実行ファイルと同じ場所に置き, 実行ファイル名が違う場合は`sakura`の部分を変更してください.  

+ [sakura.default.ini](https://github.com/mimix33/sakura_2201/raw/master/resource/sakura.default.ini)  
  デフォルト設定値を設定してあるファイルです. ここに初期値を設定することで常にその状態で起動します.  
  ここで設定した値のままの場合は`sakura.ini`には出力されなくなります.  

+ [sakura.keywordset.json](https://github.com/mimix33/sakura_2201/raw/master/resource/sakura.keywordset.json)  
  強調キーワードのセットリストです. セット名, 大文字小文字の区別, ファイル名を指定します.  
  共通設定からの強調キーワード設定は可能ですが保存はされなくなりますので注意が必要です. 必要に応じてエクスポートしてください.  
  また, `sakura.ini`には出力されなくなります.  

+ 最新のキーワードセットはこちら [keyword_pack.zip](https://github.com/mimix33/sakura_2201/raw/master/doc/keyword_pack.zip) (355KB)  

<br>

**Build environment**  
+ 2.2.0.1をベースに[リポジトリ](http://svn.code.sf.net/p/sakura-editor/code/sakura/trunk2)の追っかけ. ベースリビジョンからのマージ情報は[こちら](https://github.com/mimix33/sakura_2201/raw/master/doc/changes_from_r4011.txt). あと、[パッチ](https://sourceforge.net/p/sakura-editor/patchunicode/)のマージ  
+ MSVC2017でビルド  
+ Boostを使用 (各種コンテナ, 正規表現)  
+ Luaを使用 (マクロ)  
+ 挙動の制御 (共有フラグ)としてレジストリを使用しています  

<br>

**Changed**  
+ ファイル系  

|改良版|本家|
|-|-|
|履歴を別ファイル (`sakura.recent.json`)に出力|`sakura.ini`に出力|
|起動時に存在しないファイル・フォルダ履歴を削除する||
|デフォルト設定ファイル (`sakura.default.ini`)の使用||
|強調キーワード設定は `sakura.keywordset.json`から読み込む<br>(共通設定からの設定不可)|初期化時は内蔵キーワードをインポート, 以後`sakura.ini`に出力|
|カラー設定のインポートはカラー情報だけを適用させる|表示, カラー, 装飾情報を適用|
|マクロに使用できる言語に `Lua`を追加||
|履歴 (検索, 置換, Grep)の値を少なめに変更<br>検索キー: `16`<br>置換キー: `16`<br>Grepファイル: `16`<br>Grepフォルダ: `16`|検索キー: `30`<br>置換キー: `30`<br>Grepファイル: `30`<br>Grepフォルダ: `30`|
|多重オープンの許可 (Shiftを押しながらファイルのドロップ)|１つのみ|

+ 表示系  

|改良版|本家|
|-|-|
|EOFのみの行 (起動時とか)にも行番号を表示|表示なし|
|行を中央揃えにする (行の間隔を上下に配分)|上揃え|
|半角空白文字を `･`で描画, NBSPも半角空白として `×`で表示|`o`の下半分を表示, NBSPは表示されない|
|タブ文字を線のみで描画 (Sublime Textみたいな)|矢印, または任意の文字|
|コメント行の背景カラーを改行以降もその色で描画|改行まで|
|空白, タブ, 改行, EOFのカラーは現在のテキストカラーから自動で設定|個々にカラー設定|
|選択範囲カラーは元のテキストカラーをそのまま使用する (Text:0%, Back:100%)|選択範囲カラーとブレンドされる|
|太字装飾の文字列を選択したときに選択範囲カラーの装飾の影響を受けないように修正|選択範囲カラー設定が使用される|
|カーソル行アンダーラインを行番号から引っ張る|入力エリアのみ|

+ 操作, 編集系  

|改良版|本家|
|-|-|
|ミニマップの表示, 操作性を改良 (Sublime Textを模倣)||
|ミニマップに検索文字列, ブックマークのある行を設定した背景色で塗りつぶし|表示なし|
|垂直, 水平スクロールの挙動をメモ帳の挙動と同じにする<br>垂直マージン1行, 水平マージン1, 16文字移動|垂直マージン3行, 水平マージン1, 1文字移動|
|検索, ジャンプなどのカーソルが大きく移動する処理ではジャンプ先のカーソル行をセンタリングする|最近接ジャンプなので画面端にくることが多い|
|タブ入力文字の切り替え機能 (`S_ChangeTabWidth`マクロを修正, 負の値を設定するとタブと空白を相互に切り替えます)|できない|

+ UI系  

|改良版|本家|
|-|-|
|タブと編集ウィンドウのバグ修正とスタイル調整 (モダンに?)|メニュー下に境界線や編集画面に枠がある|
|リソース (ダイアログ)のフォントを `9, "MS Shell Dlg"`へ変更|`9, "ＭＳ Ｐゴシック"`|
|変更, キーマクロ記録中にタブ名のカラーを変更||
|タブをダブルクリックで閉じられるようにする||
|選択タブのアクティブ化をマウス押下時に行いレスポンス向上|マウス押上時にアクティブになる|
|Grepフォルダの指定を物理的に4つに増やす|１つ|
|Grep「現在編集中のファイルから検索」をチェックした時の状態を保持しないようにする|保持される|
|置換ダイアログの置換後テキストに置換前テキストを設定|前回のテキスト|
|正規表現検索のときに正規表現記号をクォート (`^abc$`を検索する場合 `\^abc\$`にする)||
|アウトライン解析ダイアログのドッキング時はコントロールカラーのままにする|背景カラーが使用される|
|ステータスバーのカスタマイズ<br>・カーソル移動時のちらつき抑制<br>・表示情報の内容を修正<br>・左クリックでメニューを表示||
|タグファイル作成時にフォルダの初期位置を `tags`, `ctags.cnf`ファイルがあるところまで辿る|カレントフォルダ|
|ダイレクトジャンプ一覧の表示カラムを選別||
|メインメニューは常にデフォルトを使用する|カスタマイズ可能|

<br>

**Bugfix**  
+ 検索マーク切り替え, インクリメンタルサーチの際に検索ダイアログの「正規表現」が影響を受けないように  
  \- 常時、正規表現で検索しているとコレ結構ストレスたまります  

+ ルールファイルを設定してアウトライン解析をするとデフォルトが逆順になっている  

+ ミニマップ上をクリックしたときにフォーカスを移さずに入力に支障が出ないようにする  

+ 行番号縦線を行番号の色で描画する  
  \- 行番号縦線はその行に変更があった場合, その行だけ変更色で縦線が引かれてしまうので区切りの線としては微妙だったため  

+ 行番号が非表示でブックマークが表示のときブックマークは線で描画する  
  \- 行番号非表示時のブックマーク表示がなかったのでブックマークのカラー設定を無効にしている時と同じように表示する  

<br>


(C) 2017 mimix.
