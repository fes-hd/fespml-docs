# 初期セットアップ

## 必須条件

サンプルデータは、AVEVA **ACP** プロジェクトのデータベースに含まれる鋼構造カタログ、仕様、プロパティ、および MDS 辞書データを使用します。サンプルデータを利用するには、次のデータベースをプロジェクトに含めてください：

| Name                     | DB No. | Description                                                |
| ------------------------ | -----: | ---------------------------------------------------------- |
| MASTER/MDSDICT           |   7323 | AVEVA Master Multi-Discipline Supports Dictionary database |
| MASTER/STL_PROFILE_CATA  | 250700 | AVEVA Master Steelwork Profile Catalogue database          |
| MASTER/STL_PROFILE_SPECS | 250701 | AVEVA Master Steelwork Profile Specifications database     |
| MASTER/STL_PROP          | 251709 | AVEVA E3D Structural Design Property database              |

## サンプルカタログの準備

プロジェクト用にサンプルカタログを準備するには、以下の手順に従います：

1. **Paragon** モジュールを開きます。

2. サンプルのCATAとSPWLが直下に作成されるように、CEをトップレベル要素に設定します。

   ![Set CE](_images/setup_set_ce_to_cata.png)

3. **SDS** タブで、**Load Master** をクリックします。

   ![Load Master](_images/setup_menu_load_master.png)

4. 確認ダイアログで **Yes** をクリックします。

   ![Confirm](_images/setup_confirm.png)

5. `/SDS-CATA` と `/SDS-SPWL` が作成されたことを確認します。

   ![New Elements](_images/setup_new_cata_spec.png)

## 図面テンプレートライブラリの準備

プロジェクト用にサンプル図面テンプレートライブラリを準備するには、以下の手順に従います：

1. **Draw** モジュールを開きます。

2. サンプルのDEPTとSTYLWLが直下に作成されるように、CEをトップレベル要素に設定します。

   ![Set CE](_images/setup_set_ce_to_dept.png)

3. **SDS** タブで、**Load Master** をクリックします。

   ![Load Master](_images/setup_menu_load_master.png)

4. 確認ダイアログで **Yes** をクリックします。

   ![Confirm](_images/setup_confirm.png)

5. `/FES-LIBRARIES` と `/FES-PENSTYLES` が作成されたことを確認します。

   ![New Elements](_images/setup_new_dept_stylwl.png)
