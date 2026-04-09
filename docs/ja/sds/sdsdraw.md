# 図面生成フォーム

**SDS Draw** フォームは、サポート詳細図面を生成します。

![SDS Draw](_images/ui_sdsdraw_form.png)

## コンテキストメニュー

リスト上で右クリックするとコンテキストメニューが開きます。

![Context Menu](_images/ui_sdsdraw_context_menu.png)

### Open

選択した図面を開きます。

### Update

図面オプションファイル（Draw Option File）の[drawProcedures](drawopt.md#drawprocedures)にリストされたコマンドを実行して、選択した図面を更新（または生成）します。

### Regenerate

図面が既に存在する場合は最初にそれを削除し、選択した図面を再生成します。

### Publish as PDF

選択した図面を、設定ファイル（Configuration File）の[drawPublishPath](settings.md#drawpublishpath)で指定されたフォルダにPDFファイルとしてエクスポートします。

### Publish as DWG

選択した図面を、設定ファイル（Configuration File）の[drawPublishPath](settings.md#drawpublishpath)で指定されたフォルダにDWGファイルとしてエクスポートします。

### Publish MTO

選択したサポートのMTO（材料集計）テーブルをCSVファイルとして、設定ファイルの[drawPublishPath](settings.md#drawpublishpath)で指定されたフォルダにエクスポートします。

### Activate

選択した行の **Active** チェックボックスをオンにします。

### Deactivate

選択した行の **Active** チェックボックスをオフにします。

### Delete

選択した行を削除します。

## File

![File](_images/ui_sdsdraw_file_menu.png)

### Import

Excel（.xlsx）ファイルからリストにデータをインポートします。

### Export

リストをExcel（.xlsx）ファイルにエクスポートします。

### Open Publish Path

設定ファイル（Configuration File）の[drawPublishPath](settings.md#drawpublishpath)で指定されたフォルダを開きます。

### Quit

フォームを閉じます。

## Edit

![Edit](_images/ui_sdsdraw_edit_menu.png)

### Add Supports from CE & Below

CE配下のすべてのSUPPO要素を行として追加します。

### Add All Supports in MDB

現在のMDB内のすべてのSUPPO要素を行として追加します。

### Delete Invalid Ref Supports

**Support** 列に無効なリファレンスを持つすべての行を削除します。

### Refresh

リストを更新します。

## Run

![Run](_images/ui_sdsdraw_run_menu.png)

### Batch Update Drawings

リストの **Active** チェックボックスがオンになっているすべての図面を更新します。エラーが発生した場合でも、残りの図面の処理を続行します。

### Regenerate (Toggle)

オンにすると、バッチ更新中に既存の図面を削除してから更新します。

### Savework When Each Update (Toggle)

オンにすると、バッチ更新中の各図面の更新後に自動的にSaveworkを行います。
