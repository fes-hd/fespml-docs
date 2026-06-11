# 図面オプションファイル

## はじめに

図面オプションファイル（Draw Option File）は、SDSがサポート図面をどのように生成するかを定義するJSONファイルです。**SDS Draw** フォームでは、各サポートはリスト内でオプションファイルに割り当てられます。サポート図面を生成または更新する際、SDSはそのサポートに割り当てられたオプションファイルを読み込み、その設定を適用します。

![Option File](_images/settings_default_opt.png)

## プロパティ

### templateDrwg

テンプレートのDRWG Ref。SDSがサポート図面を新しく生成または再生成する際、SDSはこの値で指定されたDRWGをコピーし、図面テンプレートとして使用します。

**例:**

```json
"templateDrwg": "/FES/DRA/PRJ/TMP/SUPPO/A3"
```

### plotStyle

サポート図面をPDFにエクスポートする際に使用されるPLTSTY Ref。SDSはPDF出力にこのプロットスタイルを使用します。

**例:**

```json
"plotStyle": "/FES-Monochrome"
```

### drawProcedures

サポート図面を生成または更新するために使用されるPMLコマンドリスト。SDSはコマンドを **上から順に** 実行します。

SDS によって処理される各 SUPPO について、コマンドリストが実行される前にその SUPPO 用の `!!SDSDRAWER` が利用可能になります。コマンドリスト内では、`!!SDSDRAWER` の組み込みメソッドを使用できるほか、必要に応じて独自の PML コマンドを追加することもできます。

**利用可能なメソッド:**

- `.ClearLayers(!vorder is STRING)` - 寸法およびラベル要素用のレイヤーをクリアします。
- `.UpdateViews()` - すべてのビューを更新します。
- `.DrawMtoTable()` - MTOテーブル（材料集計表）を描画します。
- `.DrawMtoLabels(!vorder is STRING)` - MTO の部品番号ラベルを作図します。
- `.DrawTouchedElementLabels(!vorder is STRING)` - 接触している要素の名前ラベルを作図します。
- `.SpreadTextLabels(!vorder is STRING)` - テキスト系ラベルをリモート配置で分散配置します。
- `.DrawGeneralSymbols(!vorder is STRING)` - パイプの端部/破断記号および原点記号を描画します。
- `.DrawRefDimensions(!vorder is STRING)` - 最も近いグリッドに対する参照寸法を描画します。
- `.DrawPipeNames(!vorder is STRING)` - サポートされているパイプ名のラベルを描画します。
- `.DrawWeldSymbols(!vorder is STRING)` - 溶接記号を描画します。
- `.DrawDimensions(!vorder is STRING)` - 寸法を描画します。
- `.DrawDetailOlays()` - 詳細ビューを描画します。

> [!NOTE]
> `!vorder` を持つメソッドの場合、`ALL` を渡すか、スペース区切りの `looking` 値のリストを渡して、対象のVIEW要素とその処理順序を選択します。
> `ALL` は、`viewDefs` のエントリと同じ順序を使用します。

**例:**

```json
"drawProcedures": [
  "!!SDSDRAWER.ClearLayers('ALL')",
  "!!SDSDRAWER.UpdateViews()",
  "!!SDSDRAWER.DrawMtoTable()",
  "!!SDSDRAWER.DrawGeneralSymbols('ALL')",
  "!!SDSDRAWER.DrawWeldSymbols('FRONT RSIDE PLAN')",
  "!!SDSDRAWER.DrawDimensions('FRONT RSIDE PLAN')",
  "!!SDSDRAWER.DrawRefDimensions('PLAN')",
  "!!SDSDRAWER.DrawPipeNames('PLAN RSIDE FRONT')",
  "!!SDSDRAWER.DrawMtoLabels('ISO3')",
  "!!SDSDRAWER.DrawTouchedElementLabels('ISO3')",
  "!!SDSDRAWER.SpreadTextLabels('ISO3')",
  "!!SDSDRAWER.DrawDetailOlays()"
]
```

