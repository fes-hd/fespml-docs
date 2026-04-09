# 設定ファイル

## はじめに

SDSは、環境変数 `%XXXDFLTS%` （XXXはプロジェクトコード）で定義されたプロジェクトのデフォルトディレクトリにある設定JSONファイル `sds_settings.json` を使用してカスタマイズできます。

Windowsの既定のアプリで設定JSONファイルを開くには、**Command Window** で以下のコマンドを実行します：

```pml
!!sdssettingsopen()
```

ファイルが存在しない場合は、SDS がプロジェクトのデフォルトディレクトリに自動的に作成します。

## プロパティ

### zoneCondition

各 ZONE がサポート作成に使用されるかどうかを決定する論理式。

**デフォルト:**

```json
"zoneCondition": "purp inset('SUPP','SDS')"
```

これは、ZONE の purpose（目的）が `SUPP` または `SDS` に設定されている場合、SDSによってそれがサポートのZONEとして扱われることを意味します。

### volmSuffix

SDSが SUPPO を作成する ZONE を決定するために使用される VOLM 名の接尾辞（suffix）。

新規サポートを作成する際、ピックされた配管コンポーネントが VOLM 要素の VOLUME 内にある場合、SDSは、その VOLM 名から `volmSuffix` を削除した名前を持つ ZONE の配下に SUPPO を作成します。

**デフォルト:**

```json
"volmSuffix": "/VOLM"
```

### drwgSuffix

サポート図面の DRWG 名の接尾辞。

**デフォルト:**

```json
"drwgSuffix": "/DR"
```

### overShlbSuffix

サポート図面上のオーバーレイ・シート図枠（overlay sheets）に使用される SHLB 名の接尾辞。

**デフォルト:**

```json
"overShlbSuffix": "/OVERS"
```

### catePurpose

