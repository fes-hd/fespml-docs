# アンシラリーデータファイル

## はじめに

アンシラリーデータファイル（Ancillary Data File）は、SDSが配管に付随するアンシラリー（サポート部品など）をどのように作成するかを定義するJSONファイルです。設定ファイルの[assyAnciPaths](settings.md#assyancipaths)で指定されたディレクトリに保存されます。

## プロパティ

### tag

このアンシラリーデータファイルの一意な名前です。SDSは、モデル内でアンシラリーを作成する際に、どのデータファイルを使用したかを識別するためにこのtagを使用します。作成された要素にtagがどのように保存されるかについては[assyTagAttrib](settings.md#assytagattrib)を、仮アンシラリー用として予約されているtag値については[assyTagPrelim](settings.md#assytagprelim)を参照してください。

![Tag](_images/ancillary_tag.png)

**例:**

```json
"tag": "U-BOLT"
```

### description

アンシラリー選択フォームに表示される説明文です。

![Description](_images/ancillary_description.png)

**例:**

```json
"description": "U-Bolt 0.5\" - 24\""
```

### imgfile

アンシラリー選択フォームに表示される画像ファイルのパスです。

![Image](_images/ancillary_image.png)

**例:**

```json
"imgfile": "%pmllib%\\sds\\img\\sds_an_ubolt.png"
```

### condition

選択した配管コンポーネントに対して評価される論理式です。SDSは、これがtrueを返す場合にのみアンシラリー選択フォームで**Available**（利用可能）として表示し、それ以外の場合は表示しません。

**例:**

```json
"condition": "TYPE EQ 'TUBI' AND UNSET(IPAR)"
```

これは、要素のタイプが`TUBI`であり、保温（insulation）が設定されていない場合にアンシラリーが利用可能であることを意味します。

### owntype

モデル内に作成するアンシラリーの親（owner）要素のタイプです。

**オプション:**

- `SUPC` - 一般的なサポートコンポーネント用
- `TRUNNI` - トラニオンサポートコンポーネント用
- `LUG` - ラグサポートコンポーネント用
- `HANG` - パイプハンガー用

**例:**

```json
"owntype": "SUPC"
```

### components

SDSがアンシラリーを構築するために使用するコンポーネント定義のリストです。各エントリは作成する1つのコンポーネントを定義し、SDSは指定された順序でコンポーネントを作成します。

アンシラリーを作成する際、SDSはまず`owntype`で指定されたタイプの親要素を作成し、その下位（member）要素として各`components`エントリを作成します。子要素の作成時、SDSは`spec`で指定されたSPECから、`gtype`、`stype`、および選択された配管コンポーネントの呼び径サイズに一致するSPCOを選択し、`spref`を設定します。各子要素の作成後、SDSは（指定されていれば）`postCommands`を実行します。

**プロパティ:**

- `spec` (必須) - コンポーネントを選択するために使用されるSPEC Ref。
- `gtype` (必須) - コンポーネントを選択するために使用されるGtype。
- `stype` (必須) - コンポーネントを選択するために使用されるStype。
- `matref` - コンポーネントの材質を指定するSOLI Ref。
- `insu` - `true`の場合、選択された配管コンポーネントと同じ保温（insulation）のSPECをこのコンポーネントに設定します。
- `reduOffset` - 呼び径/距離調整用レジューサー（`gtype`が`REDU`）のオフセット方向。

  オプション:
  - `CENTRE` - オフセットなし
  - `BOTTOM` - 下面合わせ
  - `TOP` - 上面合わせ

- `reduBores` - 呼び径/距離調整用レジューサー（`gtype`が`REDU`）の呼び径サイズの組み合わせ。

  プロパティ:
  - `abore` - 到達側（Arrive）の呼び径サイズ
  - `lbore` - 離脱側（Leave）の呼び径サイズ

- `postCommands` - コンポーネント作成後に実行するPMLコマンド。

**例:**

```json
"components": [
  {
    "spec": "/SDS-ANCI",
    "gtype": "ANCI",
    "stype": "REST",
    "postCommands": [":MDSTrunNote1 'DO NOT CUT HOLE IN PIPE'"]
  },
  {
    "spec": "/SDS-ANCI",
    "gtype": "REDU",
    "stype": "MAKE",
    "insu": true,
    "reduOffset": "BOTTOM",
    "reduBores": [
      { "abore": "50mm",  "lbore": "40mm" },
      { "abore": "80mm",  "lbore": "50mm" },
      { "abore": "100mm", "lbore": "80mm" }
    ]
  },
  {
    "spec": "/SDS-ANCI",
    "gtype": "PLAT",
    "stype": "TREP",
    "matref": "/E3DSD_STEEL",
    "postCommands": ["clearance 100mm behind compref of first tranci"]
  }
]
```

### postCommands

SDSがアンシラリーの作成を完了した後に実行するPMLコマンド。

**例:**

```json
"postCommands": ["$m\"%apsdflts%\\sds\\ancillaries\\cmds.txt\""]
```

### steelEndLengths

アンシラリーが接触する鋼材の端部長さ（呼び径サイズ別）。各値は、鋼材の端から配管の中心線までの距離です。

**プロパティ:**

- `bore` - アンシラリーの呼び径サイズ。

- `open` - 他の鋼材に接続されていない鋼材の長さ。

![Open End](_images/ancillary_steel_end_open.png)

- `close` - 他の鋼材に接続されている鋼材の長さ。

![Close End](_images/ancillary_steel_end_close.png)

- `angle` - 他の鋼材に斜め切り（angled cut）で接続されている鋼材の長さ。

![Angled Cut End](_images/ancillary_steel_end_angle.png)

**例:**

```json
"steelEndLengths": [
  { "bore": "50mm",  "open": "70mm",  "close": "100mm", "angle": "100mm" },
  { "bore": "80mm",  "open": "90mm",  "close": "125mm", "angle": "125mm" },
  { "bore": "100mm", "open": "100mm", "close": "135mm", "angle": "135mm" }
]
```

### steelBoltGauges

ボルト固定式アンシラリーのための鋼材のボルトゲージ距離（`spref`別）。各エントリは、鋼材のLBOTからボルト固定位置までの距離を指定します。

![Bolt Gauge](_images/ancillary_steel_bolt_gauge.png)

**プロパティ:**

- `spref` - 鋼材の断面プロファイルのSPCO Ref。
- `xdist` - 鋼材のLBOTから鋼材カタログで見てX方向のボルト固定位置までの距離。
- `ydist` - 鋼材のLBOTから鋼材カタログで見てY方向のボルト固定位置までの距離。

**例:**

```json
"steelBoltGauges": [
  { "spref": "/BS-L50x50x6", "xdist": "30mm", "ydist": "30mm" },
  { "spref": "/BS-L65x65x6", "xdist": "35mm", "ydist": "35mm" },
  { "spref": "/BS-L75x75x9", "xdist": "40mm", "ydist": "35mm" }
]
```

### steelTouchedCmds

アンシラリーが鋼材に接触した際に実行するPMLコマンド。

SDSがこれらのコマンドを実行する際、接触した鋼材（GENSECまたはSCTN要素）のリファレンスを `!!SDSTOUCHEDSCTN` に割り当てます。これらのコマンド内でこの変数を使用して、接触した鋼材にアクセスできます。

**例:**

```json
"steelTouchedCmds": ["!!ce.mem[1].desp[1] = !!SDSTOUCHEDSCTN.rpro.ftka"]
```
