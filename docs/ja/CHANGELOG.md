# 変更履歴

## 3.2.0 (2026-07-01)

- **SDS Draw** フォームで CSV のインポートおよびエクスポートに対応しました。
- MTO 番号ラベルの要素タイプを `GLAB` から `SLAB` に変更しました。
- Draw Option ファイル形式を変更しました。
  - [drawProcedures](sds/drawopt.md#drawprocedures) プロパティにおいて、`!!SDSDRAWER` の組み込みメソッド `DrawMtoLabels`、`DrawTouchedElementLabels`、`SpreadTextLabels`、`SetViewTitles` を追加し、`DrawItemLabels` を削除しました。
  - View Definition に [title](sds/drawopt.md#title)、[labMtoNo](sds/drawopt.md#labmtono)、[labTouchItem](sds/drawopt.md#labtouchitem) プロパティを追加しました。
  - View Definition の `labHoleCLines` プロパティを [labCenterLines](sds/drawopt.md#labcenterlines) に改名しました。
- **Support Editor** フォームにエラーチェック機能を追加し、グローバル関数 [sdsgetsuppoerrors](sds/functions.md#sdsgetsuppoerrors) を追加しました。
- **Support Editor** フォームに [Move to Correct ZONE](sds/sdsedit.md#move-to-correct-zone) ボタンを追加しました。

## 3.1.0 (2026-04-13)

- JSON 解析に PML.NET を使用するように変更しました。
- Ancillary Data File の [steelBoltGauges](sds/ancillary.md#steelboltgauges) プロパティのメンバーを変更しました。
- **SDS Draw** フォームの **File** メニューに [Open Publish Path](sds/sdsdraw.md#open-publish-path) を追加しました。
- 新しいグローバル関数 [sdsrename](sds/functions.md#sdsrename) を追加しました。
- [Extend Section to a Cursor Pick](sds/sdsedit.md#extend-section-to-a-cursor-pick) ボタンを改善し、ancillary をピックしたときに各サポート要素の位置も調整するようにしました。
- SDS がエッジ位置指定フォームを初めて開くときに、グラフィックスのピックモードを設定するようにしました。
- 傾斜配管に取り付けられた ancillary をグラフィックスでピックした線へ移動する際の位置を修正しました。
- フレームワーク選択フォームを開く際のパフォーマンスを改善しました。

## 3.0.0 (2026-03-26)

- 新しいSDSの初回リリース
