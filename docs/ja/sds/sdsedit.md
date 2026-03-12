# サポートエディタフォーム

**SDS Support Editor** フォームは、対象のSUPPO要素を編集するためのツールを提供します。

## Track CE

![Track CE](_images/ui_track_ce.png)

このトグルが有効な場合、フォームはCEを追跡します：CEが変更されるたびに、CEがSUPPOであるかSUPPO内にある場合、そのSUPPOが対象（target）になります。

## Name

![Name](_images/ui_suppo_name.png)

対象のSUPPOの名前を表示します。編集することで、対象のSUPPOの名前を変更できます。

## Members

![Members](_images/ui_suppo_members.png)

対象のSUPPOのメンバー要素をリスト表示します。このリストを右クリックするとコンテキストメニューが開きます：

- **Reselect...**: 選択した要素の別のタグを選択します。
- **Delete**: 選択した要素を削除します。

## Create

### Add Preliminary

![Add Preliminary](_images/ui_add_preliminary.png)

ピックした配管コンポーネントに仮（preliminary）のアンシラリーを作成します。

### Add Ancillary

![Add Ancillary](_images/ui_add_ancillary.png)

ピックした配管コンポーネントにアンシラリーを作成します。

### Add Framework

![Add Framework](_images/ui_add_framework.png)

ピックした位置に取り付けるフレームワークを作成します。

### Add Framework Without Pick

![Add Framework Without Pick](_images/ui_add_framework_nopick.png)

位置をピックせずにフレームワークを作成します。

### Add Special Framework

![Add Special Framework](_images/ui_add_special_framework.png)

特殊な形状のための空のフレームワークを作成します。

## Modify Ancillary

### Position Through a Cursor Pick (Ancillary)

![Position Through a Cursor Pick](_images/ui_move_through.png)

3Dビューで位置をピックするように促し、現在のアンシラリーを、設定された方向（direction）に沿って、ピックした位置を通る参照面に交差するまで移動します。

### Distance (Ancillary)

![Distance](_images/ui_move_distance.png)

前の配管コンポーネントまたはアンシラリーから、現在のアンシラリーまでの距離を表示します。編集すると、現在のアンシラリーを前のコンポーネント/アンシラリーから離れる方向（leave direction）に入力された距離だけ移動します。

### Rotate Ancillary

![Rotate](_images/ui_rotate.png)

回転アイコンをクリックすると、現在のアンシラリーを、その方向に沿った軸を中心に、**By** ボックスに入力された角度（度）だけ回転させます。

### Align Ancillary Positions

![Align Ancillary Positions](_images/ui_align_positions.png)

対象フレーム内の他のすべてのアンシラリーのうち、現在のアンシラリーの方向と平行な方向を持つものを移動します。現在のアンシラリーの位置を通り、現在のアンシラリーの方向に対して垂直な参照面に交差するまで、それらの方向に沿って移動します。

### Align Ancillary Directions

![Align Ancillary Directions](_images/ui_align_directions.png)

対象フレーム内の他のすべてのアンシラリーのうち、方向が現在のアンシラリーの方向と平行なものを回転させます。これにより、それらの方向が現在のアンシラリーの方向と同じになります。

### Recover Bad Compref Ancillaries

![Recover Bad Compref Ancillaries](_images/ui_recover_compref.png)

対象のSUPPO内にある、compref属性に無効な参照を含むアンシラリーを復旧します。各アンシラリーについて、SDSは接触している配管コンポーネントを検索し、そのコンポーネントを新しいcomprefとして設定します。

## Modify Trunnion

### Position Through a Cursor Pick (Trunnion Component)

![Position Through a Cursor Pick](_images/ui_move_through.png)

3Dビューで位置をピックするように促し、現在のトラニオンコンポーネントを、トラニオンの方向に対して垂直でかつピックした位置を通る参照面に接するまで移動します。

### Spool (Trunnion Component)

![Spool](_images/ui_move_spool.png)

現在のトラニオンコンポーネントのarrive側のチューブ長さを表示します。編集すると、現在のトラニオンコンポーネントのarrive側のチューブ長さが入力された値になるように移動します。

### Rotate Trunnion Component

![Rotate](_images/ui_rotate.png)

回転アイコンをクリックすると、現在のトラニオンコンポーネントを、トラニオン方向に沿った軸を中心に、**By** ボックスに入力された角度（度）だけ回転させます。

## Modify Framework

### Convert to Special

![Convert to Special](_images/ui_convert_special.png)

現在のフレームワークを、フレームワークデータファイル（Framework Data File）による定義からSpecialに変換し、手動で編集できるようにします。

### Reset Origin

![Reset Origin](_images/ui_reset_origin.png)

現在のフレームワークを、デフォルトの原点位置に戻します。

### Set Origin to a Cursor Pick

![Set Origin to a Cursor Pick](_images/ui_set_origin.png)

3Dビューで位置をピックするように促し、現在のフレームワークのSTRU要素の位置（position）値をピックした位置に設定します。これは保存された原点値のみを更新し、モデル内のフレームワーク自体は移動させません。

### Extend Section to a Cursor Pick

![Extend Section to a Cursor Pick](_images/ui_extend_section.png)

3Dビューで位置をピックするように促し、現在の鋼材（steelwork section）をピックした位置まで延長します。また、ピックした位置の要素がジョイント定義の[condition](framework.md#condition)を満たしている場合、現在のフレームワークタグ用にフレームワークデータファイルで定義されたジョイントFIXING要素を作成します。

### Delete Joint Fixing

![Delete Joint Fixing](_images/ui_delete_joint.png)

現在のジョイントFIXING要素を削除します。

## General

### Merge 2 Supports

![Merge 2 Supports](_images/ui_merge_supports.png)

3DビューでSUPPO要素をピックするように促し、ピックしたSUPPOのすべてのメンバー要素を対象のSUPPOのメンバーとして含めます。

### Copy Framework from Another Support

![Copy Framework from Another Support](_images/ui_copy_framework.png)

3DビューでSUPPO要素をピックするように促し、ピックしたSUPPOから対象のSUPPOへフレームワークをコピーします。
