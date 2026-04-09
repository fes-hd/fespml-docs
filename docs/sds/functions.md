# SDS Global Functions

SDS provides the following useful global functions.

## sdssettingsopen

`!!sdssettingsopen()`

Opens the configuration JSON file with the default app in Windows. If the file does not exist, SDS automatically creates it in the project's defaults directory.

**Example:**

```pml
!!sdssettingsopen()
```

## sdsgetplatedetail

`!!sdsgetplatedetail(!ref is DBREF) is STRING`

Returns the description text used in the MTO table for the specified PANE or BOX element reference.

**Example:**

```pml
q var !!sdsgetplatedetail(ce)
```

## sdsrename

`!!sdsrename(!old is STRING, !new is STRING)`

Renames the support from the specified old name to the specified new name.

**Example:**

```pml
!!sdsrename('/PS-0001','/PS-0002')
```
