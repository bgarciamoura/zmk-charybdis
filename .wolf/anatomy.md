# anatomy.md

> Auto-maintained by OpenWolf. Last scanned: 2026-07-08T16:06:08.233Z
> Files: 89 tracked | Anatomy hits: 0 | Misses: 0

## ../../../../mnt/c/Users/Public/

- `dongle-capture.ps1` (~386 tok)

## ../../../../tmp/

- `install-docker.sh` — Docker Engine + Compose v2 install for Ubuntu 24.04 (noble), WSL2. (~618 tok)

## ../../.claude/

- `settings.json` (~43 tok)
- `statusline-command.sh` — Claude Code statusLine command (~575 tok)

## ../../.claude/projects/-home-bgarciamoura-projects-zmk-charybdis/memory/

- `charybdis_hardware_setup.md` — Composição da montagem (~1231 tok)
- `MEMORY.md` — Memory Index (~230 tok)
- `nrf52840_supermini_pinout.md` — Identificação (~1579 tok)
- `zmk_pmw3360_modules.md` (~476 tok)
- `zmk_split_ble_findings.md` — Como ZMK split realmente pareia (~842 tok)

## ./

- `.gitignore` — Git ignore rules (~170 tok)
- `build.yaml` — Build matrix describing every board/shield/keymap combo to build. (~1646 tok)
- `CLAUDE.md` — OpenWolf (~1607 tok)
- `KEYMAP_EDITING.md` — Referência de quais arquivos editar pra cada tipo de mudança no keymap (bindings, behaviors, combos, macros, trackball, layout físico). Inclui layer indices canônicos (BASE 0 / NUM 1 / NAV 2 / SYM 3 / GAME 4 / EXTRAS 5 / SLOW 6 / SCROLL 7), key positions e fluxo de build. (~2348 tok)
- `README.md` — Project documentation (~2845 tok)
- `TRACKBALL_MOD.md` — Passo-a-passo do mod PMW3360 + Bastardkb Elite-C Holder 2.1 stock + nice!nano: jumper CS sensor→P0.20, troca driver pra george-norton/zmk-driver-pmw3360, polled mode. **Histórico — usuário migrou pra PMW3610.** (~3059 tok)
- `TRACKBALL_PMW3610.md` — Guia ATIVO: setup PMW3610-Module (chinês 32mm com LDO 2.0V) + Bastardkb Elite-C Holder 2.1 stock + nice!nano. Pinout J8 completo, 3 jumpers diretos (VDDIO+VDD→VCC, NCS→D3/P0.20, MOT→D0/P0.06), pinctrl SCK=P1.13/SDIO=P0.10. Troubleshooting + apêndice histórico. (~2804 tok)

## .claude/

- `settings.json` (~441 tok)

## .claude/rules/

- `openwolf.md` (~313 tok)

## .github/workflows/

- `build.yml` — CI: Build and Release ZMK Firmware (~4303 tok)
- `draw_keymaps.yml` — CI: Draw keymaps (~2522 tok)

## boards/shields/charybdis_common/

- `charybdis.dtsi` — include <dt-bindings/zmk/matrix_transform.h> (~367 tok)
- `Kconfig.bt.defconfig` (~60 tok)
- `Kconfig.dongle.defconfig` (~68 tok)
- `Kconfig.reset.defconfig` (~56 tok)

## boards/shields/charybdis_dongle/

- `charybdis_dongle.conf` — # Split keyboards (~469 tok)
- `charybdis_dongle.overlay` — Documentation: https://zmk.dev/docs/development/hardware-integration/dongle (~915 tok)
- `Kconfig.defconfig` (~15 tok)
- `Kconfig.shield` (~22 tok)

## boards/shields/charybdis_left_bt/

- `charybdis_left_bt.conf` (~9 tok)
- `charybdis_left_bt.overlay` — include "../charybdis_common/charybdis.dtsi" (~163 tok)
- `Kconfig.defconfig` (~14 tok)
- `Kconfig.shield` (~23 tok)

## boards/shields/charybdis_left_dongle/

- `charybdis_left_dongle.conf` (~20 tok)
- `charybdis_left_dongle.overlay` — include "../charybdis_common/charybdis.dtsi" (~163 tok)
- `Kconfig.defconfig` (~15 tok)
- `Kconfig.shield` (~25 tok)

## boards/shields/charybdis_right_bt/

- `charybdis_right_bt.conf` — # Split keyboards (~387 tok)
- `charybdis_right_bt.overlay` — include "../charybdis_common/charybdis.dtsi" (~274 tok)
- `Kconfig.defconfig` (~14 tok)
- `Kconfig.shield` (~24 tok)

