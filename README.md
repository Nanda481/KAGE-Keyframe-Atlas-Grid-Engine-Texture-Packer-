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
<img width="1440" height="900" alt="Screenshot (1950)" src="https://github.com/user-attachments/assets/f62663c3-d59c-40d7-8d8c-88e6fe7b4d8c" />


## Sign in — free account


Username:
``` KAGEfree ```
Password:
``` kage123 ```

First sign-in,Internet connection required
Afterwards,Works offline during the grace period

Donation for Dev
Dana:  ``` 085960290154 ```
Ovo:   ``` 085960290154 ```

Contact Whatsapp:   ``` 085960290154 ```
Contact email:      ``` Faniisnanda@gmail.com ```

Official Youtube Channel Developer: https://www.youtube.com/@fani_isnanda

# KAGE

**Keyframe Atlas & Grid Engine** — atlas packing, pivot measurement, animation preview, and multi-engine export for 2D game modders.

KAGE turns a folder of loose sprite frames into a production-ready spritesheet **plus the exact manifest your engine expects**. It measures character pivots for you, previews every action as an animation, and writes cocos2d plist, TexturePacker JSON, Unity, Godot, and Senki XML in a single pass. All processing runs locally on your machine.

Available for **Windows** and **Android** · current release **0.9.0**

---

## Modules

| Module | What it does |
|---|---|
| **Atlas Packer** | Trims transparent padding, shares identical frames, rotates and packs frames into the smallest possible sheet. Multi-page output, each page cropped to its own content. |
| **Offset Studio** | Detects the character body with Auto BBox, computes the pivot offset, and writes it straight into the manifest. Per-action or per-frame, with batch apply and reusable presets. |
| **Animation Preview** | Plays each action (idle, hurt, nAttack, skill 1–5) with ground and anchor guides, adjustable FPS, onion skin, and drag-to-reorder timeline. |
| **Export & Plist** | Picks the target engine, shows the manifest live as you change options, then writes PNG + manifest + runtime helper. |
| **Senki XML** | Generates V1 and V2 skill XML alongside your atlas, with per-action stats blocks and event plans. |
| **Senki Tools** | Plist → XML converter, frame coverage checker, and SplitSheet for rebuilding individual frames from an existing atlas. |
| **Settings** | Six curated themes plus a custom accent, three interface languages, and adjustable UI typography. |

---

## Highlights

### Packing that actually minimizes

- **Auto Size** searches for the smallest canvas using real bounding-box measurement across several aspect ratios — it shrinks the sheet instead of inflating it.
- **Ten packing algorithms** (MaxRects, Skyline, Guillotine) plus an **Optimal** mode that tries them all and keeps the densest result.
- **Preflight check** runs as soon as frames are loaded, reporting how many frames fit and which ones are missing before you commit to a pack.
- **Identical-frame sharing** keyed on pixel content *and* trim geometry, so frames with different padding never overwrite each other's metadata.
- **Straight-alpha preserved byte-exact.** Soft glow and semi-transparent pixels survive packing, splitting, and preview without collapsing.
- Multi-page up to 512 sheets, padding 0–512 px, optional power-of-two rounding, and a 16384 px ceiling.

### Offset Studio — no more hand-written plist values

- **Auto BBox** finds the character body from the alpha channel and sets the measurement box automatically.
- Offset is computed as **X = (R − L) / 2** and **Y = −B**, then written directly into the exported manifest.
- Drag the box handles or type the left / right / bottom spacing; nudge with arrow keys (1 px, or 10 px with Shift).
- **Per-Action** and **Per-Frame** modes stay synchronized — switching modes never changes the exported result.
- **Batch apply** to every action or frame of identical size, with a preview list and confirmation.
- **Presets** store both modes and measurement boxes, so a measured character can be reused on another project.
- Nine anchor presets, including Unity's bottom-left convention. Every offset change is undoable.

### Viewer built for large atlases

- **GPU path:** OpenGL 3.3 with a single mipmapped texture and a shader-drawn checkerboard.
- **CPU path:** LOD pyramid with a 512 px tile cache, used automatically when the driver or VRAM cannot handle the atlas.
- Zoom from **0.4% to 12800%** with smooth interpolation, zoom-to-cursor, and pan inertia — no stutter on huge sheets.
- Minimap navigator, frame outlines colour-coded by state, pixel grid, and viewport snapshot to PNG.

### Senki / NARSEN tooling

- **XML generator** for V1 and V2 formats, with setDelay, setAttackBox, setCommand, setChargeB, and setMove.
- **Per-action editors** for stats and events, each with a frame preview and playback so you can see what you are editing.
- **Coverage checker** compares a skill XML against your plists or active project and reports found, missing, and unused frames as a percentage.
- **SplitSheet** rebuilds individual frames from an atlas, auto-detecting cocos2d format 0–3, JSON Hash, JSON Array, and binary plist.

