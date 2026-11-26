<div align="center">

# ◈ KAGE

**Keyframe Atlas & Grid Engine**

Atlas packer · Offset studio · Animation preview · Multi-engine exporter · Senki XML tooling

![version](https://img.shields.io/badge/release-0.9.0-E11D5F?style=for-the-badge&labelColor=0B0D12)
![windows](https://img.shields.io/badge/Windows-10%2F11%20x64-22D3EE?style=for-the-badge&labelColor=0B0D12)
![android](https://img.shields.io/badge/Android-APK-34D399?style=for-the-badge&labelColor=0B0D12)
![theme](https://img.shields.io/badge/theme-crimson-9E1244?style=for-the-badge&labelColor=0B0D12)
![lang](https://img.shields.io/badge/UI-ID%20%7C%20EN%20%7C%20%E4%B8%AD%E6%96%87-FBBF24?style=for-the-badge&labelColor=0B0D12)

Concept, UI/UX, render architecture, atlas packer & offset studio by **Fann Isnnd**

</div>

---

## ▦ What is KAGE

KAGE turns a folder of loose sprite frames into a **production-ready spritesheet plus the exact manifest your engine expects**. It is built for 2D developers and game modders who need pixel-exact atlases, correct pivots, and engine-specific metadata — without hand-editing `.plist` files.

Everything runs locally. The desktop viewer is GPU-accelerated with automatic CPU fallback. No cloud upload, no account needed for the packing itself.

```csv
pillar,what_it_means
Pixel-exact,Straight-alpha preserved byte-for-byte; soft glow never collapses
Truly minimal sheet,Auto Size searches the SMALLEST canvas via real bounding-box fixpoint
Engine-aware,cocos2d plist f2/f3 · JSON Hash/Array · Unity · Godot 4
Modder tooling,Senki XML V1/V2 generator · frame coverage checker · atlas splitter
Offline-first,All processing on-device; network only for license activation
```

---

## ◈ Interface at a Glance

```text
┌───────────────────────────────────────────────────────────────────────────────┐
│ ◈ KAGE    0/0 frame · atlas — · engine —       Tema  Bahasa  Load  Pack  Export │
├─────────────┬─────────────────────────────────────────────────┬───────────────┤
│  ▦ Packer   │  SHEET  UTIL  FRAMES  MISSING  ROTATED  SHARED   │  Viewport     │
│  ⊹ Offset   │  ──────────────────────────────────────────────  │  ───────────  │
│  ▶ Animation│  ✓  preflight banner — all frames fit            │  Zoom    100% │
│  ≡ Export   │  ┌───────────────────────────────────────────┐   │  Engine  Auto │
│  ✦ Senki XML│  │                                           │   │  Filter  Auto │
│  ✧ Tools    │  │             ATLAS VIEWPORT                │   │  Backdrop Void│
│  ◈ About    │  │      GPU mipmapped  /  CPU tiled LOD      │   │  Checker  ON  │
│             │  │                                           │   │  Outlines ON  │
│  0 frame    │  └───────────────────────────────────────────┘   │  Grid     OFF │
│  0 action   │  ◀   Page 1 / 1   ▶    page thumbnails           │  Inertia  ON  │
│ ┌─────────┐ │                                                  │               │
│ │ TIME &  │ │                                                  │   minimap ▣   │
│ │ LICENSE │ │                                                  │               │
│ └─────────┘ │                                                  │               │
├─────────────┴─────────────────────────────────────────────────┴───────────────┤
│ Ready                            60 paint/s · 0.42 ms     ▰▰▰▰▱▱▱▱   12:34:56  │
└───────────────────────────────────────────────────────────────────────────────┘
```

```csv
region,role
Header,Brand · live chips (frames / atlas / engine) · theme · language · load · pack · export
Sidebar,7 views · session counters · project name · Time & License card
Stat strip,SHEET · UTIL · FRAMES · MISSING · ROTATED · SHARED · ALGO
Banner,Preflight verdict before you commit to a pack
Viewport,Checkerboard · pixel grid · frame outlines · labels · HUD · minimap
Right dock,Live render tuning (zoom / engine / filter / cache / VRAM / overlays)
Status bar,State · paint rate · progress · local clock
```

---

## ⚡ Feature Map

```csv
view,glyph,primary_job
Atlas Packer,▦,Trim · dedupe · rotate · pack into the smallest multi-page atlas
Offset Studio,⊹,Measure pivots per-action or per-frame · batch · presets
Animation,▶,Play the action with ground + anchor guides · reorder frames
Export & Plist,≡,Pick target engine · live manifest preview · write files
Senki XML,✦,Generate V1/V2 skill XML alongside PNG + manifest
Senki Tools,✧,Plist→XML · Cek Frame · SplitSheet
About,◈,Build info · credits · config folder
```

### ▦ Atlas Packer

```csv
feature,detail
Algorithms,10 rectpack strategies (MaxRects / Skyline / Guillotine) + Optimal mode that tries them all
Auto Size,Bounding-box fixpoint + 7 aspect ratios — shrinks the canvas instead of inflating it
Multi-page,1..512 pages; EVERY page cropped to its own content bbox
Rotation,Optional 90° rotation for tighter packing
Trim,Alpha-bbox trim with correct sourceColorRect / spriteSourceSize metadata
Dedupe,Identical-frame sharing keyed on pixel digest + trim geometry + source size
Preflight,Fit check before packing; MISSING frames reported with a colored banner
Tighten,One click: enable Trim and repack for the densest sheet
Disk cache,Keyed on parameters + file size/mtime; auto-trimmed at 3 GB
Adaptive effort,Auto-reduces search depth above 120 / 300 frames to keep the UI responsive
Limits,Padding 0..512 · auto-size cap 16384 px · optional power-of-two rounding
```

### Viewport / Render

```csv
feature,detail
GPU backend,OpenGL 3.3 core · one mipmapped texture · checkerboard computed in GLSL
CPU backend,LOD pyramid + 512 px tile LRU cache
Auto fallback,Degrades on driver / VRAM limits and recovers at runtime without crashing
Zoom,0.4% .. 12800% · smooth zoom · zoom-to-cursor · Fit / 1:1 / zoom-to-frame
Pan,Inertia · minimap navigator · click or drag to jump
Outline colors,Violet = normal · Amber = rotated · Cyan = shared
Tuning,Filter Auto/Nearest/Linear · mip sharpness · zoom smoothing · tile RAM · VRAM budget
Backdrops,Void / Ink / Plum / Slate / Wine
Extras,Viewport snapshot to PNG · live paint/s and ms · multi-page thumbnail strip
```

### ⊹ Offset Studio

```csv
feature,detail
Measure box,8 drag handles + move · arrow-key nudge 1 px (Shift = 10 px)
Formula,"X = (R - L) / 2 ; Y = -B"
Helpers,Auto BBox · Reset · onion skin of the next frame at 35%
Modes,Per-Action (all frames) and Per-Frame (individual) — fully synchronized
Resolution,frame offset > action offset > engine default — identical in both modes
Anchors,9 presets · top-left and Unity bottom-left conventions
Batch,Apply to every action / frame of the same size with preview + confirmation
Presets,Save / apply / delete · stores action + frame offsets and measure boxes
Variants,One action name with mixed frame sizes is split into size variants automatically
Undo,Every offset / preset / batch / delete / clear action is undoable
```

### ▶ Animation Preview

```csv
feature,detail
Playback,Play / Pause / Prev / Next · FPS 1..60 · Loop · Onion
World canvas,Union bbox of all frames positioned by pivot + offset, with margin
Guides,Teal ground line · amber dashed anchor line
Timeline,Thumbnail strip · drag to reorder · click to jump
```

### ≡ Export

```csv
key,label,manifest,helper,typical_target
cocos2d_f2,cocos2d plist (format 2),1 .plist per PNG,—,cocos2d-x / Cocos Creator 2
cocos2d_f3,cocos2d plist (format 3),1 .plist per PNG,—,cocos2d-x modern
json_hash,JSON Hash (TexturePacker),1 .json per PNG,—,Phaser / PixiJS
json_array,JSON Array (TexturePacker),1 .json per PNG,—,Phaser / PixiJS / generic
unity,Unity (JSON + C# helper),1 .json for all pages,KageAtlas.cs,Unity 2021+
godot,Godot 4 (JSON + GDScript helper),1 .json for all pages,kage_atlas.gd,Godot 4
```

```csv
option,detail
PNG compression,0..9
Live preview,Manifest updates as you change options · XML / JSON syntax highlighting
Naming,base.png / base_0.png / base_1.png … — references always follow the live base name
Warnings,Missing frames reported and excluded · rotation warnings for Unity / Godot
Extras,Copy manifest to clipboard · open output folder
```

### ✦ Senki XML

```csv
feature,detail
Versions,V1 (unit / action name / f / e) and V2 (animation / action value / frameName / eventName)
Grouping,Actions derived automatically from frame-name prefix + index
Events,setDelay / setAttackBox / setCommand / setChargeB / setMove
Attack types,ac_hit / n_hit / o_hit / f_hit / l_hit / bl_hit / ab_hit / c_hit
Commands,setInvincible / reInvincible / findTarget / setTransport
Skill filter,Movement actions (idle / walk / run / hurt / float / jump / …) receive no events
Stats block,data (V1) / date (V2): attackType / attackValue / attackRangeX / attackRangeY / cd
Per-action plan,Events before first frame / after last frame / per frame · multi-value setCommand
Editors,Edit Stats Action and Edit Event per Action dialogs with frame preview + Play
Output,One .xml written alongside PNG + manifest on Export
```

### ✧ Senki Tools

```csv
tab,purpose,input,output
Plist → XML,Build one XML from many plists without loading a session,2+ .plist / .json (+ optional atlas PNG),combined XML + live preview
Cek Frame,Verify a skill XML against your frames,XML + plist(s) or the active project,total / unique / found / missing / unused / coverage% + report
SplitSheet,Rebuild individual frames from an existing atlas,PNG + .plist / .json,PNG files in an output folder
```

```csv
capability,detail
Format detection,cocos2d format 0/1/2/3 · JSON Hash · JSON Array · binary plist · XML plist
Rotation conventions,unrotated (rect stores pre-rotation size) or atlas (rect already atlas-space)
Trim,Reconstructs the original source canvas including transparent padding
Independence,SplitSheet writes files only — it does NOT auto-load into Atlas Packer
Feedback,Progress ring · per-frame log · contact sheet · Open Folder
```

---

## 🚀 How to Use

### A · Folder of frames → engine-ready atlas

```csv
step,do_this,where,you_should_see
1,Launch KAGE and sign in,Gate dialog,Main window opens
2,Load your frames,Header > Load Folder (or drag a folder in),Frame list filled; preflight banner shows the fit result
3,Check packing options,Left panel > Packer Options,Auto Size ON is recommended
4,Pack,Header > Pack Atlas (Ctrl+P),Atlas appears with live stats
5,Inspect,Wheel = zoom · drag = pan · double-click = fit,Outlines and labels if enabled
6,Pick export format,Export & Plist > Format Ekspor,Live manifest preview on the right
7,Set output folder + base name,Export & Plist,Target folder and file name
8,Export,Header > Export (Ctrl+E),PNG + manifest (+ helper / + XML) written
9,Open the result,Export & Plist > Buka Folder,File manager opens the output folder
```

### B · Fixing pivots and offsets

```csv
step,do_this,where,note
1,Open Offset Studio,Sidebar ⊹,Action list on the left
2,Pick an action,Action list,First frame loads in the measure editor
3,Choose mode,Right panel > Mode Offset,Per-Action = one offset for all frames; Per-Frame = individual
4,Adjust the box,Drag handles or type Space L / R / B,Offset display shows the resulting X and Y
5,Apply,Terapkan ke Action,Per-Action apply resets that action's per-frame overrides (Undo restores them)
6,Reuse,Batch ke ukuran sama,Applies to every action / frame of identical size
7,Save for later,Preset Offset > Simpan,Stores both modes; apply it to another project anytime
8,Verify,Animation ▶,Ground line and anchor line show the pivot visually
```

### C · Rebuilding frames from an existing atlas

```csv
step,do_this,where,note
1,Open Senki Tools,Sidebar ✧,Three tabs
2,Go to SplitSheet,Third tab,
3,Select the atlas PNG,PNG / atlas field,
4,Select the manifest,Plist / JSON field,.plist (XML or binary) or .json
5,Choose format + rotation,FORMAT section,Auto (detect) + unrotated fits most KAGE / TexturePacker output
6,Choose output folder,OUTPUT section,Leave empty to use <manifest>_split_frames
7,Split,Split Sheet button,PNG files are written; contact sheet appears
8,Open the folder,Buka Folder,Files are NOT loaded into Atlas Packer
9,Optional: pack them again,Header > Load Folder,Point it at the split output folder
```

### D · Generating a Senki skill XML

```csv
step,do_this,where,note
1,Load frames or add plists,Load Folder / Senki Tools > Plist → XML,Session frames or plist-only both work
2,Open Senki XML,Sidebar ✦,
3,Turn it ON,Ikut saat export = ON,XML will be written on Export
4,Pick version,Versi XML,V1 for older clients; V2 for newer
5,Configure events,SetDelay / SetAttackBox,The skill-only filter is applied automatically
6,Fine-tune per action,Edit Stats Action / Edit Event per Action,Click a frame row to see it; press Play to animate
7,Check coverage,Senki Tools > Cek Frame,Choose XML + comparison source then Analyze / Scan
8,Export,Header > Export,PNG + manifest + .xml in the output folder
```

### Keyboard shortcuts (desktop)

```csv
keys,action
Ctrl+O,Open project
Ctrl+S,Save project
Ctrl+P,Pack / refresh atlas
Ctrl+E,Export
Ctrl+F,Focus frame search
Ctrl+comma,Settings (theme / language / font)
Space,Play / pause (Animation viewport focused)
0,Fit to view (viewport focused)
1,Zoom 100% (viewport focused)
plus / minus,Zoom in / out (viewport focused)
Arrow keys,Pan viewport / nudge measure box 1 px
Shift+Arrow,Nudge measure box 10 px
Delete,Delete selected frames (undoable)
Double-click,Rename frame (frame list) / Fit (viewport)
```

---

## 📱 Android

The Android build shares the **same pure-Python core** as the desktop version, so packing geometry, trimming, dedupe, offset resolution, export manifests and Senki XML output are produced by identical code paths.

```csv
aspect,android
Distribution,APK — sideload (enable "Install unknown apps")
Core engine,Shared kage_core: packer · imaging · offsets · formats · senki
Theme,Material 3 · crimson seed · dark / light
Interaction,Touch — pinch zoom, drag pan, tap to select
Session,Project save / load and autosave on device storage
```

```csv
step,do_this
1,Download the APK from Releases
2,Allow installation from your browser / file manager
3,Install and launch KAGE
4,Sign in (internet required on first activation)
5,Pick your frame folder / files
6,Pack, tune offsets, then Export
7,Find the output in your chosen folder
```

> Desktop remains the reference build for the OpenGL viewport, multi-window Senki editors and multi-page thumbnail strip.

---

## 🎨 GUI Theme

Six curated presets plus a fully custom accent. Every token is generated from one HSV seed, so the whole interface stays consistent — and switches live without restart.

```csv
theme,accent_hue,base,label
crimson,347,dark,Crimson · Merah
purple,265,dark,Purple · Ungu
green,152,dark,Emerald · Hijau
blue,212,dark,Azure · Biru
amber,42,dark,Amber · Kuning
light,212,light,Light · Putih
custom,0..359,dark or light,Custom accent
```

**Crimson token reference** — the palette the screenshots use:

```csv
token,hex,used_for
BG,#0B0D12,Window background
CANVAS,#0A0C10,Viewport backdrop (Void)
INSET,#0E1117,Inputs · lists · code panels
SURF_TOP,#151A24,Card gradient top
SURF_BOT,#111520,Card gradient bottom
BORDER,#293042,Card and input borders
BORDER_HI,#3A4358,Hover / focus borders
TEXT,#ECEFF5,Primary text
MUTED,#98A1B5,Secondary text
FAINT,#757F95,Section headers · hints
VIOLET,#E11D5F,Primary accent
VIOLET_L,#FF5C8A,Accent highlight · outline (normal)
VIOLET_D,#9E1244,Accent pressed · selection
MAGENTA,#FF4D77,Gradient companion
FUCHSIA,#FF3D8A,Measure box stroke
TEAL,#F97276,Secondary accent · ground line
CYAN,#22D3EE,Focus ring · shared-frame outline
AMBER,#FBBF24,Rotated-frame outline · anchor line
SUCCESS,#34D399,Preflight OK · measured marker
DANGER,#FF6B6B,MISSING · errors
INFO,#7DA2E8,Informational
```

```csv
setting,range,effect
UI font size,5..17 px,Live preview; layout guards keep text from clipping
UI font,auto-picked,Segoe UI Variable / Segoe UI / Inter / Noto Sans …
Mono font,auto-picked,Cascadia Mono / Consolas / JetBrains Mono …
Language,ID / EN / 中文(简体),Applies to menus, dialogs, tabs and table headers
```

---

## 📦 Requirements

```csv
item,desktop,notes
OS,Windows 10 / 11 x64,No installer — single executable
CPU,Any x64,More cores = faster packing
RAM,4 GB,8 GB+ recommended for large atlases
GPU,OpenGL 3.3 capable,Optional — CPU renderer is used automatically otherwise
Disk,~200 MB,Plus pack cache (auto-trimmed at 3 GB)
Admin rights,Not required,
Network,First sign-in only,Offline grace period afterwards
```

```csv
runtime_path,purpose
%USERPROFILE%\.kage\settings.json,Theme / language / font / last folders
%USERPROFILE%\.kage\license.dat,Signed license cache (device-bound)
%USERPROFILE%\.kage\remember.dat,Encrypted saved credentials (Windows DPAPI)
%USERPROFILE%\.kage\offset_presets.json,Your offset presets
%USERPROFILE%\.kage\autosave.kage,Crash-safe session autosave
%USERPROFILE%\.kage\cache\,Pack result cache
%USERPROFILE%\.kage\error.log,Handled errors
%USERPROFILE%\.kage\crash.log,Native crash dump
```

---

## 🔐 Activation

```csv
topic,behavior
First sign-in,Internet connection required
Afterwards,Works offline during the grace period
Binding,A license / key is bound to one device
New device,Ask the seller for a device / HWID reset
Credentials,Stored encrypted, bound to the device
Expired,Read-only mode: opening and exporting existing projects still works; loading new frames is locked
Sign out,"Hapus kredensial tersimpan" in the gate dialog
```

---

## ⚠ Known Limitations

```csv
topic,detail
Unity / Godot rotation,Runtime helpers do not rotate sprites — turn OFF Allow Rotation for these targets
Missing frames,Frames that do not fit are excluded from export and reported
Max texture,An atlas larger than your GPU limit automatically uses the CPU renderer
Auto-size cap,16384 px per side
Senki stats,Movement actions intentionally have no stats block
Android viewport,Touch image viewer, not the desktop OpenGL pipeline
```

---

## 📄 License & Credits

```csv
item,detail
Repository license,BSL-1.0 (see LICENSE)
Binaries,KAGE executable and APK — original work by Fann Isnnd
Attribution,Required — do not claim authorship or remove the author name
Source,Not distributed; this repository publishes binaries and documentation only
```

**KAGE — Keyframe Atlas & Grid Engine**
Concept, UI/UX design, render architecture, atlas packer and offset studio by **Fann Isnnd**.

Built with Python · PySide6 · rectpack · Pillow · Flet.

<sub>Original work. Please do not claim authorship, remove credit, or redistribute the binaries without attribution.</sub>
