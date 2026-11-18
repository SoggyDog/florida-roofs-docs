---
title: Florida Roofs Tile Snap
---

# Florida Roofs Tile Snap

User guide for Unreal Engine 5.8. A free editor tool for the **[Florida Roofs: Materials &
Roof Kit](buyer-guide.html)** pack.

The pack's lead pans, tile-profile vents and round hoods are shaped to the tiles of its
barrel and flat tile coverings, so they only sit right on a tile cell. This plugin puts
them there: select the pieces, run one command, and each one moves onto the nearest tile
cell of the roof under it, turns to face up the slope, and switches to the mesh made for
that roof's pitch.

## Install

1. Install the plugin from Fab into your engine (Fab Library, or the Epic Games
   Launcher's Fab section), or copy the `FloridaRoofsTileSnap` folder into your project's
   `Plugins` folder.
2. In the editor: **Edit > Plugins**, search for "Florida Roofs Tile Snap", tick it, and
   restart the editor. It turns on the **Python Editor Script Plugin** it needs.

The plugin contains no assets and no code to compile: an editor Python script and the
menu entries for it.

## Use

1. Your tile roof uses a Florida Roofs tile instance (`MI_TileBarrel_*`,
   `MI_TileBarrelClose_*` or `MI_TileFlat_*`) with **WorldAligned** ticked (Tiling group).
   The tool measures the tile grid the same way the material lays the tiles out: from the
   roof actor's pivot along each facet.
2. Drag the pieces into the level and drop them roughly where you want them on the roof:
   `SM_TilePan_*` (lead pans), `SM_TileVent_*` (tile-profile vents),
   `SM_TileHood_Round_*` (round hoods). Any pitch version will do.
3. Select them and choose **Tools > Florida Roofs > Snap Tile Pieces to Roof**, or
   right-click one of them and choose the same entry.

Each piece moves to the nearest tile cell under it (at most half a tile), turns to face up
the slope, and is swapped for the version made for the roof's pitch (`_P4` to `_P8`). The
whole snap is one undo step. The Output Log has one line per piece saying what was done
or why it was skipped.

## When a piece is skipped

- **"the roof under it is not a Florida Roofs material with WorldAligned ticked"**: tick
  WorldAligned on the roof's instance, or check that the piece is above the roof (the tool
  looks straight down from 3 m above the piece).
- **"is not a tile kit piece"**: only pans, tile vents and round hoods are snapped; other
  kit pieces are placed by hand.
- **"no roof under it"**: move the piece over the roof.

## Limits

- Works on WorldAligned roofs only (roofs with metre UVs are laid out by their own UVs,
  which the tool cannot read).
- Snaps to the facet the trace hits; on a hip or valley line, nudge the piece onto the
  facet you want first.
