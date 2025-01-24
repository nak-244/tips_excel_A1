# 概要
Excelファイルをやり取りする際は「カーソルをA1セルに合わせる」というお作法があるそうです。  
  
たくさんシートがあるときにいちいち確認するのが面倒なので、自動でできるようにマクロをクイックアクセスツールバーに登録しています。  
同じような内容の記事は多くあると思いますが、次の現場に移動した際自分ですぐ使えるようにメモしておきたいと思います。  

# マクロの内容
- カーソルと表示位置をA1に合わせる
- 表示の倍率を100％に合わせる（目が悪くてよく拡大するので）
- マクロが実行し終わったら１枚目のシートに移動してメッセージを出す

## 手順
### 1. 個人用マクロブックにマクロを保存
個人用マクロブックにマクロを保存するとどのExcelファイルでも使用できます。

#### (1)個人用マクロブックを表示させる
開発者タブ->マクロの記録
マクロの保存先を個人用マクロブックに指定し、何もせずにOKボタンを押す

#### (2)開発者タブ->VisualBasic
先ほど作成した個人用マクロブックのモジュールに以下を貼り付けて保存する
```
Sub Cursor_A1()

' 画面更新をさせない（チカチカするため）
Application.ScreenUpdating = False

Dim ws As Worksheet
' 各シートを順番に見ていく
For Each ws In Worksheets
' カーソルをA1に移動
ws.Select
Range("A1").Select
' 表示位置を左上端に移動
ActiveWindow.ScrollColumn = 1
ActiveWindow.ScrollRow = 1
' 表示倍率を１００％に戻す
ActiveWindow.Zoom = 100
Next ws

' １枚目のシートに移動
Sheets(1).Select
'画面更新を再開させておく
Application.ScreenUpdating = True
' メッセージを表示
MsgBox "処理が完了しました"

End Sub
```


### 2. クイックアクセスツールバーに登録
Excel -> 環境設定 -> リボンとツールバー -> クイックアクセスツールバー  
コマンドの選択で[マクロ]を選択  
先ほど作成したマクロを登録  
