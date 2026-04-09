# SDSグローバル関数

SDSには、以下の便利なグローバル関数が用意されています。

## sdssettingsopen

`!!sdssettingsopen()`

設定JSONファイルをWindowsの既定のアプリで開きます。ファイルが存在しない場合は、SDS がプロジェクトの defaults ディレクトリに自動的に作成します。

**例:**

```pml
!!sdssettingsopen()
```

## sdsgetplatedetail

`!!sdsgetplatedetail(!ref is DBREF) is STRING`

指定した PANE または BOX 要素参照に対する、MTO テーブルで使用される説明文を返します。

**例:**

```pml
q var !!sdsgetplatedetail(ce)
```

## sdsrename

`!!sdsrename(!old is STRING, !new is STRING)`

指定した旧名称のサポートを、指定した新名称に変更します。

**例:**

```pml
!!sdsrename('/PS-0001','/PS-0002')
```
