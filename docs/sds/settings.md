# Configuration File

## Introduction

SDS can be customized using the configuration JSON file `sds_settings.json` in the project's defaults directory, as defined by the environment variable `%XXXDFLTS%` (where XXX is the project code).

To open the configuration JSON file with your Windows default app, run the following command in the **Command Window**:

```pml
!!sdssettingsopen()
```

If the file does not exist, it is automatically created in the project's defaults directory.

## Properties

### zoneCondition

A logical expression that determines whether each ZONE is used for support creation.

**Default:**

```json
"zoneCondition": "purp inset('SUPP','SDS')"
```

This means that if the ZONE's purpose is set to `SUPP` or `SDS`, SDS treats it as a support ZONE.

### volmSuffix

VOLM Name suffix to determine ZONE where to create a support.

**Default:**

```json
"volmSuffix": "/VOLM"
```

### drwgSuffix

DRWG Name suffix for support drawings.

**Default:**

```json
"volmSuffix": "/DR"
```

### overShlbSuffix

SHLB Name suffix for overlay sheets of support drawings.

**Default:**

```json
"overShlbSuffix": "/OVERS"
```

### catePurpose

CATE Purpose value indicates that this is a support catalog. When you click **Generate Spec** on the **SDS** tab, SDS gathers the `CATE` and `STCA` elements whose purpose matches this value. SDS then uses them to update the SPEC elements defined in [`specAnci`](#specanci) and [`specJoin`](#specjoin).

**Default:**

```json
"catePurpose": "SDS"
```

This means that if the catalog's purpose is set to `SDS`, SDS treats it as a support catalog.

### assyTagAttrib

The attribute name used to store the ancillary data tag. When you create a new ancillary, SDS sets the attribute named by this value to the ancillary data tag.

**Default:**

```json
"assyTagAttrib": "FUNC"
```

This means SDS stores the ancillary data tag in the `FUNC` attribute of the ancillary element.

### assyTagPrelim

The ancillary data tag value used to indicate a preliminary. When you create a preliminary ancillary, SDS loads the ancillary data whose tag matches this value and sets the ancillary element to match that data.

**Default:**

```json
"assyTagPrelim": "PRELIM"
```

This means the ancillary data tagged as `PRELIM` is used for preliminary ancillary elements.

### assyAnciPath

Path to the directory where ancillary data JSON files are stored.

**Example:**

```json
"assyAnciPath": "%pmllib%\\sds\\ancillaries"
```

> [!TIP]
> To specify a path, you can use environment variables enclosed in percent signs (%).

### assyFrmwPath

Path to the directory where framework data JSON files are stored.

**Example:**

```json
"assyFrmwPath": "%pmllib%\\sds\\frameworks"
```

### specAnci

SPEC Ref for ancillary catalogs.

**Example:**

```json
"specAnci": "/SDS-ANCI"
```

### specJoin

SPEC Ref for structural joint catalogs.

**Example:**

```json
"specAnci": "/SDS-JOIN"
```

### suppoTouchHier

Hierarchies (and below) to search for elements touched by the support. When you generate a support drawing, SDS also draws the touched elements found under these hierarchies.

**Example:**

```json
"suppoTouchHier": "/SITE-A /SITE-B /SITE-C"
```

This means SDS draws the support model and any touched elements found under the `/SITE-A`, `/SITE-B`, and `/SITE-C` hierarchies.

### drawDefaultRegi

Default REGI Ref for new entries in the **SDS Draw** form.

![REGI Column](_images/conf_default_regi.png)

**Example:**

```json
"drawDefaultRegi": "/SAMPLE-REGI"
```

When you append a new row in the **SDS Draw** form, SDS automatically sets the value in the REGI column to `/SAMPLE-REGI`.

### drawDefaultLiby

Default LIBY Ref for new entries in the **SDS Draw** form.

![LIBY Column](_images/conf_default_liby.png)

**Example:**

```json
"drawDefaultLiby": "/SAMPLE-LIBY"
```

When you append a new row in the **SDS Draw** form, SDS automatically sets the value in the LIBY column to `/SAMPLE-LIBY`.

### drawDefaultOpt

Default draw option file path for new entries in the **SDS Draw** form.

![Option File Column](_images/conf_default_opt.png)

**Example:**

```json
"drawDefaultOpt": "%pmllib%\\sds\\drawopts\\support_drawing_a3.json"
```

### drawPublishPath

Path to the directory where support drawings are published as PDF files.

**Example:**

```json
"drawPublishPath": "%userprofile%\\sds_publish"
```

This means SDS publishes drawings to the `sds_publish` folder under the user's profile directory.

### mtoGroupMode

Mode for grouping MTO items that have the same description.

**Example:**

```json
"mtoGroupMode": "PCSONLY"
```

**Options:**

- `OFF` - Do not group items.

  Example:

  | No. | Description |    Q'ty |
  | --: | :---------- | ------: |
  |   1 | 4" U-BOLT   |       1 |
  |   2 | 4" U-BOLT   |       1 |
  |   3 | L50x50x6    | 700.0mm |
  |   4 | L50x50x6    | 500.0mm |
  |   5 | L50x50x6    | 500.0mm |

- `PCSONLY` - Group only items whose quantity is not length-based.

  Example:

  | No. | Description |    Q'ty |
  | --: | :---------- | ------: |
  |   1 | 4" U-BOLT   |       2 |
  |   2 | L50x50x6    | 700.0mm |
  |   3 | L50x50x6    | 500.0mm |
  |   4 | L50x50x6    | 500.0mm |

- `ON` - Group all items.

  Example:

  | No. | Description |     Q'ty |
  | --: | :---------- | -------: |
  |   1 | 4" U-BOLT   |        2 |
  |   2 | L50x50x6    | 1700.0mm |

### mtoItemDefs

Definitions for generating MTO table rows. Each entry selects elements with `selection`, then fills the columns by evaluating the other properties as PML expressions for each collected element.

**Properties:**

- `selection` - PML selection expression that selects elements.
- `desc` - PML expression that composes the description text.
- `pcs` - PML expression that provides the item quantity.
- `length` - PML expression that provides the item length.
- `weight` - PML expression that provides the item weight.
- `labpos` - Position the item label’s leader line points to.

**Example:**

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

Datal file definitions. When you click **Load Master** on the **SDS** tab, SDS runs each Datal file whose `dbtype` matches the current DB type, unless an element with the name specified by `name` already exists.

**Properties:**

- `name` - Name of the top-level hierarchy element.
- `dbtype` - Target DB type for deploying the Datal file.
- `file` - Path to the Datal file.

**Example:**

```json
"datalDefs": [
  {
    "name": "/SDS-SPWL",
    "dbtype": "CATA",
    "file": "%pmllib%\\sds\\datals\\SDS-SPWL.txt"
  }
]
```