### Interface

- **Six themes** plus a fully custom accent hue, generated from a single colour seed and applied live.
- **Three languages:** Bahasa Indonesia, English, and 简体中文 — including the Senki tooling.
- Adjustable UI font size with live preview, and layout guards that keep text from clipping at any size.
- Project files with atomic save, 60-second autosave, crash recovery, drag-and-drop, and undo throughout.

---

## Export formats

| Format | Output | Runtime helper | Typical target |
|---|---|---|---|
| cocos2d plist (format 2) | one .plist per page | — | cocos2d-x, Cocos Creator 2, Senki |
| cocos2d plist (format 3) | one .plist per page | — | modern cocos2d-x |
| JSON Hash (TexturePacker) | one .json per page | — | Phaser, PixiJS |
| JSON Array (TexturePacker) | one .json per page | — | Phaser, PixiJS, generic |
| Unity | one .json for all pages | KageAtlas.cs | Unity 2021+ |
| Godot 4 | one .json for all pages | kage_atlas.gd | Godot 4 |

Senki XML can be written alongside any of these in the same export.

---

## Installing

### Windows

Download `KAGE.exe` from the [Releases](../../releases) page and run it. No installer, no dependencies, no administrator rights required. Configuration and cache are created automatically in `%USERPROFILE%\.kage`.

### Android

Download the APK from the [Releases](../../releases) page, allow installation from your browser or file manager, then install and launch. The Android build shares the same core engine, so packing geometry, offsets, and manifests match the desktop output.

An internet connection is required on first sign-in; afterwards the app works offline during the grace period.

---

## Requirements

| Item | Minimum | Notes |
|---|---|---|
| OS | Windows 10 x64 | Windows 10 / 11 |
| Memory | 4 GB | 8 GB or more recommended for large atlases |
| Graphics | OpenGL 3.3 capable | Optional — the CPU renderer is used automatically otherwise |
| Storage | ~200 MB | Plus pack cache, trimmed automatically at 3 GB |
| Network | First activation only | Offline afterwards |
| For Android | Android 9.0 or above | 4GB RAM |


---

## Bahasa Indonesia

**KAGE (Keyframe Atlas & Grid Engine)** — tools untuk modder Senki / NARSEN.

- **Texture Packer** mendeteksi ukuran sheet otomatis saat frame dimuat, lalu menyusun atlas terpadat dan menghasilkan plist siap pakai.
- **Offset Studio** mendeteksi tubuh karakter lewat Auto BBox, menghitung **X = (R − L) / 2** dan **Y = −B**, lalu menuliskannya langsung ke plist — tidak perlu mengukur dan menulis manual satu per satu.
- **Animation Preview** memutar tiap action (idle, hurt, nAttack, skill 1–5) lengkap dengan garis ground dan anchor.
- **Export** PNG + plist cocos2d, JSON TexturePacker, Unity, Godot, dan Senki XML dalam satu langkah.
- **Senki Tools**: konversi multi-plist ke XML, cek coverage frame, dan pecah atlas kembali menjadi frame individual.
- **Zoom halus tanpa lag** berkat akselerasi OpenGL (GPU) dengan fallback CPU otomatis.
- **Enam tema + custom accent**, tiga bahasa (Indonesia, English, Mandarin), dan ukuran font yang bisa diatur.

Unduh di halaman [Releases](../../releases). Koneksi internet hanya diperlukan saat aktivasi pertama.

---

## License & credits

Repository files are released under the terms in [LICENSE](LICENSE).

**KAGE — Keyframe Atlas & Grid Engine**  
Concept, UI/UX design, render architecture, atlas packer, and offset studio by **Fann Isnnd**.

Built with Python, PySide6, rectpack, Pillow, and Flet.

Original work. Please do not claim authorship or remove the author credit.


Screenshot Preview. for windows
<img width="1440" height="900" alt="Screenshot (1951)" src="https://github.com/user-attachments/assets/b592fb42-15f1-4849-95ce-12731a343726" />
<img width="1440" height="900" alt="Screenshot (1952)" src="https://github.com/user-attachments/assets/23679e11-5106-47de-a98b-00d490c8aabe" />
<img width="1440" height="900" alt="Screenshot (1956)" src="https://github.com/user-attachments/assets/3b2d82c7-afad-4497-a961-faec2c9aff6a" />

<sub>Original work. Please do not claim authorship, remove credit, or redistribute the binaries without attribution.</sub>
