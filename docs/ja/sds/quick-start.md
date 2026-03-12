# クイックスタート

## サポートのモデリング

### サポート用ZONEの作成

まず、SUPPO要素を保存するために、purposeが`SUPP`に設定されたZONEを少なくとも1つ作成する必要があります。ZONEを作成するには、以下の手順に従います：

1. **General** タブで、**Zone** をクリックします。

   ![Create ZONE](_images/start_create_zone.png)

2. ZONEの名前を入力し、purposeを`SUPP`に設定してから、**OK** をクリックします。

   ![Create ZONE Form](_images/start_create_zone_form.png)

### アンシラリー付きの新規サポート作成

![Create SUPPO](_images/start_create_suppo.gif)

新規のSUPPO要素を作成するには、以下の手順に従います：

1. **SDS** タブで、**Ancillary** をクリックします。
2. 開いたダイアログでアンシラリータイプを選択し、**OK** をクリックします。

> [!TIP]
> E3D Designの起動後、初めてSDSの機能を使用する際は、SDSの読み込みに時間がかかります。

### サポートフレームワークの作成

![Create Framework](_images/start_create_frmw.gif)

サポートフレームワークを作成するには、以下の手順に従います：

1. **SDS Support Editor** フォームで、![Add Framework](_images/ui_add_framework.png ":no-zoom") **Add Framework** をクリックします。
2. グラフィカルビューで、サポートを固定する位置をピックします。
3. 開いたダイアログでフレームワークのタイプを選択し、**OK** をクリックします。

## サポートの図面化

### REGI & LIBYの作成

サポート図面用のDRWG要素と詳細ビュー用のOVER要素を保存するために、REGI要素とLIBY要素を作成します。以下の手順に従います：

1. **Draw** モジュールを開くか、**Draw functionality in Model** を有効にして **Design** モジュールを開きます。

   > [!TIP]
   > **Draw functionality in Model** の詳細については、AVEVA Documentationの[記事](https://docs.aveva.com/bundle/e3d-design/page/1048435.html)を参照してください。

2. **Home** または **Draw** タブで、**Open** をクリックします。

   ![Open](_images/start_open_draw.png)

3. DEPTを選択し、右クリックメニューからREGI要素とLIBY要素を作成します。

   ![Create REGI & LIBY](_images/start_create_regi_liby.png)

### サポート図面の生成

![Generate Drawings](_images/start_generate_draw.gif)

サポートモデルからサポート図面を生成するには、以下の手順に従います：

1. **SDS** タブで、**Draw** をクリックします。
2. フォームメニューで、**Edit** > **Add All Supports in MDB** をクリックします。
3. リストで、**REGI** 列にREGI名を、**LIBY** 列にLIBY名を入力します。
4. フォームメニューで、**Run** > **Batch Update Drawings** をクリックします。
5. 確認ダイアログで、**Yes** をクリックします。
6. 図面が正常に生成されたことを確認します。
