# SDSメニュータブ

リボンメニューの **SDS** タブからは、SDSの一般的な機能にアクセスできます。

![SDS Tab](_images/ui_sdstab.png)

## Create

> [!TIP]
> 新しいSUPPOの名前は、ZONE内にある既存のSUPPO要素の命名規則に基づいて自動的に割り当てられます。

### Preliminary

ピックした配管コンポーネントに仮（preliminary）のアンシラリーを取り付けた新しいSUPPO要素を作成します。ピックした配管コンポーネントが VOLM 要素のボリューム内にある場合、SUPPOは、その VOLM 名から `/VOLM` 接尾辞を削除した名前の ZONE の下に作成されます。

### Ancillary

ピックした配管コンポーネントにアンシラリーを取り付けた新しいSUPPO要素を作成します。ピックした配管コンポーネントが VOLM 要素のボリューム内にある場合、SUPPOは、その VOLM 名から `/VOLM` 接尾辞を削除した名前の ZONE の下に作成されます。

### Empty Support

SUPPO要素のみを新規作成します。SUPPOは、purpose が `SUPP` または `SDS` の現在のZONE要素の下に作成されます。

## Modify

### Modify Support

現在のSUPPO要素に対する[サポートエディタフォーム](sdsedit.md)を開きます。

## Delete

### Delete Support

現在のSUPPO要素を削除します。

## Tools

### Sort Supports

現在のZONE要素の下にあるSUPPO要素を名前でソートします。

### Draw

[図面生成フォーム](sdsdraw.md)を開きます。

### Load Master

マスターデータ（カタログ、図面テンプレートなど）を現在のDBにロードします。詳細については、設定ファイルの [datalDefs](settings.md#dataldefs) を参照してください。

### Generate Spec

purpose が `SDS` の CATE 要素の下にある SCOM 要素から、アンシラリー SPEC 要素の下に SPCO 要素を作成または更新します。また、purpose が `SDS` の STCA 要素の下にある JOIN 要素から、ジョイント SPEC 要素の下に SPCO 要素を作成または更新します。

### Reload Settings

`sds_settings.json` ファイルを再ロードし、SDSを再初期化します。

> [!TIP]
> ファイルの読み込み時に JSON の解析エラーが発生した場合、そのエラーは Command Window に表示されます。

## Help

### Open Docs

ドキュメントを開きます。
