# Local Image Metadata Catalog

Simple local GUI app for browsing generated images and viewing key generation metadata.

## Features
- Select one folder or multiple folders
- Scan images (`png/jpg/jpeg/webp/bmp/tiff`)
- Thumbnail catalog with both vertical and horizontal scrolling
- Adjustable thumbnail size
- Adjustable number of thumbnail columns
- Double-click preview window with full-size image viewing
- Favorites support with star marking
- Custom tags per image
- Search/filter by filename and generation metadata fields
- Sorting: `Newest` / `Oldest` across all selected folders
- Right metadata panel with clean structure:
  - Prompt
  - Negative prompt
  - Model
  - Sampler
  - Scheduler
  - Seed
  - CFG
  - Steps
  - Resolution
  - File size
  - LoRAs

## Install
```powershell
cd "E:\AI code projects\One"
py -m pip install -r requirements.txt
```

## Run
```powershell
cd "E:\AI code projects\One"
py app.py
```

## Build EXE (Windows)
### Option A: Use build script
```powershell
cd "E:\AI code projects\One"
powershell -ExecutionPolicy Bypass -File .\build_exe.ps1
```
- Default builds `onedir` (faster startup, recommended for local use).
- Output: `dist\LocalImageMetadataCatalog\LocalImageMetadataCatalog.exe`

To build single-file EXE:
```powershell
cd "E:\AI code projects\One"
powershell -ExecutionPolicy Bypass -File .\build_exe.ps1 -OneFile
```
- Output: `dist\LocalImageMetadataCatalog.exe`

### Option B: Manual build
```powershell
cd "E:\AI code projects\One"
py -m pip install pyinstaller
py -m PyInstaller --noconfirm --clean --windowed --name LocalImageMetadataCatalog --onedir app.py
```

## Notes
- Metadata is read from `PIL.Image.info` and EXIF.
- Automatic1111 parameters are parsed from the `parameters` block.
- ComfyUI parameters are parsed from the `prompt` JSON graph when available.
- Depending on generator/workflow, some fields may be missing.
- Preview controls:
  - Double-click thumbnail: open full preview
  - Mouse wheel: zoom in/out
  - `+` / `-`: zoom
  - `Ctrl + 0`: reset zoom to 100%
  - `F`: fit image to window
- Catalog filters:
  - Search: filename, prompt, negative prompt, model, sampler, scheduler, seed, CFG, steps, resolution, LoRAs
  - Prompt tag filter: searches inside positive prompt text metadata
  - Favorites only: show only starred images
- Metadata actions:
  - `Copy prompt`: copies positive prompt of selected image
  - `Favorite`: star/unstar selected image
  - `Save tags`: saves comma-separated tags for selected image
- Favorites and tags are stored in `.image_catalog_state.json` next to `app.py`.
- Selected scan folders are restored on next launch and scanned automatically.
- In EXE mode, state is stored next to the `.exe` as `.image_catalog_state.json`.
