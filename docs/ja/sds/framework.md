# フレームワークデータファイル

## はじめに

フレームワークデータファイル（Framework Data File）は、SDSがサポートフレームワークをどのように作成するかを定義するJSONファイルです。設定ファイル（Configuration File）の[assyFrmwPaths](settings.md#assyfrmwpaths)で指定されたディレクトリに保存されます。

## プロパティ

### tag

このフレームワークデータファイルの一意な名前です。SDSは、モデル内でフレームワークを作成する際に、どのデータファイルを使用したかを識別するためにこのtagを使用します。作成された要素にtagがどのように保存されるかについては[assyTagAttrib](settings.md#assytagattrib)を参照してください。

![Tag](_images/framework_tag.png)

**例:**

```json
"tag": "FGP-A-L50"
```

### description

フレームワーク選択フォームに表示される説明文です。

![Description](_images/framework_description.png)

**例:**

```json
"description": "Goalpost on Floor L50 Angled Cut"
```

### imgfile

フレームワーク選択フォームに表示される画像ファイルのパスです。

![Image](_images/framework_image.png)

**例:**

```json
"imgfile": "%pmllib%\\sds\\img\\sds_fr_floor_goalpost.png"
```

### pickFor

サポートの原点からフレームワークを取り付ける表面に向かう方向。ピックした方向が `pickFor` に一致しない場合、SDSはフレームワーク選択フォームで **Available**（利用可能）を `False` に設定します。

**オプション:**

- `DOWN` - 床（原点から下方向）
- `UP` - 天井（原点から上方向）
- `LEFT` - 原点の左側の壁
- `RIGHT` - 原点の右側の壁
- `FRONT` - 原点の手前の壁
- `BACK` - 原点の奥の壁

**例:**

```json
"pickFor": "DOWN"
```

### vertical

このフレームワークが垂直（縦引き）配管用であるかどうか。サポートする配管の方向が `vertical` と一致しない場合、SDSはフレームワーク選択フォームで **Available**（利用可能）を `False` に設定します。

**オプション:**

- `false` - **水平**（横引き）配管用
- `true` - **垂直**（縦引き）配管用

**例:**

```json
"vertical": false
```

### minBore

このフレームワークに取り付けることができるアンシラリーの最小呼び径サイズ。サポートされるアンシラリーの中に `minBore` より小さい呼び径を持つものがある場合、SDSはフレームワーク選択フォームで **Available**（利用可能）を `False` に設定します。

**例:**

```json
"minBore": "15mm"
```

### maxBore

このフレームワークに取り付けることができるアンシラリーの最大呼び径サイズ。サポートされるアンシラリーの中に `maxBore` より大きい呼び径を持つものがある場合、SDSはフレームワーク選択フォームで **Available**（利用可能）を `False` に設定します。

**例:**

```json
"maxBore": "600mm"
```

### endPrepLeft

バー（bar section）の左端の端部形状タイプ。SDSは、アンシラリーデータファイル内の[steelEndLengths](ancillary.md#steelendlengths)を検索する際にこの設定を使用します。

**オプション:**

- `OPEN` - 端部が他の鋼材セクションに接続されていない。
- `CLOSE` - 端部が他の鋼材セクションに接続されている。
- `ANGLE` - 端部が他の鋼材セクションに斜め切り（angled cut）で接続されている。

**例:**

```json
"endPrepLeft": "CLOSE"
```

### endPrepRight

バーの右端の端部形状タイプ。[endPrepLeft](#endprepleft)と同じです。

**例:**

```json
"endPrepRight": "CLOSE"
```

### endExtendOffset

SDSがピックされた取り付け位置に到達するようにバーの端部を自動的に延長する際に適用される、追加のオフセット量。自動延長される長さを短くするには、負の値を指定します。

**例:**

```json
"endExtendOffset": "25mm"
```

### bar

アンシラリーが配置されるバーセクションの定義。詳細については、[Section Definition](#section-definition)を参照してください。

**例:**

```json
"bar": {
  "suffix": "BAR",
  "spref": "/BS-PFC100x50x10",
  "matref": "/E3DSD_S275JR",
  "jusline": "LBOT",
  "lmirror": false,
  "ydir": "D WRT OWN"
}
```

### legs

レッグ（脚部）セクションの定義。レッグのエントリで省略されたプロパティは、`bar` の値を継承します。詳細については、[Section Definition](#section-definition)を参照してください。

**例:**

```json
"legs": [
  {
    "suffix": "LEG-L",
    "side": "LEFT",
    "lmirror": false,
    "ydir": "W WRT OWN",
    "zdir": "D WRT OWN",
    "xoffset": "0mm",
    "zoffset": "20mm"
  },
  {
    "suffix": "LEG-R",
    "side": "RIGHT",
    "lmirror": true,
    "ydir": "E WRT OWN",
    "zdir": "D WRT OWN",
    "xoffset": "0mm",
    "zoffset": "20mm"
  }
]
```

### postCommands

SDSがフレームワークの作成を完了した後に実行するPMLコマンド。

**例:**

```json
"postCommands": ["$m\"%apsdflts%\\sds\\frameworks\\cmds.txt\""]
```

## Section Definition

鋼材セクション定義。

**プロパティ:**

### suffix

親要素の名前に追加されてGENSEC名を構成する接尾辞。

**例:**

```json
"suffix": "BAR"
```

これは、SDSがGENSEC名を `<SUPPO Name>/STRU-BAR` にすることを意味します。

### side

（レッグのみ）レッグセクションがバーセクションのどちら側に接続するかを指定します。

**オプション:**

- `LEFT` - バーセクションの左側に接続する。
- `RIGHT` - バーセクションの右側に接続する。
- `MID` - バーセクションの中点に接続する。

**例:**

```json
"side": "LEFT"
```

### spref (Section)

このGENSECの鋼材プロファイルを指定するSPCO Ref。

**例:**

```json
"spref": "/BS-PFC100x50x10"
```

### matref (Section)

このGENSECの材質を指定するSOLI Ref。

**例:**

```json
"matref": "/E3DSD_S275JR"
```

### shop (Section)

このGENSECの工場/現場（Shop/Site）フラグ。このフラグは、サポート図面上での現場溶接（field weld）記号の配置位置に影響します。

**例:**

```json
"shop": false
```

### jusline

このGENSECの基準線となるP-Line名。

**例:**

```json
"jusline": "LBOT"
```

### lmirror

GENSECがミラー反転した形状で作成されるかどうか。

**例:**

```json
"lmirror": false
```

### ydir

このGENSECのSPINEに対するY方向。`ydir` を変更するとGENSECの向きが回転します。

**例:**

```json
"ydir": "W WRT OWN"
```

### zdir

（レッグのみ）レッグセクションが伸びる方向。

**例:**

```json
"zdir": "D WRT OWN"
```

### xoffset

（レッグのみ）GENSECの開始位置からのXオフセット。

> [!TIP]
> X/Y/Z方向は、**SDS Support Editor** フォームが開いている間に3Dビューに表示される軸の矢印と一致します。
>
> ![XYZ](_images/framework_xyz.png)

**例:**

```json
"xoffset": "25mm"
```

### yoffset

（レッグのみ）GENSECの開始位置からのYオフセット。

**例:**

```json
"yoffset": "-25mm"
```

### zoffset

（レッグのみ）GENSECの開始位置からのZオフセット。

**例:**

```json
"zoffset": "20mm"
```

### postCommands (Section)

GENSEC作成後に実行するPMLコマンド。

**例:**

```json
"postCommands": ["!!ce.desp[1] = 50"]
```

### startJoints

セクションの始端に接続されるFIXINGジョイントの定義。詳細については、[Joint Definition](#joint-definition)を参照してください。

SDSは、[endJoints](#endjoints)と同じロジックを適用します。

**例:**

```json
"startJoints": [
  {
    "spref": "/SDS-JOIN/SDS-TP-WELD-P50",
    "matref": "/E3DSD_S275JR",
    "orientation": "Y is N WRT OWN and Z is D WRT OWN",
    "cutback": "RPRO PTHK"
  }
]
```

### endJoints

セクションの終端に接続されるFIXINGジョイントの定義。詳細については、[Joint Definition](#joint-definition)を参照してください。

SDSはエントリを上から下に確認し、ピックされた取り付け要素と `condition` が一致する**最初**のエントリを使用します。 `condition` が省略された場合は、常に `true` として扱われます（これをフォールバックエントリとして使用します）。その後、SDSはセクションの終端にそのFIXINGジョイントを作成します。

**例:**

```json
"endJoints": [
  {
    "condition": "PURP OF ZONE eq 'CIV'",
    "spref": "/SDS-JOIN/SDS-BP-BOLT2X-C100",
    "matref": "/E3DSD_S275JR",
    "shop": false,
    "orientation": "Y is E WRT OWN and Z is U WRT OWN",
    "cutback": "RPRO PTHK",
    "members": [
      {
        "spref": "/SDS-JOIN/SDS-BOLT-ANCHOR-M12",
        "position": "P5POS",
        "orientation": "Z is P5DIR"
      },
      {
        "spref": "/SDS-JOIN/SDS-BOLT-ANCHOR-M12",
        "position": "P6POS",
        "orientation": "Z is P6DIR"
      }
    ]
  },
  {
    "spref": "/SDS-JOIN/SDS-BP-WELD-C100",
    "matref": "/E3DSD_S275JR",
    "orientation": "Y is E WRT OWN and Z is U WRT OWN",
    "cutback": "RPRO PTHK"
  }
]
```

## Joint Definition

FIXINGジョイントの定義。

**プロパティ:**

### condition

このジョイントが作成されるために、ピックされた取り付け要素が満たす必要のある論理式。`condition` が省略された場合は、常に `true` となります。

**例:**

```json
"condition": "PURP OF ZONE eq 'CIV'"
```

これは、SDSがこのジョイントを作成するのは、ピックされた要素が `PURP` が `CIV` のZONEの配下にある場合のみであることを意味します。

### spref (Joint)

このFIXINGのジョイントカタログを指定するSPCO Ref。

**例:**

```json
"spref": "/SDS-JOIN/SDS-BP-BOLT2X-C100"
```

### matref (Joint)

このFIXINGの材質を指定するSOLI Ref。

**例:**

```json
"matref": "/E3DSD_S275JR"
```

### shop (Joint)

このFIXINGの工場/現場（Shop/Site）フラグ。このフラグは、サポート図面上での現場溶接（field weld）記号の配置位置に影響します。

**例:**

```json
"shop": false
```

### orientation

このFIXINGに適用される向き（Orientation）。

**例:**

```json
"orientation": "Y is N WRT OWN and Z is D WRT OWN"
```

### cutback

ジョイントのために、取り付けられるセクションの端部を切り詰める量。

**例:**

```json
"cutback": "RPRO PTHK"
```

### postCommands (Joint)

FIXING作成後に実行するPMLコマンド。

**例:**

```json
"postCommands": ["BY U 50mm"]
```

### members

このジョイントの一部として作成されるメンバーFIXING要素の定義。各エントリは、1つのメンバーFIXINGと、それがどのように配置・向き付けされるかを記述します。

**プロパティ:**

- `spref` - このFIXINGのメンバージョイントカタログを指定するSPCO Ref。
- `matref` - このFIXINGの材質を指定するSOLI Ref。
- `position` - このFIXINGの配置位置。
- `orientation` - このFIXINGの向き（Orientation）。