## boards/shields/charybdis_right_dongle/

- `charybdis_right_dongle.conf` (~420 tok)
- `charybdis_right_dongle.overlay` — include "../charybdis_common/charybdis.dtsi" (~287 tok)
- `Kconfig.defconfig` (~15 tok)
- `Kconfig.shield` (~26 tok)

## boards/shields/charybdis_trackball/

- `charybdis_pmw3610.dtsi` (~679 tok)

## boards/zephyr/

- `module.yml` (~11 tok)

## config/

- `charybdis_zmk.yml` (~106 tok)
- `charybdis-layouts.dtsi` — include <physical_layouts.dtsi> (~980 tok)
- `qwerty.json` (~1500 tok)
- `west.yml` (~122 tok)

## config/charybdis/

- `charybdis_left.conf` (~28 tok)
- `charybdis.conf` — # Bluetooth (~303 tok)

## config/dongle_prospector/

- `dongle_prospector_common.conf` — # Shared Prospector dongle settings for the nice!nano-based stacked build. (~318 tok)
- `dongle_prospector_no_sensor.conf` — # Prospector dongle variant for hardware without the APDS9960 ambient light sensor. (~46 tok)
- `dongle_prospector_no_sensor.overlay` (~21 tok)
- `dongle_prospector_sensor.conf` — # Prospector dongle variant for hardware with the APDS9960 ambient light sensor fitted. (~36 tok)

## config/dongle_prospector_layouts/

- `dongle_prospector_layout_classic.conf` — # Prospector status screen layout: Classic. (~24 tok)
- `dongle_prospector_layout_field.conf` — # Prospector status screen layout: Field. (~23 tok)
- `dongle_prospector_layout_operator.conf` — # Prospector status screen layout: Operator. (~24 tok)
- `dongle_prospector_layout_radii.conf` — # Prospector status screen layout: Radii. (~41 tok)

## config/dongle_prospector_themes/

- `dongle_prospector_theme_blue.overlay` (~56 tok)
- `dongle_prospector_theme_green.overlay` (~40 tok)
- `dongle_prospector_theme_purple.overlay` (~40 tok)
- `dongle_prospector_theme_red.overlay` (~40 tok)

## config/dongles/

- `prospector.overlay` (~0 tok)
- `standard.overlay` (~0 tok)

## config/keymap_features/

- `behaviors.dtsi` — define KEYS_L 0 1 2 3 4 5 12 13 14 15 16 17 24 25 26 27 28 29 36 37 38  // Left-hand keys. (~2548 tok)
- `combos.dtsi` — ╭──────┬──────┬──────┬──────┬──────┬──────╮  ╭──────┬──────┬──────┬──────┬──────┬──────╮ (~673 tok)
- `macros.dtsi` (~2222 tok)

## config/keymaps/

- `canary.keymap` — include <behaviors.dtsi> (~2299 tok)
- `colemak_dh.keymap` — include <behaviors.dtsi> (~2299 tok)
- `focal.keymap` — include <behaviors.dtsi> (~2299 tok)
- `graphite.keymap` — include <behaviors.dtsi> (~2299 tok)
- `qwerty.keymap` — include <behaviors.dtsi> (~3411 tok)

## config/trackball/

- `charybdis_pointer.dtsi` — include <input/processors.dtsi> (~208 tok)

## firmwares/

- `.gitignore` — Git ignore rules (~25 tok)

## keymap-drawer/

- `README.md` — Project documentation (~1255 tok)

## keymap-drawer/configs/

- `config-all-layers.yaml` (~2631 tok)
- `config-combo.yaml` (~1046 tok)
- `config-stacked.yaml` (~3164 tok)

## keymap-drawer/stacked/

- `composite-template.html` — Declares html (~301 tok)
- `legend-1x1.yaml` (~25 tok)

## local-build/

- `build_setup.sh` — build_zmk_locally.sh - Build ZMK firmware locally based on the matrix created from build.yaml (~3960 tok)
- `docker-compose.yml` — Docker Compose services (~82 tok)
- `README.md` — Project documentation (~730 tok)

## scripts/

- `keymap_converter.py` — URL configuration (~2778 tok)
- `layouts.py` (~670 tok)
- `make_stacked.py` — load_yaml, flatten, resolve, make_stacked_key + 2 more (~1144 tok)
- `render_stacked_composite.js` — Composite keymap renderer (Playwright). (~2927 tok)
