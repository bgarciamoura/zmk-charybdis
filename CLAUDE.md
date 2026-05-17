# OpenWolf

@.wolf/OPENWOLF.md

This project uses OpenWolf for context management. Read and follow .wolf/OPENWOLF.md every session. Check .wolf/cerebrum.md before generating code. Check .wolf/anatomy.md before reading files.


# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this repo is

ZMK firmware **config** for the wireless Charybdis 3x6 split keyboard (not application code). The artifacts here are Zephyr device tree (`.dtsi`, `.overlay`, `.keymap`), Kconfig (`.conf`), and a build matrix (`build.yaml`). Builds happen against upstream ZMK pulled in via `config/west.yml`.

Targets three deployment formats from the same sources:
- **bt** — Bluetooth split (left + right halves talk directly)
- **dongle_standard_nano** — split + a USB dongle as central
- **dongle_prospector_*** — dongle with a Prospector display addon (multiple board/sensor/layout variants)

## Common commands

**Local build (Docker, recommended for fast iteration):**
```bash
cd local-build
docker-compose run --rm builder            # builds everything in build.yaml
docker-compose run --rm --entrypoint bash builder   # interactive shell for debugging
```
Output lands in `firmwares/` at the repo root, organized by `format/keymap/`.

**To build only a subset:** edit `build.yaml` and comment out unwanted entries or keymaps before invoking the builder. There is no "build a single shield" flag; selection is driven by `build.yaml`.

**CI build:** `.github/workflows/build.yml` runs the same matrix on push to `main` and on tags (tags also produce a GitHub release with zipped firmware bundles). `.github/workflows/draw_keymaps.yml` regenerates the keymap SVG/PNG renders in `keymap-drawer/` on push to `main`.

**USB logging (battery-costly, off by default):** set `ENABLE_USB_LOGGING="true"` at the top of `local-build/build_setup.sh`. This also disables the `studio-rpc-usb-uart` snippet because both use USB CDC.

## Architecture

### Build matrix is the source of truth
`build.yaml` is consumed by both CI (`.github/workflows/build.yml`, parsed in Python) and the local Docker build (`local-build/build_setup.sh`, parsed with `yq`/`jq`). Any change to build flavors, keymaps, or Prospector overlays must work for both. The two parsers must stay behaviorally aligned — if you change the schema, update both.

Each entry expands to one build per (board × shield × keymap). For Prospector entries, `extra_conf_files` and `extra_dtc_overlay_files` are concatenated with `;` and passed via `-DEXTRA_CONF_FILE` / `-DEXTRA_DTC_OVERLAY_FILE`.

### Custom shields and modules
Custom shields live in `boards/shields/` (not `config/`). They're discovered by ZMK because the build passes `-DZMK_EXTRA_MODULES=$ROOT/boards;$ROOT/zmk-pmw3610-driver;$ROOT/prospector-zmk-module`. `boards/zephyr/module.yml` declares this directory as a Zephyr module with `board_root: ..`.

`config/west.yml` pulls in three projects: upstream `zmk` (main), `zmk-pmw3610-driver` (trackball sensor), and `prospector-zmk-module` (display dongle). All three are required for a full build to succeed.

### Keymap selection mechanic (non-obvious)
ZMK's cmake searches `${ZMK_CONFIG}/${SHIELD}.keymap`. Both the CI workflow and `build_setup.sh` therefore **copy** the requested keymap from `config/keymaps/<name>.keymap` to `config/<target>.keymap` before invoking `west build`. If you add a new keymap, drop it in `config/keymaps/` and add its name under `keymap:` in `build.yaml` — do not create per-shield copies.

### Shared Charybdis Kconfig fragments
`config/charybdis/*.conf` are shared across shields, but ZMK only searches the top-level `${ZMK_CONFIG}` directory (no recursion). Both CI and local build copy these up to `config/` before building. Don't try to `#include` them or reference them with subdirectory paths.

### Stacked shield strings
Prospector entries use a stacked shield string like `"charybdis_dongle prospector_adapter"`. The full string is passed to `-DSHIELD` (Zephyr concatenates the overlays), but the primary token (`charybdis_dongle`) is used for overlay-target discovery in `boards/shields/<primary>/*.overlay`. Both build paths handle this split — preserve it if you touch the build logic.

### `studio-rpc-usb-uart` is auto-applied
Both build paths automatically add `-S studio-rpc-usb-uart` (CI: `-DSNIPPET=studio-rpc-usb-uart`) when the target is `charybdis_right_bt` or `charybdis_dongle` (the USB centrals). It's skipped automatically when USB logging is on. Don't add it manually in `build.yaml`.

### Where customizations belong
- **Trackball behavior** (speed, scroll, precision mode): `config/trackball/charybdis_pointer.dtsi`. Layer overrides in this file reference the SCROLL (7) and SLOW (6) layers — keep these in sync with the layer indices used in keymaps.
- **Combos / macros / behaviors** (HRM, tap-dance, layer-tap variants): `config/keymap_features/{combos,macros,behaviors}.dtsi`. Included by every keymap.
- **Physical layout** (key positions for keymap-drawer and ZMK Studio): `config/charybdis-layouts.dtsi`.
- **Per-keymap layout** (layer order, bindings): `config/keymaps/<name>.keymap`. Layer order is BASE/NUM/NAV/SYM/GAME/EXTRAS/MOUSE/SLOW/SCROLL — many other files reference these by index, so don't reorder lightly.
- **Prospector display variants:** `config/dongle_prospector_layouts/` (operator/classic/radii/field) and `config/dongle_prospector_themes/` (radii-only color overlays). Selection is per build entry in `build.yaml`.

### Settings reset is a special case
`settings_reset` is an upstream ZMK shield, not one of ours. `build_setup.sh` patches its overlay (`rows = <0>` → `<1>`, `events = <>` → `<0>`) to silence a GCC zero-length-array warning. The artifact is published at `firmwares/settings_reset.uf2` (top level, no subfolder) so it shows up plainly in releases.

## Keymap rendering pipeline
The `keymap-drawer` workflow (`draw_keymaps.yml`) auto-commits regenerated diagrams to `keymap-drawer/` on every push to `main`. Don't hand-edit files under `keymap-drawer/stacked/` or `keymap-drawer/all_layers/` — they'll be overwritten. Style/legend tuning lives in `keymap-drawer/configs/*.yaml` and `keymap-drawer/stacked/composite-template.html`. See `keymap-drawer/README.md` for the full breakdown of which file controls what.
