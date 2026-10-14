# Figma interaction notes

Research for adapting PhotoCraft’s canvas behavior toward Figma. Sources are Figma Help Center articles unless a blog post or forum thread is named. Community cheat sheets are marked as such.

PhotoCraft’s menus still list the Photoshop shortcuts (⌘= zooms, ⌘0 fits, ⌘1 is 100%). The canvas view follows Figma: the wheel pans, ⇧ pans sideways, and ⌘/Ctrl or ⌥ zooms toward the pointer. ⌘/Ctrl-click selects the layer inside a group. Selection changes stay out of the undo stack. The rest of this note is the behavior those choices came from.

## Undo

⌘Z undoes. ⇧⌘Z redoes. Windows also commonly accepts Ctrl Y for redo; Figma’s help center documents undo more clearly than redo, so confirm redo against the in-app shortcuts panel (⌃⇧? on Mac, Ctrl Shift ? on Windows).

Selection changes are undo steps. A click, a selection, and a deselection each occupy history. One ⌘Z often restores the previous selection, and the next ⌘Z undoes the edit. That is the behavior to copy. It lets a mistaken click, or a walk down into nested layers, be reversed without starting the selection over. Forum threads asking Figma to drop this are long-running, and Figma staff have said it is known with no scheduled change ([When will Figma fix the UNDO behaviour?](https://forum.figma.com/report-a-problem-6/when-will-figma-fix-the-undo-behaviour-39468), [preference to exclude selection](https://forum.figma.com/suggest-a-feature-11/user-preference-to-include-or-exclude-object-selection-in-undo-17503)). People who want it kept use it to recover a deep selection and to return to a frame they had selected earlier.

Zoom and pan are view state for the current tab. They are not undo steps. [Adjust your zoom and view options](https://help.figma.com/hc/en-us/articles/360041065034-Adjust-your-zoom-and-view-options) says zoom changes apply only in the current tab.

There is no on-canvas list of undo steps. Older states live in version history: autosave checkpoints, named versions, and a non-destructive restore that keeps the current file as its own checkpoint. [View a file’s version history](https://help.figma.com/hc/en-us/articles/360038006754-View-a-file-s-version-history).

Multiplayer adds one invariant, from Evan Wallace’s [Multiplayer Editing in Figma](https://www.figma.com/blog/multiplayer-editing-in-figma/) (2016): if you undo a long way, copy something, and redo back to the present, the document must not change. Undo rewrites redo history at the moment of the undo, and redo rewrites undo history at the moment of the redo, so “put back what I did” cannot clobber a collaborator’s later edit.

## Pan and zoom

From [Navigate Figma Design files](https://help.figma.com/hc/en-us/articles/30925881896727-FD4B-Navigate-Figma-Design-files), [Adjust your zoom and view options](https://help.figma.com/hc/en-us/articles/360041065034-Adjust-your-zoom-and-view-options), [Pan and zoom in FigJam](https://help.figma.com/hc/en-us/articles/1500004414582-Pan-and-zoom-in-FigJam), and [Use Figma products with a keyboard](https://help.figma.com/hc/en-us/articles/360040328653-Use-Figma-products-with-a-keyboard).

Pan:

- Hold Space and drag. Space is a temporary hand tool; releasing it returns the previous tool. H leaves the hand tool on.
- Trackpad: two-finger drag pans. Pinch zooms.
- Mouse wheel pans vertically. Shift plus the wheel pans horizontally.
- Preferences can switch the wheel to zoom (`Use scroll wheel zoom`) and can enable right-click-drag to pan.
- Middle-mouse drag also pans. That one is community practice, not the help article.
- With nothing selected, arrow keys pan. Shift plus the arrows pans farther, and the distance scales with zoom. With a selection, the same keys nudge (below).

Zoom:

- A new file opens at zoom-to-fit.
- Pinch to zoom. ⌘ or Ctrl plus the wheel zooms. A Magic Mouse double-tap zooms in and back out.
- The point under the cursor stays put while zooming. The help article describes the gesture; the cursor anchor is observed product behavior, also stated on community cheat sheets.
- Shift + and Shift − zoom from the keyboard. + or ⌘+ zooms in, and − or ⌘− zooms out, including on non-US layouts ([Select keyboard layout](https://help.figma.com/hc/en-us/articles/5665442977431-Select-keyboard-layout)).
- Shift 1 fits the page. Shift 2 fits the selection. A link to a layer opens zoomed to that layer.
- The percentage in the toolbar is editable.
- Zoom scales the canvas, not the toolbars. In the desktop app, interface scale is a separate setting.
- The pixel grid appears at 400% and above. ⌘' toggles it. ⇧⌘' toggles snap to the pixel grid. The grid does not have to be visible for snapping to work.

## Selection

From [Select layers and objects](https://help.figma.com/hc/en-us/articles/360040449873-Select-layers-and-objects).

A click on something inside a group or frame selects the parent. Enter, or a double-click, steps one level down. ⇧Enter selects the parent. Tab and ⇧Tab move among siblings. ⌘-click (Ctrl-click on Windows) deep-selects the object under the cursor. ⌘-right-click opens a menu of every layer under the cursor, in layers-panel order, including locked layers (shown with a lock). Hidden layers are omitted from that menu until shown.

Esc clears the selection. Clicking empty canvas does the same. ⇧-click adds or removes an object. ⌘A selects everything on the canvas. ⇧⌘A inverts the selection.

A drag on empty canvas marquees top-level objects. ⌘-drag (Ctrl-drag) marquees nested objects and can select children without their parent. Selecting a parent selects its children, so the group moves together.

Hovering a row in the layers panel draws that layer’s bounds on the canvas (`Preferences > Highlight on hover`). Option 1 focuses the layers panel.

Matching objects (the same layer repeated across frames) can be selected together with ⌥⌘A, or by ⇧-dragging across the frames that contain them. The Edit menu can also select every layer with the same fill, stroke, effect, font, text properties, or component instance. A mixed selection exposes Selection Colors so one fill or stroke can be edited across the set.

View-only collaborators get a different chrome: a solid outline on the selection, a dashed outline on its parent, and the layer name in the properties panel. They can select; they cannot edit.

## Direct manipulation

From [Adjust alignment, rotation, position, and dimensions](https://help.figma.com/hc/en-us/articles/360039956914-Adjust-alignment-rotation-position-and-dimensions), [Arrange layers with Smart selection](https://help.figma.com/hc/en-us/articles/360040450233-Arrange-layers-with-Smart-selection), [Measure distances between layers](https://help.figma.com/hc/en-us/articles/360039956974-Measure-distances-between-layers), and the [Smart selection announcement](https://www.figma.com/blog/introducing-smart-selection/).

Moving, resizing, and rotating happen on the object. Edge handles change one axis, corner handles change both, and the selection shows its size in a label. Hovering just outside a corner rotates around the selection’s center. Shift snaps rotation to 15°. ⌥R (Alt R) reveals a draggable rotation origin. ⇧H and ⇧V flip.

Nudge, when something is selected: arrow keys move by the small nudge (default 1), Shift plus an arrow by the big nudge (default 10). Both are preferences, in points ([Set small and big nudge values](https://help.figma.com/hc/en-us/articles/4404575206295-Set-small-and-big-nudge-values)).

Snap draws a red guide to centers and outer edges of other objects, and to the pixel grid. Hold Control to suspend snap to objects or geometry while dragging. Snap settings are account-wide, also available from quick actions.

Alignment shortcuts sit on a WASD cluster: Alt W top, Alt A left, Alt S bottom, Alt D right, Alt V vertical centers, Alt H horizontal centers. One object aligns to its parent. Several objects align to each other. Shift-clicking an alignment control aligns the selection as a group to the parent frame.

Distribute keeps the outermost objects fixed and equalizes the gaps. Tidy up goes further: it lines objects up and equalizes spacing so the selection becomes a smart selection. Shortcut from the announcement post: ⌥⌘T (Ctrl Alt T).

A smart selection (evenly spaced objects overlapping on an axis, or a grid) grows pink handles on the canvas. Dragging a handle between items changes the gap for the whole set. A pink ring in an item marks it so it can be reordered inside the set. ⌘D while an item is marked inserts a duplicate and shifts the rest. Rearranging does not rewrite layer order in the panel. 2D sets behave like lists of lists; hold ⌘ to swap two items instead of inserting into a row.

Measuring is a modifier, not a tool. Select one object, hold Option (Alt), and hover another. A red line shows the horizontal and vertical gap, including across frames and groups. ⌘⌥ hover measures to a nested layer. The same Option-hover works between anchor points in vector edit mode. Persistent measurement annotations are a separate tool, Shift M, used more in Dev Mode ([Guide to inspecting](https://help.figma.com/hc/en-us/articles/22012921621015-Guide-to-inspecting)).

## Parenting, constraints, and auto layout

From [Parent, child, and sibling relationships](https://help.figma.com/hc/en-us/articles/360039959014-Parent-child-and-sibling-relationships), [Frames in Figma Design](https://help.figma.com/hc/en-us/articles/360041539473-Frames-in-Figma-Design), [Apply constraints](https://help.figma.com/hc/en-us/articles/360039957734-Apply-constraints-to-define-how-layers-resize), and [Guide to auto layout](https://help.figma.com/hc/en-us/articles/360040451373-Guide-to-auto-layout).

Dropping an object onto a frame reparents it when the object is smaller than the frame. A larger object stays outside. Holding Space during the drag prevents that reparent, and holding Space while dragging a child past the frame edge keeps the current parent.

Constraints (left, right, left-and-right, center, scale, and the same on the vertical axis) apply to children of ordinary frames. A dotted preview on the canvas shows the active constraints. They do not apply inside auto layout. Hold ⌘ (Ctrl) while resizing a frame to ignore constraints for that drag.

Auto layout is Shift A on a frame or a selection (a selection gets a new frame). ⌥⇧A removes it. Padding and gaps are editable from the canvas: Option sets opposite sides, Option Shift sets all sides, double-click an edge to hug contents, Option double-click to fill the container. Suggest auto layout (⌃⇧A) infers the nested frames. Layer order inside auto layout is flow order, so reordering moves the object.

The scale tool (K) is the proportional resize that also scales strokes and blurs and ignores nested constraints. Shift while resizing an unlocked object locks aspect ratio for that drag; Control temporarily unlocks a locked ratio.

## Properties

From [Copy and paste objects](https://help.figma.com/hc/en-us/articles/4409078832791-Copy-and-paste-objects), [Copy and paste properties](https://help.figma.com/hc/en-us/articles/4412765442967-Copy-and-paste-properties-between-layers), and the alignment article’s field behavior.

- Option-drag duplicates. Release the mouse before the key, or the original moves instead of copying.
- ⌘D duplicates in place, except a top-level frame, which lands to the right. Repeating ⌘D continues the same offset, and continues a rotation if the previous duplicate was rotated.
- Paste here drops at the cursor. Paste to replace (⇧⌘R) swaps the selected object and keeps its place.
- Copy properties is ⌥⌘C, paste properties is ⌥⌘V. A single fill, stroke, or effect can be copied by selecting that row in the sidebar and using ordinary ⌘C / ⌘V. Pasting text properties applies to the matching run around the cursor, or to a highlighted range.
- X, Y, W, H, and rotation fields accept math, including on a mixed selection (`Mixed+100` adds 100 to each).
- Scrub a field by dragging its label, or by Option-dragging the field. Dragging the pointer up the screen speeds the scrub through 2×, 1×, 1/2, and 1/4. Scrubbing continues past the edge of the window.

## Vectors

[Vector networks](https://help.figma.com/hc/en-us/articles/360040450213-Vector-networks) are the part of the pen that other editors usually lack. A network can branch. It does not have to be one directed loop that returns to its start. The pen (P) places points; dragging a point sets the curve; clicking an existing point closes. Escape leaves the path open. Any shape can be edited as a network afterward. Snap to geometry, in vector edit mode, aligns a point to other points, and Control suspends it while zoomed in.

## Finding commands

The shortcuts panel opens with ⌃⇧? and sits along the bottom so the canvas stays usable. Shortcuts already used are highlighted, and pressing one updates the panel immediately ([Use Figma products with a keyboard](https://help.figma.com/hc/en-us/articles/360040328653-Use-Figma-products-with-a-keyboard), [Figma’s New Finger Tips](https://www.figma.com/blog/figmas-new-finger-tips/)). Hovering a control also shows its shortcut.

The actions menu (⌘K) searches commands, assets, plugins, and bulk selects such as “same fill” or “same font” ([Use the actions menu](https://help.figma.com/hc/en-us/articles/23570416033943-Use-the-actions-menu-in-Figma-Design)). The keyboard-layout article still lists quick actions as ⌘/. Both are worth treating as the command palette. Shift I is quick insert for components. ⌘\ hides the interface chrome.

## Collaboration on the canvas

From the multiplayer post, [Adjust your zoom and view options](https://help.figma.com/hc/en-us/articles/360041065034-Adjust-your-zoom-and-view-options), and [View and manage comments](https://help.figma.com/hc/en-us/articles/360041547593-View-and-manage-comments).

Other people appear as named cursors and selections. Avatars sit in the corner; clicking one follows that person, and following is optional so leaving does not stop their presentation. ⌥⌘\ hides cursors. A personal file starts private; sharing is explicit.

Comments are pins on a point or region of the canvas, not a side thread detached from the picture. They cluster when zoomed out. C enters comment mode, which cannot edit objects. Esc returns to editing. ⇧C shows or hides pins. Hover previews a pin; click opens the thread.

## What transfers to a photo editor

The canvas habits transfer directly: selection in the undo stack, Space to pan, zoom toward the cursor, wheel and pinch, fit and zoom-to-selection, snap guides with a modifier to suspend them, Option to measure, Option-drag to duplicate, ⌘D to repeat the last duplicate, scrubbable number fields, a shortcuts panel that stays open, and a command palette.

Frames, auto layout, constraints, components, and vector networks are Figma’s design-tool model. They are documented here because they are where the product is strongest. They are a different document than a layered photograph, so they are reference rather than the first things to copy.
