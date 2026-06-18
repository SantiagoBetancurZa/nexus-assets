# nexus-assets — NEXUS visual-novel asset CDN

Single, deduplicated home for **all** NEXUS visual assets — character sprites, scene
backgrounds, the campus map and endings — organized and labeled so they can be referenced
**by URL from Figma Make** (URL images don't count toward Make's 30-media cap).

- **Machine-readable index:** [`manifest.json`](./manifest.json) (every asset → relative path + full URL + tags).
- **Assumed base URL:** `https://nexus-assets.vercel.app` — if you deploy this repo to a
  different Vercel project/domain, swap the base; all paths below are relative to it.
- **Serving:** pure static. Vercel serves every file as-is from the repo root (no build).

```
characters/{santiago,alejandra,aya}/<character>_<emotion>.png   # transparent sprites
scenes/intro/intro_01..07.png            # opening cutscene (office + city)
scenes/tuesday/tuesday_01..04.png        # Tuesday — library / auditorium (Santiago)
scenes/wednesday/wednesday_01..04.png    # Wednesday — lecture halls (Alejandra)
scenes/thursday/thursday_01..04.png      # Thursday — empty lab/room backgrounds
scenes/thursday/thursday_aya_01..07.png  # Thursday — Aya recruitment cutscene (composited)
scenes/rooms/{classroom,library,lab}.png # standalone room backgrounds
map/campus_map.png                       # isometric campus map
endings/bad_ending.png                   # dramatic bad ending
```

## Use from Figma Make
Reference any asset by `BASE + relative path`, e.g.:

```
https://nexus-assets.vercel.app/characters/aya/aya_idea.png
https://nexus-assets.vercel.app/scenes/wednesday/wednesday_01.png
https://nexus-assets.vercel.app/scenes/thursday/thursday_aya_03.png
https://nexus-assets.vercel.app/map/campus_map.png
```

Sprite emotion labels and per-scene descriptions live in `manifest.json`.

## Provenance / dedup notes
Consolidated from scattered sources under `~/Desktop/00. Make/` and the game's
`campus/public/img/`. Exact-duplicate copies were collapsed to one canonical file:

- **Sprites** = the emotion-labeled set from `Assets personajes/` (same renders the game ships).
- **Aya cutscene** `thursday_aya_*` = the 1920×1080 web exports (`escena_aya_01..07`); the
  hi-res masters (3344×1882) and the 57 MB `.psd` stay in `00. Make/Nueva Escena Aya/` (archival).
- **Day backgrounds** (`tuesday/wednesday/thursday_*`) had repeated frames in the game
  (e.g. frames 3-5 identical) — kept once; see `manifest.json` `desc` for which game slots reuse them.
- **Map**: `MapCanvas.png` (1749×952) chosen over the tighter `campus_map.png` crop (1577×952).
- **Ending**: `escena_fin_malo.png` (web) chosen; `Primer fin del juego/1.png` is its hi-res master.

## Deploy
This is a static asset repo. To publish: connect it to a Vercel project (Framework = Other,
no build command, output = repo root) or run `vercel` from this folder. After deploy, the URLs
above resolve. _Do not deploy/push without the owner's go-ahead._
