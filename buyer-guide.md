---
title: Florida Roofs: Materials & Roof Kit
---

# Florida Roofs: Materials & Roof Kit

User guide for Unreal Engine 5.8.

Roof coverings and roof parts as they are found on Florida and Sunbelt houses:
architectural shingle, concrete barrel and flat tile, standing seam, 5V crimp and the
metal roof-overs used on manufactured homes. Every covering ages the way that material
really fails, with live sliders from new to worn. The look and the wear were checked
against a home inspector's drone photos of real roofs. No photos are included in the pack.

- [Quick start](#quick-start)
- [What's in the pack](#whats-in-the-pack)
- [Putting a covering on your roof](#putting-a-covering-on-your-roof)
- [Condition and wear](#condition-and-wear)
- [Material parameters](#material-parameters)
- [Roof kit pieces](#roof-kit-pieces)
- [Lighting and performance](#lighting-and-performance)
- [Known limits](#known-limits)

## Quick start

1. Open `FloridaRoofs/Maps/Showcase` to see every covering and kit piece.
2. Drag a material instance onto your roof mesh, for example
   `MI_ShingleArch_WeatheredGray_Fair`.
3. If your roof's UVs are not laid out in metres (most aren't), open the instance and
   tick **WorldAligned** (Tiling group). The covering now lays itself out on every facet:
   courses along the eave, running down the slope, at real size.
4. Move the wear sliders (Wear group) to age the roof.

## What's in the pack

### Coverings

Each colour has a clean instance `MI_<Covering>_<Colour>` and three children with preset
wear: `_Good`, `_Fair`, `_Worn`. All textures are 2048 px and tile seamlessly.

| Covering | What it is | Tile size | Colours |
|---|---|---|---|
| ShingleArch | Laminated architectural asphalt shingle, 143 mm exposure | 2.0 m | WeatheredGray, Charcoal, LightGray, TanBrownBlend, BrownBlend, Driftwood, GrayGreen, Green, Black |
| ShingleCap | Hip and ridge cap shingle (used by the kit's ridge and hip pieces) | 2.0 m | as ShingleArch |
| TileBarrel | Concrete S tile, even barrel and pan | 2.1 m | Terracotta, TerracottaBlend, TanBlend, Gray, White |
| TileBarrelClose | Concrete S tile, tall round barrels, narrow deep pans | 2.1 m | as TileBarrel |
| TileFlat | Flat concrete tile, 30 cm courses | 2.1 m | Charcoal, Slate, Brown, Tan, Terracotta |
| TileCap | Concrete ridge, hip and rake caps (used by the tile kit) | 2.0 m | all tile colours |
| MetalSeam | Standing seam, 16" panels, striated pans | 2.03 m | Galvalume, White, LightGray, AshGray, Charcoal, DarkBronze, Green, Taupe |
| MetalSeamFlat | Standing seam, flat pans | 2.03 m | as MetalSeam |
| Metal5V | 5V crimp, 24" panels, exposed screws | 1.83 m | Galvalume, White |
| MetalRib | Rib panel roof-over, 16" ribs, cross laps | 2.03 m | White, MillFinish, Galvalume |
| MetalCorr | Close 4" rib roof-over | 1.83 m | MillFinish, White |

### Roof kit

Static meshes for everything that sits on or caps a roof: ridge and hip caps, ridge vents,
plumbing stacks, exhaust hoods, off-ridge and turtle vents, chimneys with crickets, tile
ridge / hip / rake caps with mortar, roof-to-wall flashing, lead pans and tile vents, and
metal ridge, hip, rake and eave trim with boots and flues. Most pieces come at 4, 5, 6, 7
and 8 in 12 (metal trim 3-8 in 12); the pitch is the `_P<n>` at the end of the name.

### Example roofs

In `Meshes`: a gable, a hip with deliberately wrong UVs (to show WorldAligned), a standing
seam hip roof, two manufactured-home roof-overs, and cross-gable tile roofs at 6 in 12
with cut tile valleys in each tile profile (`SM_ExampleValley`, `SM_ExampleValleyClose`,
`SM_ExampleValleyFlat`; each with its `Band` of cut tiles and its `Ridge`). Each comes with
the materials it wears in the demo maps.

In `Meshes/Showcase`: the showcase houses, including two L-plan houses with a gable wing
over the garage: a shingle one with closed-cut valleys (the wing's shingles run through
the valley, the main roof's are cut along it) and a barrel tile one with cut tile valleys
over W valley pans, its wing ridge teed into the main ridge.

## Putting a covering on your roof

The covering needs to know which way is down the slope. There are two ways to tell it.

**WorldAligned (recommended for your own meshes).** Tick `WorldAligned` on the instance.
Each flat facet then gets its own layout from its geometry: U along the eave, V down the
slope, in metres. Your mesh's UVs, normals and tangents are ignored by the covering. The
normal map and the parallax depth follow the same layout, so lighting stays correct on
every facet.

- The layout starts at the roof actor's pivot: courses, crimps and the tile grid are
  measured from it along each facet. Put the pivot where you want the pattern to start
  (a gable corner is a good choice). The texture moves with the roof when you move it.
- Facets must be flat (normal roof planes are). Curved surfaces get a faceted layout.
- The pattern breaks where two facets meet at a hip or ridge, as a real roof does; the
  kit's caps cover that line.

**Mesh UVs.** Leave WorldAligned off when your roof's UVs are already in metres, with U
along the eave and V running down the slope (Unreal's V; in Blender, before export, v
runs up the slope). The example gable is built this way. This is cheaper than
WorldAligned and lets you place the tile grid exactly.

## Condition and wear

Each covering wears the way that material actually fails:

- **Asphalt shingle** loses granules. The loss shows as a fine freckle of single bare
  granules that thickens on some tabs and never evenly; it is worst on ridge and hip caps
  and near the butt edges. Black algae streaks run down the slope; moss starts in the
  shade lines.
- **Concrete tile** keeps its shape but loses its colour coat: the barrel crowns fade
  chalky and pale. Black streaks run down the pans, dirt collects in pans and at the butts,
  moss grows under the butts.
- **Standing seam** paint chalks (lighter, flatter, greyer); grime collects at the seam
  feet and streaks down; installer scuffs appear in foot-traffic paths.
- **5V and roof-over metal** rust around the screws and along the laps, with rust streaks
  running down. Owners patch them: dabs of sealant over screws and coated strips over
  laps. On roof-overs water ponds in the pans and leaves stains.

The presets:

| | Algae | Grime | Moss | GranuleLoss | Fade |
|---|---|---|---|---|---|
| ShingleArch Good / Fair / Worn | 0.2 / 0.45 / 0.6 | 0.3 / 0.5 / 0.65 | 0 / 0.1 / 0.3 | 0.03 / 0.12 / 0.25 | 0 / 0.03 / 0.05 |
| ShingleCap | 0.1 / 0.23 / 0.3 | 0.3 / 0.5 / 0.65 | 0 / 0.05 / 0.15 | 0.06 / 0.24 / 0.5 | 0 / 0.03 / 0.05 |
| Tiles and TileCap | 0.18 / 0.36 / 0.55 | 0.3 / 0.5 / 0.7 | 0 / 0.1 / 0.3 | 0.03 / 0.05 / 0.15 | 0 / 0.04 / 0.08 |
| MetalSeam, MetalSeamFlat | 0 / 0.08 / 0.15 | 0.15 / 0.3 / 0.45 | 0 | 0.01 / 0.03 / 0.05 | 0.03 / 0.12 / 0.25 |
| Metal5V, MetalRib, MetalCorr | 0.05 / 0.2 / 0.4 | 0.2 / 0.4 / 0.6 | 0 / 1 / 2 | 0.01 / 0.04 / 0.06 | 0.03 / 0.12 / 0.25 |

Keep caps a step more worn than the field they sit on; they weather first.

## Material parameters

All instances share `M_RoofLayered`. Override any parameter on an instance.

### Wear

| Parameter | Range | What it does |
|---|---|---|
| Algae | 0-1 | Black algae streaks running down the slope. On metal: faint mildew streaks. |
| Grime | 0-1 | Dirt in low spots and down-slope streaks. On fastened metal it includes the rust streaks below screws and the ponding stains. |
| Moss | 0-1 | Moss in shade lines and under butts. **On Metal5V, MetalRib and MetalCorr it is sealant patches instead**: 1 shows the screw dabs, 2 also the lap strips (type 2; the slider stops at 1). |
| GranuleLoss | 0-1 | The fraction of the surface that has failed. Shingle: bare granules. Tile: colour coat loss on the crowns. Standing seam: scuffs. Fastened metal: rust. Values above about 0.3 look extreme. |
| Fade | 0-1 | Sun fade and chalking: colour moves toward grey and lighter; metal goes matte. |
| MacroMix | 0-1 | How much an 8 m variation map modulates every layer, so the wear comes and goes across a large roof instead of repeating every tile. 0.5 by default. |
| BareRough | 0-1 | Roughness where the surface has failed. |

The colours the layers blend toward (`AlgaeCol`, `GrimeCol`, `MossCol`, `BareCol`) are in
the Wear colours group. Each covering sets its own.

### Tiling

| Parameter | What it does |
|---|---|
| WorldAligned | Lays the covering out from each facet's geometry (see above). |
| TileMeters | Size of one texture repeat, in metres. Set per covering; change it only to rescale the whole covering. |
| MacroMeters | Size of the wear-variation map's repeat (8 m). |
| WearTexels | Resolution of the wear map. Leave as set. |

### Parallax

| Parameter | What it does |
|---|---|
| ParallaxDepth | Depth of the surface relief in texture units (set from each covering's real height; 0 turns parallax off). |
| ParallaxMinSteps, ParallaxMaxSteps | Ray-march steps when looking straight down / at grazing angles (12 / 48). Lower for speed. |
| FieldNormal | 1 uses the covering's normal map; 0 makes it flat. Use 0 on real tile meshes that should only take the covering's colour and wear. |

Parallax writes pixel depth offset, so meshes set into the field (lead pans, vent tiles,
mortar beds, chimney walls) cut into the barrels and pans where they meet them. The
silhouette of the roof stays flat.

## Roof kit pieces

### Frames

All kit pieces share one set of conventions, so pieces from different families line up:

- Units are centimetres; pieces are modelled at real size.
- **Ridge, hip and trim modules are 2 m long** along +X. Butts face -X: lay a run from its
  -X end, `Start` (or `GableStart` / `WallStart` / `HipEnd`) first, then `Cap` modules
  every 200 cm, then the matching end.
- **Ridge pieces**: origin on the ridge line, at the top plane of the field covering.
- **Hip pieces**: +X runs up the hip line, Z points out of the hip. The hip pieces are for a
  regular hip (both facets at the same pitch, 45 degrees in plan).
- **Roof penetrations** (stacks, hoods, vents, chimneys, boots, flues): origin on the roof
  at the piece's centre, the roof rising toward +Y. Stacks and flues stand plumb; hoods and
  box vents sit square to the roof.
- **Gable rake pairs** (`*Rake_Run5`): both rakes of one gable end, for a 5 m run, origin on
  the ridge line at the gable.
- Pick the piece whose `_P<n>` matches your roof pitch (n in 12).

### Shingle roofs

- Ridge: `SM_ShingleRidge_<Kind>_P<n>`, kinds `Cap`, `Vent` (caps raised over a ridge vent,
  louvres showing along both sides), `VentStart` / `VentEnd` (closes the vent run),
  `GableStart` / `GableEnd`, `HipEnd` (starts the ridge where hips meet, with a saddle cap
  over the junction). Slot 0 takes a `MI_ShingleCap_*`, slot 1 a `MI_RidgeVent_*`.
- Hip: `SM_ShingleHip_Start` (ends in a point at the eave corner), `Cap`, `Top` (cut flush
  under the ridge's HipEnd saddle).
- New houses usually have no ridge vent: they use off-ridge vents
  (`SM_OffRidge_Shingle`), one on each facet just below where the hips meet the ridge.
- Stacks (`SM_Stack_RubberBoot` / `LeadSleeve`, 2" and 3"), exhaust hoods (`SM_Cap_Laundry`,
  `SM_Cap_Bath`), turtle vents (`SM_Turtle`, set in pairs 32 cm apart), chimney with
  cricket (`SM_Chimney`).

### Tile roofs

- Ridge and hip caps come in two styles: `Barrel` (half-round) and `Angular` (A-shaped,
  used on flat tile). Ridge kinds as for shingle, plus `WallStart` / `WallEnd` (for a ridge
  that dies into a wall) and `End`.
- Rakes: `SM_TileRake_<Style>_Run5_P<n>`, caps down both gable edges on a white rake board.
- Roof against a wall: `SM_TileWall_Run5_P<n>`, a flashing leg up the wall on each facet.
- Lead pans (`SM_TilePan_*`), tile-profile vents (`SM_TileVent_*`) and round hoods
  (`SM_TileHood_Round_*`) are fitted to the tile shapes, so they only sit right on a tile
  cell. The free companion plugin **[Florida Roofs Tile Snap](tile-snap.html)** places them for you: drop
  the pieces roughly where you want them, select them, and choose **Tools > Florida Roofs
  > Snap Tile Pieces to Roof** (or the same entry on the right-click menu). Each piece
  moves to the nearest tile cell of the roof under it, turns to face up the slope, and
  switches to the mesh for that roof's pitch. Undo works. The roof must have WorldAligned
  ticked; the Output Log says what was done to each piece. Without the plugin, place them
  by hand: the showcase's tile roofs have every piece snapped, to copy from. (Fab content
  packs cannot contain scripts, so the tool is a separate plugin.)
- Chimney with a tile cricket: `SM_Chimney_Tile`.

### Metal roofs

- Standing seam: `SM_MetalRidge_<Cap|CapRust|GableStart|GableEnd>`, `SM_MetalHip_<Cap|CapRust>`,
  `SM_MetalRake_Run5`, `SM_MetalEave`, boots (`SM_MetalBoot_Round` / `Square`, 2" and 3")
  and a gas flue (`SM_MetalFlue`). Place boots and flues in a pan, between seams (seams
  every 16").
- 5V crimp and rib: `SM_5V*` / `SM_Rib*` ridge rolls and flat rake trim, and
  `SM_Metal5VBoot_*` / `SM_MetalRibBoot_*` / `*Flue`, seated on those panels' flats. Use
  the `CapRust` modules among plain `Cap` ones for the occasional rusted screw.
- 5V and rib eaves show the cut panel ends, so each module's crimps have to line up with
  the field's. The modules are whole crimp steps long: `SM_5VEave_30cm` (one step,
  30.48 cm) and `SM_5VEave_183cm` (six steps); `SM_RibEave_41cm` (40.64 cm) and
  `SM_RibEave_203cm` (five steps). Start the run where the field's crimp grid starts (with
  WorldAligned, at the roof actor's pivot along the eave) and lay modules end to end,
  long ones first, then single steps. For the opposite eave, turn the same module 180
  degrees. Metal roofs are laid in whole panels, so make the eave length a whole number
  of steps; any remainder is left bare.

### Kit materials

Kit meshes use named slots (Boot, Pipe, Lead, Hood, Body, Flange, Stucco, Mortar,
Flashing, Sealant, Rust ...). Each slot starts with a finish from `MI_Kit_*`; swap the
paint finishes to match the roof (in Florida, vents and hoods are usually painted to match
the shingle or left galvanized). Slots that are clad in the covering itself (`Field` on the
chimney's cricket, the tile pieces) take the covering's instance.

## Lighting and performance

- **Project settings.** With Lumen, turn on **Generate Mesh Distance Fields** (Project
  Settings > Rendering; new desktop projects have it on). Without it Lumen has nothing to
  trace and the viewport says so in red. The showcase's sun and sky light are Movable, so
  there is no lighting to build.
- **Valley bands.** The cut-tile band and the tile ridge meshes of the valley roofs have
  **Affect Distance Field Lighting** off on their actors. Keep it off if you place them
  yourself: their distance fields are too coarse for hundreds of thin overlapping tiles,
  and the sky light's distance field occlusion draws dark shards across the valley.
- The materials were checked both with Lumen and without it (screen-space reflections,
  no dynamic GI). The look is practically the same. Keep a Sky Light in the level:
  bare metal reflects the sky, and without one it reads too dark.
- The wear map is stored uncompressed (compression smears the per-granule loss), so each
  covering uses more memory than a standard texture set.
- Kit meshes are Nanite (the import default) and have no hand-made LODs; Unreal builds
  fallback meshes for platforms without Nanite. Every kit mesh has simple collision (one
  convex hull).
- Parallax costs 12-48 texture reads per pixel. For distant roofs, make an instance with
  `ParallaxMaxSteps` lowered, or `ParallaxDepth` 0.

## Known limits

- Hip pieces are for regular hips (equal pitches). Irregular hips are not included.
- The roof's silhouette is flat: the tile relief is parallax, not geometry.
- The tile snap tool works on WorldAligned roofs only.
- Damage states (broken and slipped tile, storm damage) are not in this release.