この CATE Purpose の値は、それがサポートのカタログであることを示します。**SDS** タブで **Generate Spec** をクリックしたとき、SDSは purpose がこの値と一致する `CATE` および `STCA` 要素を収集します。その後、SDSはそれらを使用して、[specAnci](#specanci) および [specJoin](#specjoin) で定義された SPEC 要素を更新します。

**デフォルト:**

```json
"catePurpose": "SDS"
```

これは、カタログの purpose が `SDS` に設定されている場合、SDSによってそれがサポートカタログとして扱われることを意味します。

### assyTagAttrib

アンシラリーのデータtagや、フレームワークのデータtagの保存に使用する属性名。新規にアンシラリーまたはフレームワーク要素を作成する際、SDSはこの値で指定された名前の属性にデータtagを設定します。

**デフォルト:**

```json
"assyTagAttrib": "FUNC"
```

これは、SDSがデータtagを `FUNC` 属性に保存することを意味します。

### assyTagPrelim

仮の（preliminary）サポートであることを示すために使用されるアンシラリーのデータtagの値。仮のアンシラリーを作成する際、SDSは tag がこの値と一致するアンシラリーデータを読み込み、アンシラリー要素がそのデータと一致するように設定します。

**デフォルト:**

```json
"assyTagPrelim": "PRELIM"
```

これは、 `PRELIM` とタグ付けされたアンシラリーデータが仮のアンシラリー要素として使用されることを意味します。

### assyAnciPaths

アンシラリーデータのJSONファイルが保存されているディレクトリのパス。

**例:**

```json
"assyAnciPaths": ["%pmllib%\\sds\\ancillaries"]
```

> [!TIP]
> 各パスには、パーセント記号（%）で囲まれた環境変数を使用できます。

### assyFrmwPaths

フレームワークデータのJSONファイルが保存されているディレクトリのパス。

**例:**

```json
"assyFrmwPaths": ["%pmllib%\\sds\\frameworks"]
```

### specAnci

アンシラリーカタログ用の SPEC Ref。

**例:**

```json
"specAnci": "/SDS-ANCI"
```

### specJoin

鉄骨ジョイントカタログ用の SPEC Ref。

**例:**

```json
"specJoin": "/SDS-JOIN"
```

### suppoTouchHier

サポートが接触している要素を検索する対象の階層（およびその配下）。サポート図面を生成する際、SDSはこれらの階層下で接触している要素も見つけて描画します。

**例:**

```json
"suppoTouchHier": "/SITE-A /SITE-B /SITE-C"
```

これは、SDSがサポートモデルと、`/SITE-A`、`/SITE-B`、および `/SITE-C` の階層配下で見つかった接触要素を描画することを意味します。

### drawDatabase

**SDS Draw** フォームで使用されるデータベースファイルのパス。

**例:**

```json
"drawDatabase": "%apsdflts%\\sds_draw.db"
```

### drawDefaultRegi

**SDS Draw** フォームの新しいエントリ用のデフォルトの REGI Ref。

![REGI Column](_images/settings_default_regi.png)

**例:**

```json
"drawDefaultRegi": "/SAMPLE-REGI"
```

**SDS Draw** フォームに新しい行を追加した際、SDSはREGI列の値を自動的に `/SAMPLE-REGI` に設定します。

### drawDefaultLiby

**SDS Draw** フォームの新しいエントリ用のデフォルトの LIBY Ref。

![LIBY Column](_images/settings_default_liby.png)

**例:**

```json
"drawDefaultLiby": "/SAMPLE-LIBY"
```

**SDS Draw** フォームに新しい行を追加した際、SDSはLIBY列の値を自動的に `/SAMPLE-LIBY` に設定します。

### drawDefaultOpt

**SDS Draw** フォームの新しいエントリ用のデフォルトの図面オプションファイルのパス。

![Option File Column](_images/settings_default_opt.png)

**例:**

```json
"drawDefaultOpt": "%pmllib%\\sds\\drawopts\\support_drawing_a3.json"
```

### drawPublishPath

サポート図面が PDF ファイルとして出力（publish）されるディレクトリのパス。

**例:**

```json
"drawPublishPath": "%userprofile%\\sds_publish"
```

これは、SDSがユーザーのプロファイルディレクトリ配下の `sds_publish` フォルダに図面を出力することを意味します。

### mtoGroupMode

同じ説明（description）を持つ MTO 品目をグループ化するモード。

**例:**

```json
"mtoGroupMode": "PCSONLY"
```

**オプション:**

- `OFF` - 品目をグループ化しません。

  例:

  | No. | Description |    Q'ty |
  | --: | :---------- | ------: |
  |   1 | 4" U-BOLT   |       1 |
  |   2 | 4" U-BOLT   |       1 |
  |   3 | L50x50x6    | 700.0mm |
  |   4 | L50x50x6    | 500.0mm |
  |   5 | L50x50x6    | 500.0mm |

- `PCSONLY` - 数量が長さベースでない品目のみをグループ化します。

  例:

  | No. | Description |    Q'ty |
  | --: | :---------- | ------: |
  |   1 | 4" U-BOLT   |       2 |
  |   2 | L50x50x6    | 700.0mm |
  |   3 | L50x50x6    | 500.0mm |
  |   4 | L50x50x6    | 500.0mm |

- `ON` - 全ての品目をグループ化します。

  例:

  | No. | Description |     Q'ty |
  | --: | :---------- | -------: |
  |   1 | 4" U-BOLT   |        2 |
  |   2 | L50x50x6    | 1700.0mm |

### mtoItemDefs

MTO テーブルの行を生成するための定義。各エントリは `selection` で要素を選択し、収集した各要素に対して他のプロパティを PML 式として評価して列を埋めます。

**プロパティ:**

- `selection` - 要素を選択するPML選択式。
- `desc` - 説明（description）テキストを構成するPML式。
- `pcs` - アイテムの数量（個数）を提供するPML式。
- `length` - アイテムの長さを提供するPML式。
- `weight` - アイテムの重量を提供するPML式。
- `labpos` - 品目ラベルの引き出し線が指し示す位置。

**例:**

```json
"mtoItemDefs": [
  {
    "selection": "ALL ANCI WITH NVOL NE 0",
    "desc": "DTXR",
    "pcs": "MTOQ OF DETR",
    "length": "MTOL",
    "weight": "NWEI",
    "labpos": "P19POS"
  }
]
```

### datalDefs

Datal ファイルの定義。**SDS** タブの **Load Master** をクリックすると、規定した名前の要素（`name` で指定）が既に存在しない限り、現在の DB タイプに `dbtype` が一致する各 Datal ファイルを SDS が実行します。

**プロパティ:**

- `name` - 最上位階層となる要素の名称。
- `dbtype` - Datal ファイルを展開するターゲットの DB タイプ。
- `file` - Datal ファイルのパス。

**例:**

```json
"datalDefs": [
  {
    "name": "/SDS-SPWL",
    "dbtype": "CATA",
    "file": "%pmllib%\\sds\\datals\\SDS-SPWL.txt"
  }
]
```
