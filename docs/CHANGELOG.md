# Changelog

## 3.2.0 (2026-07-01)

- Added support for CSV import and export in the **SDS Draw** form.
- Changed the type of MTO number labels from `GLAB` to `SLAB`.
- Changed the Draw Option file format:
  - Added the `DrawMtoLabels`, `DrawTouchedElementLabels`, `SpreadTextLabels`, and `SetViewTitles` built-in methods to `!!SDSDRAWER`, and removed the `DrawItemLabels` built-in method from `!!SDSDRAWER` in the [drawProcedures](sds/drawopt.md#drawprocedures) property.
  - Added the [title](sds/drawopt.md#title), [labMtoNo](sds/drawopt.md#labmtono), and [labTouchItem](sds/drawopt.md#labtouchitem) properties to the View Definition.
  - Renamed the `labHoleCLines` property to [labCenterLines](sds/drawopt.md#labcenterlines) in the View Definition.
- Added an error-checking feature to the **Support Editor** form and the global function [sdsgetsuppoerrors](sds/functions.md#sdsgetsuppoerrors).
- Added the [Move to Correct ZONE](sds/sdsedit.md#move-to-correct-zone) button to the **Support Editor** form.

## 3.1.0 (2026-04-13)

- Changed JSON parsing to use PML.NET.
- Changed the members of the [steelBoltGauges](sds/ancillary.md#steelboltgauges) property in the Ancillary Data File.
- Added [Open Publish Path](sds/sdsdraw.md#open-publish-path) to the **File** menu of the **SDS Draw** form.
- Added the global function [sdsrename](sds/functions.md#sdsrename).
- Improved the [Extend Section to a Cursor Pick](sds/sdsedit.md#extend-section-to-a-cursor-pick) button so that it also adjusts the position of each support element when an ancillary is picked.
- Set the graphics-pick mode the first time SDS opens the edge positioning form.
- Fixed the position of an ancillary attached to sloped piping when it is moved to a graphics-picked line.
- Improved performance when opening the framework selection form.

## 3.0.0 (2026-03-26)

- First release of the new SDS