### mtoNoteName

MTOテーブルを作成する対象のNOTE要素を検索するための名前パターン。

**例:**

```json
"mtoNoteName": "*/MTO"
```

### mtoSheetPos

シート上のMTOテーブルの原点コーナーのXY位置。

![Origin Corner](_images/drawopt_mto_ref_corner.png)

> [!NOTE]
> [mtoUpToDown](#mtouptodown) がtrueの場合、原点コーナーは左下ではなく **左上** になります。

**例:**

```json
"mtoSheetPos": "300mm 20mm"
```

### mtoUpToDown

trueの場合、SDSはMTOテーブルを上から下へ描画します。

**例:**

```json
"mtoUpToDown": false
```

**オプション:**

- `false` - 下から上へ

  ![Bottom to Top](_images/drawopt_mto_bottom_to_top.png)

- `true` - 上から下へ

  ![Top to Bottom](_images/drawopt_mto_top_to_bottom.png)

### mtoDivisionNum

MTOテーブルを分割する列数。

**例:**

```json
"mtoDivisionNum": 2
```

結果:

![2 Columns](_images/drawopt_mto_2_columns.png)

### mtoColumnDefs

MTOテーブルの列の定義。各エントリが1つの列を定義し、エントリは左から右へと適用されます。

**プロパティ:**

- `header` - テーブルヘッダーに表示されるテキスト。
- `align` - 列内のテキストの配置。

  オプション:
  - `L` - 左揃え
  - `C` - 中央揃え
  - `R` - 右揃え

- `width` - シート上の列の幅。
- `value` - 列に表示するMTO品目フィールド。

  オプション:
  - `number` - 品番（Part No.）
  - `desc` - 説明（Description）
  - `qty` - 数量（Quantity）
  - `pcs` - 数量 (個数)
  - `length` - 数量 (長さ)
  - `weight` - 重量（Weight）

**例:**

```json
"mtoColumnDefs": [
  { "header": "No.",         "align": "C", "width": "10mm", "value": "number" },
  { "header": "Description", "align": "L", "width": "35mm", "value": "desc"   },
  { "header": "Q'ty",        "align": "R", "width": "20mm", "value": "qty"    },
  { "header": "Weight",      "align": "R", "width": "15mm", "value": "weight" }
]
```

結果:

![MTO Table](_images/drawopt_mto_column_defs.png)

### viewFixNorth

trueの場合、正面（Front）ビューは北向きに固定されます。falseの場合、SDSは正面ビューの方向を自動的に決定します。

> [!NOTE]
> サポートモデルが北に対して斜めに配置されている場合、SDSはこの設定を無視し、正面ビューの方向を自動的に決定します。

**例:**

```json
"viewFixNorth": true
```

### touchLabelTexts

サポートに接触している要素のラベル定義。接触している各要素に対して、SDSはエントリを順番に評価し、`condition` がtrueとなる **最初** のエントリの `expression` を使用します。どのアントリにも一致しない場合、ラベルは生成されません。

**プロパティ:**

- `condition` - 接触している要素に対して評価される論理式。
- `expression` - 接触している要素のラベルテキストを生成するPML式。

**例:**

```json
"touchLabelTexts": [
  {
    "condition": "TYPE INSET('GENSEC','SCTN')",
    "expression": "DESC OF CATR"
  },
  {
    "condition": "TRUE",
    "expression": "AFTER(FULLNAME,'/')"
  }
]
```

この例では、接触している `GENSEC` または `SCTN` 要素には `DESC OF CATR` のラベルが付けられます。それ以外の接触している要素にはフォールバックエントリ（`condition`: `TRUE`）が使用され、`AFTER(FULLNAME,'/')` のラベルが付けられます。

### defaultViewDef

すべてのVIEW要素に適用されるデフォルトの設定。SDSは各VIEWを設定する際にこの定義から開始し、その後、VIEW要素名に一致するVIEW固有のオーバーライドを適用します。詳細については、[View Definition](#view-definition)を参照してください。

### viewDefs

VIEW固有のオーバーライド定義。SDSは、その `name` パターンがVIEW要素名に一致する場合にエントリを適用します。詳細については、[View Definition](#view-definition)を参照してください。

**例:**

```json
"viewDefs": [
  {
    "name": "*/PLAN",
    "looking": "PLAN"
  },
  {
    "name": "*/FRONT",
    "looking": "FRONT"
  },
  {
    "name": "*/SIDE",
    "looking": "RSIDE"
  },
  {
    "name": "*/ISO",
    "looking": "ISO3",
    "scales": "AUTO"
  }
]
```

### detailsOlayName

詳細ビューで使用されるOLAY名の接尾辞。

**例:**

```json
"detailsOlayName": "DETAIL"
```

### detailsXYScale

OLAY要素に適用されるXYScale（XおよびYのスケール係数）。

**例:**

```json
"detailsXYScale": "1.0 1.0"
```

### detailsSheetPos

詳細ビューのシート上のXY位置。SDSは、OLAY要素が作成される順序でこれらの位置を割り当てます。

> [!NOTE]
> OLAY要素の数が `detailsSheetPos` のエントリ数を超えた場合、SDSはエラーを発生させます。

**例:**

```json
"detailsSheetPos": ["150mm 200mm", "150mm 150mm", "150mm 100mm"]
```

### detailsItems

MTO品目から生成される詳細ビューの定義。各MTO品目に対して、SDSはエントリを順番に確認し、`condition` がtrueであるエントリのOLAY要素として詳細ビューを作成します。

`overref` または `plotfile` が設定されている場合、SDSはそれを使用します。どちらも設定されていない場合、SDSはOVERを作成し、`viewdir`、`title`、`dimxpos`、および `dimypos` を使用します。`dimxpos` と `dimypos` の **両方** が省略された場合、SDSは寸法を自動生成します。

**プロパティ:**

- `condition` - 詳細ビューを生成するためにMTO品目が満たす必要のある論理式。
- `overref` - 詳細ビューに表示されるOVER Ref。
- `plotfile` - 詳細ビューに表示されるプロットファイルへのファイルパス。
- `viewdir` - SDSが OVER を自動作成する際に使用される表示方向（Looking direction）。（デフォルト: `-Z WRT CE`）
- `title` - SDSが OVER を自動作成する際に使用されるタイトル。（デフォルト: `DETAIL`）
- `dimxpos` - SDSが OVER を自動作成する際に使用される、X方向に沿った寸法線の位置。
- `dimypos` - SDSが OVER を自動作成する際に使用される、Y方向に沿った寸法線の位置。

**例:**

```json
"detailsItems": [
  {
    "condition": "TYPE EQ 'FIXING' AND GTYPE OF CATR EQ 'RIBP'",
    "viewdir": "-Z WRT CE",
    "title": "RIBPLATE DETAIL",
    "dimxpos": ["P4POS", "P3POS", "P2POS"],
    "dimypos": ["P1POS", "P2POS", "P3POS"]
  },
  {
    "condition": "TYPE EQ 'FIXING' AND GTYPE OF CATR EQ 'PLAT'",
    "viewdir": "-Z WRT CE",
    "title": "PLATE DETAIL"
  }
]
```

### detailsTempOver

詳細ビュー（OLAY要素）用の OVER をSDSが自動作成する際に使用されるテンプレート OVER Ref。

**例:**

```json
"detailsTempOver": "/FES-SUPPO-DETAIL"
```

### detailsViewDef

詳細ビュー用にSDSが自動作成するOVERの下にあるVIEW要素に適用されるビュー定義。詳細については、[View Definition](#view-definition)を参照してください。

**例:**

```json
"detailsViewDef": {
  "name": "*/VIEW",
  "maxSize": "30mm 30mm",
  "padding": "10mm"
}
```

## View Definition

サポート図面内の VIEW 要素を設定するためのビュー定義。

**プロパティ:**

### name

VIEW要素名の名前パターン。

**例:**

```json
"name": "*/PLAN"
```

### looking

VIEW要素用にプリセットされた表示方向（Looking direction）。

**例:**

```json
"looking": "PLAN"
```

**オプション:**

- `PLAN` - 平面図（Plan view）
- `FRONT` - 正面図（Front view）
- `RSIDE` - 右側面図（Right-side view）
- `LSIDE` - 左側面図（Left-side view）
- `ISO1` - 等角図（Isometric view、北が右下）
- `ISO2` - 等角図（Isometric view、北が右上）
- `ISO3` - 等角図（Isometric view、北が左上）
- `ISO4` - 等角図（Isometric view、北が左下）

### scales

VIEW要素の候補となる縮尺のスペース区切りリスト。SDSは縮尺を左から右へ試行し、`maxSize` 内に収まる最初の縮尺を使用します。

> [!NOTE]
> 値が `AUTO` に設定されている場合、SDSはリストから選択するのではなく、収まる縮尺を計算します。

**例:**

```json
"scales": "1:1 1:2 1:5 1:10 1:15 1:20 1:25 1:50"
```

### maxSize

シート上の最大ビューサイズ（幅と高さ）。

**例:**

```json
"maxSize": "100mm 100mm"
```

### padding

サポートモデルをビューに収める際に、サポートモデルのバウンディングボックスのすべての方向に適用されるパディング。

**例:**

```json
"padding": "25mm"
```

### nArrowPrefix

方位記号（北向き矢印）として使用される SYTM 要素名プレフィックス（接頭辞）。SDSはVIEWの方向に基づいて `PLAN`、`ISO1`、`ISO2`、`ISO3`、または `ISO4` のいずれかをこのプレフィックスの後に追加し、その結果のSYTM名を使用します。

![North Arrow Plan](_images/drawopt_north_arrow_plan.png) ![North Arrow Iso](_images/drawopt_north_arrow_iso.png)

**例:**

```json
"nArrowPrefix": "/FES-NORTH-ARROW-"
```

これは、SDSがSYTM要素名として `/FES-NORTH-ARROW-PLAN`、`/FES-NORTH-ARROW-ISO1`、`/FES-NORTH-ARROW-ISO2`、`/FES-NORTH-ARROW-ISO3`、または `/FES-NORTH-ARROW-ISO4` を使用することを意味します。

### dimLayerPurp

寸法要素の LAYE を検索するために使用される Purpose のパターン。SDSは Purpose がこの値に一致する最初の LAYE を使用し、その LAYE の下に寸法要素を作成します。

**例:**

```json
"dimLayerPurp": "DIM*"
```

### dimStyle

SDS作成される寸法要素に使用される DMSTYL Ref。

**例:**

```json
"dimStyle": "/FES-DIM-BLACK"
```

### dimStaggered

trueの場合、SDSは寸法テキストを千鳥状に（交互に配置）配置します。

**例:**

```json
"dimStaggered": true
```

**オプション:**

- `false` - 寸法テキストは千鳥状になりません。

  ![Not Staggered](_images/drawopt_dim_not_staggered.png)

- `true` - 寸法テキストが千鳥状になります。

  ![Staggered](_images/drawopt_dim_staggered.png)

### dimPltxtLevel

垂直寸法の投影線（projection line）上にレベルを表示するために使用される LDIM Pltxt 値。

**例:**

```json
"dimPltxtLevel": "EL #POSU+<WRT /*>"
```

結果:

![Projection Line Text](_images/drawopt_dim_pltxt_lv.png)

### labLayerPurp

ラベル要素の LAYE を検索するために使用される Purpose のパターン。SDSは Purpose がこの値に一致する最初の LAYE を使用し、その LAYE の下にラベル要素を作成します。

**例:**

```json
"labLayerPurp": "LAB*"
```

### labStyle

SDSによって作成されるラベル要素に使用される LBSTYL Ref。

**例:**

```json
"labStyle": "/FES-LABEL-BLACK"
```

### labOrigin

サポートの原点マーカーとして使用される SYTM Ref。

![Origin Marker](_images/drawopt_lab_origin.png)

**例:**

```json
"labOrigin": "/FES-ORIGIN-MARKER"
```

### labGrid

通り芯番号の風船（バルーン）記号として使用される SYTM Ref。

![Grid ID Balloon](_images/drawopt_lab_grid.png)

**例:**

```json
"labGrid": "/FES-GRID-ID"
```

### labPipeName

サポート対象パイプ名のラベルとして使用される SYTM Ref。

![Pipe Name](_images/drawopt_lab_pipe_name.png)

**例:**

```json
"labPipeName": "/FES-PIPE-NAME"
```

### labPipeEnd

配管が VIEW の手前（正面）にある場合に使用される配管端部（断面）記号の SYTM Ref。

![Pipe End](_images/drawopt_lab_pipe_end.png)

**例:**

```json
"labPipeEnd": "/FES-PIPE-END"
```

### labPipeBreak

配管が VIEW の境界でクリップされている場合に使用される配管破断記号の SYTM Ref。

![Pipe Break](_images/drawopt_lab_pipe_break.png)

**例:**

```json
"labPipeBreak": "/FES-PIPE-BREAK"
```

### labWeldLeft

左側の引出線（lead）付き溶接記号として使用される SYTM Ref。

![Left-hand Weld](_images/drawopt_lab_weld_l.png)

**例:**

```json
"labWeldLeft": "/FES-FIELD-WELD-L"
```

### labWeldRight

右側の引出線（lead）付き溶接記号として使用される SYTM Ref。

![Right-hand Weld](_images/drawopt_lab_weld_r.png)

**例:**

```json
"labWeldRight": "/FES-FIELD-WELD-R"
```

### labMtoNo

MTO 部品番号ラベルとして使用される SYTM Ref。

![MTO Part No.](_images/drawopt_lab_mto_no.png)

**Example:**

```json
"labMtoNo": "/FES-MTO-NO"
```

### labTouchItem

サポートに接する要素の名称ラベルとして使用される SYTM Ref。

![MTO Touch Item](_images/drawopt_lab_touch_item.png)

**Example:**

```json
"labTouchItem": "/FES-TOUCH-ITEM"
```

### labHoleCLines

穴の中心線（十字線）記号として使用される SYTM Ref。

![Hole CL](_images/drawopt_lab_cl_hole.png)

**例:**

```json
"labHoleCLines": "/FES-CROSS-HAIRS"
```

### rRules

VIEWの表示ルール（Representation rule）の定義。SDSは `rRules` 内の各エントリについて、VIEWの下に1つの RRUL 要素を作成し、`style` と `criteria` を設定します。

**プロパティ:**

- `style` - 表示ルールによって適用される STYL Ref。
- `criteria` - 表示ルールが適用される要素を選択するPML式。

> [!NOTE]
> `criteria` において、`$!SUPPO` は対象のSUPPO要素名に自動的に置き換えられます。

**例:**

```json
"rRules": [
  {
    "style": "/FES/DRA/PRJ/STYL/GEN/SUPPO/SUPPO",
    "criteria": "$!SUPPO"
  },
  {
    "style": "/FES/DRA/PRJ/STYL/GEN/SUPPO/PIPE",
    "criteria": "ALL PIPE"
  },
  {
    "style": "/FES/DRA/PRJ/STYL/GEN/SUPPO/OTHERS",
    "criteria": "ALL"
  }
]
```
