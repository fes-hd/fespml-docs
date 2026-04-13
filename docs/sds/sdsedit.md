# Support Editor Form

The **SDS Support Editor** form provides tools to edit the target SUPPO element.

## Track CE

![Track CE](_images/ui_track_ce.png)

When this toggle is enabled, the form tracks CE: whenever CE changes, if CE is SUPPO or within SUPPO, that SUPPO becomes the target.

## Name

![Name](_images/ui_suppo_name.png)

Shows the name of the target SUPPO. Edit it to rename the target SUPPO.

## Members

![Members](_images/ui_suppo_members.png)

Lists the member elements of the target SUPPO. Right-click this list to open the context menu:

- **Reselect...**: Select another tag for the selected element.
- **Delete**: Delete the selected element.

## Create

### Add Preliminary

![Add Preliminary](_images/ui_add_preliminary.png)

Creates a preliminary ancillary attached to the piping component you pick.

### Add Ancillary

![Add Ancillary](_images/ui_add_ancillary.png)

Creates an ancillary attached to the piping component you pick.

### Add Framework

![Add Framework](_images/ui_add_framework.png)

Creates a framework attached at the position you pick.

### Add Framework Without Pick

![Add Framework Without Pick](_images/ui_add_framework_nopick.png)

Creates a framework without picking a position.

### Add Special Framework

![Add Special Framework](_images/ui_add_special_framework.png)

Creates an empty framework for a special shape.

## Modify Ancillary

### Position Through a Cursor Pick (Ancillary)

![Position Through a Cursor Pick](_images/ui_move_through.png)

Prompts you to pick a position in the 3D view, then moves the current ancillary along its direction until it intersects the reference plane through the picked position.

### Distance (Ancillary)

![Distance](_images/ui_move_distance.png)

Shows the distance from the previous piping component or ancillary to the current ancillary. Edit it to move the current ancillary from the previous component/ancillary towards the leave direction by the entered distance.

### Rotate Ancillary

![Rotate](_images/ui_rotate.png)

Click the rotate icon to rotate the current ancillary about the axis aligned with its direction by the angle (in degrees) entered in the **By** box.

### Align Ancillary Positions

![Align Ancillary Positions](_images/ui_align_positions.png)

Moves all other ancillaries in the target SUPPO whose directions are parallel to the current ancillary direction. They are moved along their directions until they intersect the reference plane through the current ancillary position, perpendicular to the current ancillary direction.

### Align Ancillary Directions

![Align Ancillary Directions](_images/ui_align_directions.png)

Rotates all other ancillaries in the target SUPPO whose directions are parallel to the current ancillary direction so that their directions become the same as the current ancillary direction.

### Recover Bad Compref Ancillaries

![Recover Bad Compref Ancillaries](_images/ui_recover_compref.png)

Recovers ancillaries in the target SUPPO whose compref attributes contain invalid references. For each ancillary, SDS finds the piping component it contacts and sets that component as the new compref.

## Modify Trunnion

### Position Through a Cursor Pick (Trunnion Component)

![Position Through a Cursor Pick](_images/ui_move_through.png)

Prompts you to pick a position in the 3D view, then moves the current trunnion component until it touches the reference plane through the picked position, perpendicular to the trunnion direction.

### Spool (Trunnion Component)

![Spool](_images/ui_move_spool.png)

Shows the arrive tube length of the current trunnion component. Edit it to move the current trunnion component so that the arrive tube length becomes the entered value.

### Rotate Trunnion Component

![Rotate](_images/ui_rotate.png)

Click the rotate icon to rotate the current trunnion component about the axis aligned with the trunnion direction by the angle (in degrees) entered in the **By** box.

## Modify Framework

### Convert to Special

![Convert to Special](_images/ui_convert_special.png)

Converts the current framework from a Framework Data File to Special so you can edit it manually.

### Reset Origin

![Reset Origin](_images/ui_reset_origin.png)

Moves the current framework back to its default origin position.

### Set Origin to a Cursor Pick

![Set Origin to a Cursor Pick](_images/ui_set_origin.png)

Prompts you to pick a position in the 3D view, then sets the STRU element position value of the current framework to the picked position. This updates only the stored origin value; it does not move the framework in the model.

### Extend Section to a Cursor Pick

![Extend Section to a Cursor Pick](_images/ui_extend_section.png)

Prompts you to pick a position in the 3D view, then extends the current steelwork section to the picked position. It also creates the joint FIXING element defined in the Framework Data File for the current framework tag when the element at the picked position satisfies the [condition](framework.md#condition) in the joint definitions.

> [!TIP]
> If you pick an ancillary, the steelwork section is extended beyond the picked position by the length specified by [steelEndLengths](ancillary.md#steelendlengths) in the Ancillary Data File.

### Delete Joint Fixing

![Delete Joint Fixing](_images/ui_delete_joint.png)

Deletes the current joint FIXING element.

## General

### Merge 2 Supports

![Merge 2 Supports](_images/ui_merge_supports.png)

Prompts you to pick a SUPPO element in the 3D view, then includes all member elements of the picked SUPPO as members of the target SUPPO.

### Copy Framework from Another Support

![Copy Framework from Another Support](_images/ui_copy_framework.png)

Prompts you to pick a SUPPO element in the 3D view, then copies the framework from the picked SUPPO to the target SUPPO.
