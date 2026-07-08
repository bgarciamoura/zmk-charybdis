# Memory

> Chronological action log. Hooks and AI append to this file automatically.
> Old sessions are consolidated by the daemon weekly.

## Session: 2026-05-07 16:37

| Time | Action | File(s) | Outcome | ~Tokens |
|------|--------|---------|---------|--------|
| 16:48 | Created ../../.claude/projects/-home-bgarciamoura-projects-zmk-charybdis/memory/zmk_pmw3360_modules.md | — | ~494 |
| 16:48 | Created ../../.claude/projects/-home-bgarciamoura-projects-zmk-charybdis/memory/MEMORY.md | — | ~47 |
| 16:50 | Pesquisa web módulos ZMK PMW3360 (alternativas ao 3610 atual) | — | 3 forks reais; PR upstream #1163 fechado | ~6k |
| 16:55 | Registro dos achados em cerebrum.md (Key Learnings) | .wolf/cerebrum.md | ok | ~1k |
| 16:49 | Session end: 2 writes across 2 files (zmk_pmw3360_modules.md, MEMORY.md) | 0 reads | ~579 tok |
| 17:03 | Session end: 2 writes across 2 files (zmk_pmw3360_modules.md, MEMORY.md) | 1 reads | ~1913 tok |

## Session: 2026-05-08

| Time | Action | File(s) | Outcome | ~Tokens |
|------|--------|---------|---------|--------|
| --:-- | Pesquisa pinout TBK Mini (QMK keyboards/bastardkb/tbkmini + repos Bastardkb) | .wolf/cerebrum.md | ROW2COL 4 rows x 6 cols; cols=19,20,10,6,7,8; rows=18,5,4,9 (idêntico ao Charybdis Wireless Mini) | ~12k |
| 17:06 | Edited build.yaml | inline fix | ~6 |
| 17:06 | Desabilitado colemak_dh em todos os 6 grupos do build.yaml (comentado, não removido) | build.yaml | ok | ~0.5k |
| 17:06 | Session end: 3 writes across 3 files (zmk_pmw3360_modules.md, MEMORY.md, build.yaml) | 1 reads | ~1919 tok |
| 17:19 | Created build.yaml | — | ~1422 |
| 17:20 | Desabilitados bt, dongle_standard_nano, prospector_nano_*, prospector_xiao_sensor; ativos: settings_reset + dongle_prospector_xiao_no_sensor (alvo: XIAO BLE, futuro display Waveshare 1.69" touch, sem APDS9960) | build.yaml | yq valida 2 grupos ativos | ~2k |
| 17:20 | Session end: 4 writes across 3 files (zmk_pmw3360_modules.md, MEMORY.md, build.yaml) | 1 reads | ~3344 tok |
| 17:25 | Edited build.yaml | 2→4 lines | ~83 |
| 17:25 | Edited build.yaml | expanded (+18 lines) | ~262 |
| 17:25 | Edited build.yaml | 19→20 lines | ~238 |
| 17:30 | Adicionado grupo `dongle_standard_xiao` (XIAO BLE no dongle, sem Prospector). Comentado `dongle_prospector_xiao_no_sensor` para reativação futura quando Waveshare 1.69" chegar. Ativos agora: settings_reset + dongle_standard_xiao | build.yaml | yq valida 2 grupos ativos | ~3k |
| 17:26 | Session end: 7 writes across 3 files (zmk_pmw3360_modules.md, MEMORY.md, build.yaml) | 6 reads | ~4835 tok |
| 17:27 | Session end: 7 writes across 3 files (zmk_pmw3360_modules.md, MEMORY.md, build.yaml) | 6 reads | ~4835 tok |
| 17:35 | Tentativa de build local FALHOU silenciosamente — docker não disponível no shell, pipe `\| tail -200` mascarou exit 127. Logado em buglog.json (bug-001) e cerebrum Do-Not-Repeat. | .wolf/buglog.json, .wolf/cerebrum.md | bug-001 registrado | ~1k |
| 17:28 | Session end: 7 writes across 3 files (zmk_pmw3360_modules.md, MEMORY.md, build.yaml) | 6 reads | ~4835 tok |
| 17:34 | Session end: 7 writes across 3 files (zmk_pmw3360_modules.md, MEMORY.md, build.yaml) | 6 reads | ~4835 tok |
| 17:37 | Created ../../../../tmp/install-docker.sh | — | ~618 |
| 17:37 | Session end: 8 writes across 4 files (zmk_pmw3360_modules.md, MEMORY.md, build.yaml, install-docker.sh) | 6 reads | ~5497 tok |
| 17:38 | Session end: 8 writes across 4 files (zmk_pmw3360_modules.md, MEMORY.md, build.yaml, install-docker.sh) | 6 reads | ~5497 tok |

## Session: 2026-05-07 17:39

| Time | Action | File(s) | Outcome | ~Tokens |
|------|--------|---------|---------|--------|
| 17:55 | Build local Docker rodado com sucesso após instalação do docker pelo usuário. 4 firmwares gerados em 11m39s: settings_reset, charybdis_left_dongle (nice_nano), charybdis_right_dongle (nice_nano), charybdis_dongle (xiao_ble) — todos com `qwerty`. Confirmado que o shield charybdis_dongle compila em xiao_ble sem patches. | firmwares/ | sucesso | ~2k |
| 18:32 | Edited boards/shields/charybdis_dongle/charybdis_dongle.conf | 7→9 lines | ~96 |
| 18:32 | Session end: 1 writes across 1 files (charybdis_dongle.conf) | 3 reads | ~2404 tok |
| 18:41 | Session end: 1 writes across 1 files (charybdis_dongle.conf) | 3 reads | ~2404 tok |
| 18:48 | Session end: 1 writes across 1 files (charybdis_dongle.conf) | 4 reads | ~2404 tok |
| 18:51 | Session end: 1 writes across 1 files (charybdis_dongle.conf) | 4 reads | ~2404 tok |
| 18:57 | Session end: 1 writes across 1 files (charybdis_dongle.conf) | 9 reads | ~3872 tok |
| 19:07 | Session end: 1 writes across 1 files (charybdis_dongle.conf) | 12 reads | ~3872 tok |
| 19:10 | Session end: 1 writes across 1 files (charybdis_dongle.conf) | 13 reads | ~3872 tok |

| 19:45 | research | external | Elite-C-Holder 2.1 SPI pinout traced from PCB file | ~10k |
| 19:54 | Created TRACKBALL_MOD.md | — | ~3263 |
| 19:54 | Session end: 2 writes across 2 files (charybdis_dongle.conf, TRACKBALL_MOD.md) | 14 reads | ~7368 tok |
| 20:00 | Session end: 2 writes across 2 files (charybdis_dongle.conf, TRACKBALL_MOD.md) | 14 reads | ~7368 tok |
| 20:06 | Edited boards/shields/charybdis_right_dongle/charybdis_right_dongle.conf | 27→30 lines | ~350 |
| 20:07 | Session end: 3 writes across 3 files (charybdis_dongle.conf, TRACKBALL_MOD.md, charybdis_right_dongle.conf) | 14 reads | ~7743 tok |
| 20:14 | Session end: 3 writes across 3 files (charybdis_dongle.conf, TRACKBALL_MOD.md, charybdis_right_dongle.conf) | 14 reads | ~7743 tok |
| 20:15 | Edited boards/shields/charybdis_right_dongle/charybdis_right_dongle.overlay | 9→10 lines | ~86 |
| 20:16 | Session end: 4 writes across 4 files (charybdis_dongle.conf, TRACKBALL_MOD.md, charybdis_right_dongle.conf, charybdis_right_dongle.overlay) | 14 reads | ~7835 tok |
| 20:24 | Session end: 4 writes across 4 files (charybdis_dongle.conf, TRACKBALL_MOD.md, charybdis_right_dongle.conf, charybdis_right_dongle.overlay) | 14 reads | ~7835 tok |
| 20:32 | Session end: 4 writes across 4 files (charybdis_dongle.conf, TRACKBALL_MOD.md, charybdis_right_dongle.conf, charybdis_right_dongle.overlay) | 14 reads | ~7835 tok |
| 09:44 | Session end: 4 writes across 4 files (charybdis_dongle.conf, TRACKBALL_MOD.md, charybdis_right_dongle.conf, charybdis_right_dongle.overlay) | 19 reads | ~8606 tok |
| 09:48 | Edited local-build/build_setup.sh | "false" → "true" | ~47 |
| 09:49 | Session end: 5 writes across 5 files (charybdis_dongle.conf, TRACKBALL_MOD.md, charybdis_right_dongle.conf, charybdis_right_dongle.overlay, build_setup.sh) | 22 reads | ~13071 tok |
| 09:58 | Session end: 5 writes across 5 files (charybdis_dongle.conf, TRACKBALL_MOD.md, charybdis_right_dongle.conf, charybdis_right_dongle.overlay, build_setup.sh) | 22 reads | ~13071 tok |
| 10:38 | Session end: 5 writes across 5 files (charybdis_dongle.conf, TRACKBALL_MOD.md, charybdis_right_dongle.conf, charybdis_right_dongle.overlay, build_setup.sh) | 22 reads | ~13071 tok |
| 10:49 | Session end: 5 writes across 5 files (charybdis_dongle.conf, TRACKBALL_MOD.md, charybdis_right_dongle.conf, charybdis_right_dongle.overlay, build_setup.sh) | 25 reads | ~13732 tok |
| 11:01 | Session end: 5 writes across 5 files (charybdis_dongle.conf, TRACKBALL_MOD.md, charybdis_right_dongle.conf, charybdis_right_dongle.overlay, build_setup.sh) | 26 reads | ~13732 tok |
| 11:28 | Session end: 5 writes across 5 files (charybdis_dongle.conf, TRACKBALL_MOD.md, charybdis_right_dongle.conf, charybdis_right_dongle.overlay, build_setup.sh) | 26 reads | ~13732 tok |
| 11:46 | Session end: 5 writes across 5 files (charybdis_dongle.conf, TRACKBALL_MOD.md, charybdis_right_dongle.conf, charybdis_right_dongle.overlay, build_setup.sh) | 26 reads | ~13732 tok |
| 12:30 | Edited boards/shields/charybdis_dongle/charybdis_dongle.conf | expanded (+6 lines) | ~68 |
| 12:30 | Session end: 6 writes across 5 files (charybdis_dongle.conf, TRACKBALL_MOD.md, charybdis_right_dongle.conf, charybdis_right_dongle.overlay, build_setup.sh) | 27 reads | ~14001 tok |
| 12:39 | Session end: 6 writes across 5 files (charybdis_dongle.conf, TRACKBALL_MOD.md, charybdis_right_dongle.conf, charybdis_right_dongle.overlay, build_setup.sh) | 27 reads | ~14001 tok |
| 12:43 | Edited boards/shields/charybdis_dongle/charybdis_dongle.conf | 5→8 lines | ~99 |
| 12:43 | Session end: 7 writes across 5 files (charybdis_dongle.conf, TRACKBALL_MOD.md, charybdis_right_dongle.conf, charybdis_right_dongle.overlay, build_setup.sh) | 27 reads | ~14107 tok |
| 12:52 | Session end: 7 writes across 5 files (charybdis_dongle.conf, TRACKBALL_MOD.md, charybdis_right_dongle.conf, charybdis_right_dongle.overlay, build_setup.sh) | 27 reads | ~14107 tok |
| 12:57 | Session end: 7 writes across 5 files (charybdis_dongle.conf, TRACKBALL_MOD.md, charybdis_right_dongle.conf, charybdis_right_dongle.overlay, build_setup.sh) | 27 reads | ~14107 tok |
| 13:14 | Edited boards/shields/charybdis_right_dongle/charybdis_right_dongle.conf | 1→5 lines | ~79 |
| 13:14 | Session end: 8 writes across 5 files (charybdis_dongle.conf, TRACKBALL_MOD.md, charybdis_right_dongle.conf, charybdis_right_dongle.overlay, build_setup.sh) | 27 reads | ~14192 tok |
| 13:23 | Session end: 8 writes across 5 files (charybdis_dongle.conf, TRACKBALL_MOD.md, charybdis_right_dongle.conf, charybdis_right_dongle.overlay, build_setup.sh) | 27 reads | ~14192 tok |
| 13:58 | Session end: 8 writes across 5 files (charybdis_dongle.conf, TRACKBALL_MOD.md, charybdis_right_dongle.conf, charybdis_right_dongle.overlay, build_setup.sh) | 27 reads | ~14192 tok |
| 14:00 | Edited ../../.claude/statusline-command.sh | — | ~575 |
| 14:00 | Edited ../../.claude/settings.json | 3→7 lines | ~43 |
| 14:00 | Session end: 10 writes across 7 files (charybdis_dongle.conf, TRACKBALL_MOD.md, charybdis_right_dongle.conf, charybdis_right_dongle.overlay, build_setup.sh) | 32 reads | ~15292 tok |
| 14:01 | Edited boards/shields/charybdis_common/Kconfig.dongle.defconfig | 2→2 lines | ~14 |
| 14:01 | Session end: 11 writes across 8 files (charybdis_dongle.conf, TRACKBALL_MOD.md, charybdis_right_dongle.conf, charybdis_right_dongle.overlay, build_setup.sh) | 32 reads | ~15307 tok |
| 14:10 | Session end: 11 writes across 8 files (charybdis_dongle.conf, TRACKBALL_MOD.md, charybdis_right_dongle.conf, charybdis_right_dongle.overlay, build_setup.sh) | 32 reads | ~15307 tok |
| 14:12 | Edited boards/shields/charybdis_left_dongle/charybdis_left_dongle.conf | 1→2 lines | ~20 |
| 14:12 | Edited boards/shields/charybdis_right_dongle/charybdis_right_dongle.conf | 3→4 lines | ~60 |
| 14:12 | Session end: 13 writes across 9 files (charybdis_dongle.conf, TRACKBALL_MOD.md, charybdis_right_dongle.conf, charybdis_right_dongle.overlay, build_setup.sh) | 32 reads | ~15392 tok |
| 14:23 | Edited boards/shields/charybdis_common/Kconfig.dongle.defconfig | 2→2 lines | ~12 |
| 14:23 | Edited boards/shields/charybdis_common/Kconfig.dongle.defconfig | 2→2 lines | ~13 |
| 14:24 | Session end: 15 writes across 9 files (charybdis_dongle.conf, TRACKBALL_MOD.md, charybdis_right_dongle.conf, charybdis_right_dongle.overlay, build_setup.sh) | 32 reads | ~15419 tok |
| 14:35 | Session end: 15 writes across 9 files (charybdis_dongle.conf, TRACKBALL_MOD.md, charybdis_right_dongle.conf, charybdis_right_dongle.overlay, build_setup.sh) | 32 reads | ~15419 tok |
| 14:39 | Session end: 15 writes across 9 files (charybdis_dongle.conf, TRACKBALL_MOD.md, charybdis_right_dongle.conf, charybdis_right_dongle.overlay, build_setup.sh) | 32 reads | ~15419 tok |
| 14:55 | Session end: 15 writes across 9 files (charybdis_dongle.conf, TRACKBALL_MOD.md, charybdis_right_dongle.conf, charybdis_right_dongle.overlay, build_setup.sh) | 32 reads | ~15419 tok |
| 14:59 | Session end: 15 writes across 9 files (charybdis_dongle.conf, TRACKBALL_MOD.md, charybdis_right_dongle.conf, charybdis_right_dongle.overlay, build_setup.sh) | 32 reads | ~15419 tok |
| 15:01 | Session end: 15 writes across 9 files (charybdis_dongle.conf, TRACKBALL_MOD.md, charybdis_right_dongle.conf, charybdis_right_dongle.overlay, build_setup.sh) | 32 reads | ~15419 tok |
| 15:05 | Session end: 15 writes across 9 files (charybdis_dongle.conf, TRACKBALL_MOD.md, charybdis_right_dongle.conf, charybdis_right_dongle.overlay, build_setup.sh) | 32 reads | ~15419 tok |
| 15:11 | Created ../../.claude/projects/-home-bgarciamoura-projects-zmk-charybdis/memory/zmk_split_ble_findings.md | — | ~884 |
| 15:13 | Created ../../.claude/projects/-home-bgarciamoura-projects-zmk-charybdis/memory/charybdis_hardware_setup.md | — | ~1107 |
| 15:13 | Edited ../../.claude/projects/-home-bgarciamoura-projects-zmk-charybdis/memory/MEMORY.md | 1→3 lines | ~154 |
| 15:14 | Session end: 18 writes across 12 files (charybdis_dongle.conf, TRACKBALL_MOD.md, charybdis_right_dongle.conf, charybdis_right_dongle.overlay, build_setup.sh) | 33 reads | ~17717 tok |

## Session: 2026-05-08 15:14

| Time | Action | File(s) | Outcome | ~Tokens |
|------|--------|---------|---------|--------|

## Session: 2026-05-17 21:15

| Time | Action | File(s) | Outcome | ~Tokens |
|------|--------|---------|---------|--------|
| 22:02 | Edited local-build/build_setup.sh | "true" → "false" | ~28 |
| 22:02 | Edited boards/shields/charybdis_dongle/charybdis_dongle.conf | removed 12 lines | ~13 |
| 22:02 | Edited build.yaml | 4→5 lines | ~71 |
| 22:02 | Edited build.yaml | 6→7 lines | ~82 |
| 22:03 | Session end: 4 writes across 3 files (build_setup.sh, charybdis_dongle.conf, build.yaml) | 2 reads | ~4471 tok |
| 22:07 | Session end: 4 writes across 3 files (build_setup.sh, charybdis_dongle.conf, build.yaml) | 2 reads | ~4471 tok |
| 22:11 | Session end: 4 writes across 3 files (build_setup.sh, charybdis_dongle.conf, build.yaml) | 2 reads | ~4471 tok |
| 10:29 | Session end: 4 writes across 3 files (build_setup.sh, charybdis_dongle.conf, build.yaml) | 2 reads | ~4471 tok |
| 10:33 | Session end: 4 writes across 3 files (build_setup.sh, charybdis_dongle.conf, build.yaml) | 2 reads | ~4471 tok |
| 11:32 | Session end: 4 writes across 3 files (build_setup.sh, charybdis_dongle.conf, build.yaml) | 2 reads | ~4471 tok |
| 11:38 | Session end: 4 writes across 3 files (build_setup.sh, charybdis_dongle.conf, build.yaml) | 2 reads | ~4471 tok |
| 11:41 | Session end: 4 writes across 3 files (build_setup.sh, charybdis_dongle.conf, build.yaml) | 2 reads | ~4471 tok |
| 11:44 | Session end: 4 writes across 3 files (build_setup.sh, charybdis_dongle.conf, build.yaml) | 2 reads | ~4471 tok |
| 11:57 | Created TRACKBALL_PMW3610.md | — | ~2991 |
| 11:57 | Edited README.md | expanded (+8 lines) | ~265 |
| 11:58 | SESSION HIGHLIGHT 2026-05-17: usuário recebeu PMW3610-Module 20240425 (chinês, 32mm, LDO 2V onboard) + soldou half esquerda. Build matrix dongle_standard_xiao ativo. Bug-009 resolvido (USB_LOGGING travava Studio+TeraTerm). Bug do west update por mode-bit drift documentado em cerebrum. Doc completo de wiring PMW3610 criado em TRACKBALL_PMW3610.md (pinout J8 lido do schematic KiCad oficial, 3 jumpers diretos). Próximo: aplicar pinctrl change em charybdis_pmw3610.dtsi + reativar trackball no right_dongle + rebuild + flash. | TRACKBALL_PMW3610.md, README.md, .wolf/cerebrum.md, .wolf/anatomy.md, .wolf/buglog.json | ~8000 tok
| 11:59 | Edited boards/shields/charybdis_right_dongle/charybdis_right_dongle.conf | 28→25 lines | ~251 |
| 11:59 | Edited boards/shields/charybdis_right_dongle/charybdis_right_dongle.overlay | 10→9 lines | ~46 |
| 11:59 | Edited build.yaml | 4→5 lines | ~70 |
| 11:59 | Edited build.yaml | 6→7 lines | ~79 |
| 12:00 | Session end: 10 writes across 7 files (build_setup.sh, charybdis_dongle.conf, build.yaml, TRACKBALL_PMW3610.md, README.md) | 5 reads | ~11806 tok |
| 12:04 | Session end: 10 writes across 7 files (build_setup.sh, charybdis_dongle.conf, build.yaml, TRACKBALL_PMW3610.md, README.md) | 5 reads | ~11806 tok |
| 12:36 | Session end: 10 writes across 7 files (build_setup.sh, charybdis_dongle.conf, build.yaml, TRACKBALL_PMW3610.md, README.md) | 5 reads | ~11806 tok |
| 12:52 | Session end: 10 writes across 7 files (build_setup.sh, charybdis_dongle.conf, build.yaml, TRACKBALL_PMW3610.md, README.md) | 5 reads | ~11806 tok |
| 12:53 | Session end: 10 writes across 7 files (build_setup.sh, charybdis_dongle.conf, build.yaml, TRACKBALL_PMW3610.md, README.md) | 5 reads | ~11806 tok |
| 12:57 | Session end: 10 writes across 7 files (build_setup.sh, charybdis_dongle.conf, build.yaml, TRACKBALL_PMW3610.md, README.md) | 5 reads | ~11806 tok |
| 13:08 | Edited boards/shields/charybdis_right_dongle/charybdis_right_dongle.conf | 6→7 lines | ~90 |
| 13:08 | Edited boards/shields/charybdis_right_dongle/charybdis_right_dongle.conf | 3→4 lines | ~57 |
| 13:10 | Edited local-build/build_setup.sh | "false" → "true" | ~48 |
| 13:09 | Edited build.yaml | 4→5 lines | ~70 |
| 13:09 | Edited build.yaml | 6→7 lines | ~78 |
| 13:10 | Session end: 15 writes across 7 files (build_setup.sh, charybdis_dongle.conf, build.yaml, TRACKBALL_PMW3610.md, README.md) | 5 reads | ~12163 tok |
| 13:13 | Session end: 15 writes across 7 files (build_setup.sh, charybdis_dongle.conf, build.yaml, TRACKBALL_PMW3610.md, README.md) | 5 reads | ~12163 tok |
| 13:20 | Edited boards/shields/charybdis_trackball/charybdis_pmw3610.dtsi | 18→18 lines | ~163 |
| 13:22 | Edited build.yaml | 4→5 lines | ~71 |
| 13:22 | Edited build.yaml | 6→7 lines | ~80 |
| 13:24 | Session end: 18 writes across 8 files (build_setup.sh, charybdis_dongle.conf, build.yaml, TRACKBALL_PMW3610.md, README.md) | 6 reads | ~13099 tok |
| 13:27 | Session end: 18 writes across 8 files (build_setup.sh, charybdis_dongle.conf, build.yaml, TRACKBALL_PMW3610.md, README.md) | 6 reads | ~13099 tok |
| 13:32 | Session end: 18 writes across 8 files (build_setup.sh, charybdis_dongle.conf, build.yaml, TRACKBALL_PMW3610.md, README.md) | 6 reads | ~13099 tok |
| 13:34 | Edited boards/shields/charybdis_right_dongle/charybdis_right_dongle.conf | 2→1 lines | ~31 |
| 13:34 | Edited boards/shields/charybdis_right_dongle/charybdis_right_dongle.conf | 4→3 lines | ~39 |
| 13:34 | Edited local-build/build_setup.sh | "true" → "false" | ~28 |
| 13:37 | Session end: 21 writes across 8 files (build_setup.sh, charybdis_dongle.conf, build.yaml, TRACKBALL_PMW3610.md, README.md) | 6 reads | ~13204 tok |
| 13:43 | Session end: 21 writes across 8 files (build_setup.sh, charybdis_dongle.conf, build.yaml, TRACKBALL_PMW3610.md, README.md) | 6 reads | ~13204 tok |
| 14:01 | Session end: 21 writes across 8 files (build_setup.sh, charybdis_dongle.conf, build.yaml, TRACKBALL_PMW3610.md, README.md) | 6 reads | ~13204 tok |

## Session: 2026-05-17 14:01

| Time | Action | File(s) | Outcome | ~Tokens |
|------|--------|---------|---------|--------|
| 14:01 | exibe BASE layer do qwerty.keymap | config/keymaps/qwerty.keymap | ok | ~1.8k |
| 14:35 | log bug-018 (solda fria diodos cols 3/4 direita) + cerebrum learning | .wolf/buglog.json .wolf/cerebrum.md | ok | ~1.2k |

## Session: 2026-05-17 14:36

| Time | Action | File(s) | Outcome | ~Tokens |
|------|--------|---------|---------|--------|
| 14:43 | Created KEYMAP_EDITING.md | — | ~2505 |
| 14:44 | Edited CLAUDE.md | inline fix | ~82 |
| 15:10 | Criado KEYMAP_EDITING.md (referência completa de edição de keymap) + corrigido layer order errado no CLAUDE.md (MOUSE não existe) | KEYMAP_EDITING.md, CLAUDE.md | ok | ~2.5k |
| 14:45 | Session end: 2 writes across 2 files (KEYMAP_EDITING.md, CLAUDE.md) | 3 reads | ~8357 tok |

## Session: 2026-05-18 14:30

| Time | Action | File(s) | Outcome | ~Tokens |
|------|--------|---------|---------|--------|
| 15:21 | Created ../../.claude/projects/-home-bgarciamoura-projects-zmk-charybdis/memory/nrf52840_supermini_pinout.md | — | ~1484 |
| 15:21 | Edited ../../.claude/projects/-home-bgarciamoura-projects-zmk-charybdis/memory/nrf52840_supermini_pinout.md | 3→8 lines | ~227 |
| 15:21 | Edited ../../.claude/projects/-home-bgarciamoura-projects-zmk-charybdis/memory/MEMORY.md | 1→2 lines | ~119 |
| 15:22 | Session end: 3 writes across 2 files (nrf52840_supermini_pinout.md, MEMORY.md) | 4 reads | ~2615 tok |
| 15:28 | Session end: 3 writes across 2 files (nrf52840_supermini_pinout.md, MEMORY.md) | 6 reads | ~4478 tok |
| 15:33 | Session end: 3 writes across 2 files (nrf52840_supermini_pinout.md, MEMORY.md) | 6 reads | ~4478 tok |
| 15:44 | Session end: 3 writes across 2 files (nrf52840_supermini_pinout.md, MEMORY.md) | 6 reads | ~4478 tok |
| 15:49 | Session end: 3 writes across 2 files (nrf52840_supermini_pinout.md, MEMORY.md) | 6 reads | ~4478 tok |

## Session: 2026-05-18 15:54

| Time | Action | File(s) | Outcome | ~Tokens |
|------|--------|---------|---------|--------|

## Session: 2026-05-18 16:57

| Time | Action | File(s) | Outcome | ~Tokens |
|------|--------|---------|---------|--------|

## Session: 2026-05-19 22:01

| Time | Action | File(s) | Outcome | ~Tokens |
|------|--------|---------|---------|--------|
| 22:08 | Edited boards/shields/charybdis_dongle/charybdis_dongle.overlay | 14→16 lines | ~129 |
| 22:08 | Edited boards/shields/charybdis_dongle/charybdis_dongle.overlay | expanded (+18 lines) | ~152 |
| 22:08 | Edited boards/shields/charybdis_dongle/charybdis_dongle.conf | 3→7 lines | ~45 |
| 22:08 | Add SSD1306 0.96" OLED on dongle (XIAO BLE i2c1 / D4-D5 / addr 0x3C). Re-enable i2c1 (was disabled for APDS9960). CONFIG_ZMK_DISPLAY=y + BLANK_ON_IDLE=n. | charybdis_dongle.{overlay,conf} | build kicked off | ~1k |
| 22:12 | Session end: 3 writes across 2 files (charybdis_dongle.overlay, charybdis_dongle.conf) | 6 reads | ~2887 tok |
| 22:21 | Session end: 3 writes across 2 files (charybdis_dongle.overlay, charybdis_dongle.conf) | 6 reads | ~2887 tok |
| 22:34 | Edited boards/shields/charybdis_dongle/charybdis_dongle.overlay | 21→24 lines | ~207 |
| 22:35 | Edited boards/shields/charybdis_dongle/charybdis_dongle.overlay | 3→2 lines | ~25 |
| 22:35 | Session end: 5 writes across 2 files (charybdis_dongle.overlay, charybdis_dongle.conf) | 8 reads | ~3135 tok |
| 22:42 | Session end: 5 writes across 2 files (charybdis_dongle.overlay, charybdis_dongle.conf) | 8 reads | ~3135 tok |

## Session: 2026-05-19 11:18

| Time | Action | File(s) | Outcome | ~Tokens |
|------|--------|---------|---------|--------|
| 11:23 | re-solder PMW3610 wires | TRACKBALL_PMW3610.md | guidance only (no edits) | ~6000 |
| 12:19 | Edited boards/shields/charybdis_right_dongle/charybdis_right_dongle.conf | inline fix | ~10 |
| 12:20 | Edited local-build/build_setup.sh | "false" → "true" | ~28 |
| 12:20 | Session end: 2 writes across 2 files (charybdis_right_dongle.conf, build_setup.sh) | 5 reads | ~9133 tok |
| 12:21 | Session end: 2 writes across 2 files (charybdis_right_dongle.conf, build_setup.sh) | 5 reads | ~9133 tok |
| 12:30 | Session end: 2 writes across 2 files (charybdis_right_dongle.conf, build_setup.sh) | 5 reads | ~9133 tok |
| 12:47 | Session end: 2 writes across 2 files (charybdis_right_dongle.conf, build_setup.sh) | 19 reads | ~11242 tok |
| 12:57 | Session end: 2 writes across 2 files (charybdis_right_dongle.conf, build_setup.sh) | 19 reads | ~11242 tok |
| 15:39 | Session end: 2 writes across 2 files (charybdis_right_dongle.conf, build_setup.sh) | 19 reads | ~11242 tok |
| 15:42 | Session end: 2 writes across 2 files (charybdis_right_dongle.conf, build_setup.sh) | 19 reads | ~11242 tok |

## Session: 2026-07-07 15:27

| Time | Action | File(s) | Outcome | ~Tokens |
|------|--------|---------|---------|--------|
| 15:59 | Retomada debug trackball: validado que firmwares/dongle_standard_xiao/qwerty/charybdis_right_dongle.uf2 (19/05 12:27) já contém PMW3610 debug logging + USB CDC. Plano: flash + captura serial | firmwares/ | ok | ~200 |
| 16:56 | Edited boards/shields/charybdis_right_dongle/charybdis_right_dongle.conf | modified FIX() | ~100 |
| 16:59 | Edited build.yaml | modified TEMP() | ~70 |
| 16:59 | Edited build.yaml | modified TEMP() | ~78 |
| 17:05 | Diagnóstico trackball: race de power-up no init do PMW3610 (product id 0xff, IRQ nunca armada, MOT preso LOW). Fix: EXTRA_DELAY=500ms. Corrigidos erros D0/D1 e ordem 006/008 no guia. Build right_dongle disparado | charybdis_right_dongle.conf, TRACKBALL_PMW3610.md, build.yaml (temp), buglog, cerebrum | ok | ~3k |
| 17:05 | Session end: 3 writes across 2 files (charybdis_right_dongle.conf, build.yaml) | 5 reads | ~2296 tok |
| 17:06 | Edited build.yaml | 5→4 lines | ~46 |
| 17:06 | Edited build.yaml | 7→6 lines | ~52 |
| 17:07 | Build right_dongle com EXTRA_DELAY=500 concluído (3m39s, FLASH 29.59%). build.yaml restaurado pra matriz completa | firmwares/.../charybdis_right_dongle.uf2, build.yaml | ok | ~500 |
| 17:08 | Session end: 5 writes across 2 files (charybdis_right_dongle.conf, build.yaml) | 5 reads | ~2394 tok |
| 17:13 | Session end: 5 writes across 2 files (charybdis_right_dongle.conf, build.yaml) | 5 reads | ~2394 tok |
| 17:21 | Trackball CONFIRMADO funcional pós EXTRA_DELAY=500 (usuário validou cursor via dongle). Obs: dongle tinha travado durante teste anterior (causa do notify -128). Próximo: orientação + DPI | .wolf/buglog.json | ok | ~300 |
| 17:25 | Edited boards/shields/charybdis_trackball/charybdis_pmw3610.dtsi | inline fix | ~19 |
| 17:25 | Edited boards/shields/charybdis_trackball/charybdis_pmw3610.dtsi | modified 07() | ~96 |
| 17:25 | Edited build.yaml | modified TEMP() | ~70 |
| 17:25 | Edited build.yaml | modified TEMP() | ~78 |
| 17:27 | Session end: 9 writes across 3 files (charybdis_right_dongle.conf, build.yaml, charybdis_pmw3610.dtsi) | 6 reads | ~3275 tok |
| 17:32 | Edited build.yaml | 5→4 lines | ~46 |
| 17:32 | Edited build.yaml | 7→6 lines | ~52 |
| 17:47 | Build right_dongle com orientação corrigida (removidos invert-x/y, mantido swap-xy) + CPI 800→400 (4m27s). build.yaml restaurado | charybdis_pmw3610.dtsi, build.yaml | ok | ~400 |
| 17:48 | Session end: 11 writes across 3 files (charybdis_right_dongle.conf, build.yaml, charybdis_pmw3610.dtsi) | 6 reads | ~3373 tok |
| 18:37 | Edited ../../.claude/projects/-home-bgarciamoura-projects-zmk-charybdis/memory/charybdis_hardware_setup.md | 1→2 lines | ~138 |
| 18:42 | Edited build.yaml | modified TEMP() | ~71 |
| 18:42 | Edited build.yaml | modified TEMP() | ~77 |
| 18:44 | Session end: 14 writes across 4 files (charybdis_right_dongle.conf, build.yaml, charybdis_pmw3610.dtsi, charybdis_hardware_setup.md) | 6 reads | ~3669 tok |
| 18:46 | Edited build.yaml | 5→4 lines | ~46 |
| 18:46 | Edited build.yaml | 7→6 lines | ~52 |
| 18:46 | Build charybdis_dongle com SSD1306 (2m13s, driver confirmado no uf2 via strings). Firmware antigo do dongle nunca teve o overlay final do OLED. Obs: builds parciais LIMPAM firmwares/ (right_dongle.uf2 sumiu de novo — full build no fim da sessão) | firmwares/, build.yaml | ok | ~300 |
| 18:46 | Session end: 16 writes across 4 files (charybdis_right_dongle.conf, build.yaml, charybdis_pmw3610.dtsi, charybdis_hardware_setup.md) | 6 reads | ~3767 tok |
| 23:19 | Edited boards/shields/charybdis_dongle/charybdis_dongle.overlay | modified 07() | ~297 |
| 23:16 | Edited build.yaml | modified TEMP() | ~71 |
| 23:16 | Edited build.yaml | modified TEMP() | ~77 |
| 23:17 | Diagnóstico display: módulo é SH1106 mascarado de SSD1306 (estática + faixa repetitiva = frame caindo numa página só). Overlay: compatible sinowealth,sh1106 + segment-offset=2. Build dongle disparado | charybdis_dongle.overlay, buglog | ok | ~600 |
| 23:18 | Session end: 19 writes across 5 files (charybdis_right_dongle.conf, build.yaml, charybdis_pmw3610.dtsi, charybdis_hardware_setup.md, charybdis_dongle.overlay) | 7 reads | ~5046 tok |
| 23:26 | Edited build.yaml | 5→4 lines | ~46 |
| 23:23 | Edited build.yaml | 7→6 lines | ~52 |
| 23:23 | Session end: 21 writes across 5 files (charybdis_right_dongle.conf, build.yaml, charybdis_pmw3610.dtsi, charybdis_hardware_setup.md, charybdis_dongle.overlay) | 7 reads | ~5144 tok |
| 23:30 | Session end: 21 writes across 5 files (charybdis_right_dongle.conf, build.yaml, charybdis_pmw3610.dtsi, charybdis_hardware_setup.md, charybdis_dongle.overlay) | 7 reads | ~5144 tok |
| 23:33 | Session end: 21 writes across 5 files (charybdis_right_dongle.conf, build.yaml, charybdis_pmw3610.dtsi, charybdis_hardware_setup.md, charybdis_dongle.overlay) | 7 reads | ~5144 tok |
| 23:35 | Session end: 21 writes across 5 files (charybdis_right_dongle.conf, build.yaml, charybdis_pmw3610.dtsi, charybdis_hardware_setup.md, charybdis_dongle.overlay) | 7 reads | ~5144 tok |
| 23:38 | Edited boards/shields/charybdis_dongle/charybdis_dongle.overlay | modified 07() | ~170 |
| 23:38 | Edited build.yaml | modified TEMP() | ~71 |
| 23:38 | Edited build.yaml | modified TEMP() | ~77 |
| 23:40 | SH1106 refutado: firmware trava boot do dongle (sem USB/LED). Overlay revertido pra ssd1306fb. Rebuild em andamento. Próximo: capturar log serial com firmware que boota | charybdis_dongle.overlay, buglog | ok | ~500 |
| 23:40 | Session end: 24 writes across 5 files (charybdis_right_dongle.conf, build.yaml, charybdis_pmw3610.dtsi, charybdis_hardware_setup.md, charybdis_dongle.overlay) | 7 reads | ~5474 tok |
| 23:44 | Edited build.yaml | 5→4 lines | ~46 |
| 23:44 | Edited build.yaml | 7→6 lines | ~52 |
| 23:44 | Session end: 26 writes across 5 files (charybdis_right_dongle.conf, build.yaml, charybdis_pmw3610.dtsi, charybdis_hardware_setup.md, charybdis_dongle.overlay) | 7 reads | ~5572 tok |
| 23:49 | Session end: 26 writes across 5 files (charybdis_right_dongle.conf, build.yaml, charybdis_pmw3610.dtsi, charybdis_hardware_setup.md, charybdis_dongle.overlay) | 7 reads | ~5572 tok |
| 23:52 | Session end: 26 writes across 5 files (charybdis_right_dongle.conf, build.yaml, charybdis_pmw3610.dtsi, charybdis_hardware_setup.md, charybdis_dongle.overlay) | 7 reads | ~5572 tok |
| 23:54 | Created ../../../../mnt/c/Users/Public/dongle-capture.ps1 | — | ~386 |
| 23:56 | Session end: 27 writes across 6 files (charybdis_right_dongle.conf, build.yaml, charybdis_pmw3610.dtsi, charybdis_hardware_setup.md, charybdis_dongle.overlay) | 7 reads | ~5985 tok |
| 23:58 | Session end: 27 writes across 6 files (charybdis_right_dongle.conf, build.yaml, charybdis_pmw3610.dtsi, charybdis_hardware_setup.md, charybdis_dongle.overlay) | 8 reads | ~5985 tok |
| 00:00 | Session end: 27 writes across 6 files (charybdis_right_dongle.conf, build.yaml, charybdis_pmw3610.dtsi, charybdis_hardware_setup.md, charybdis_dongle.overlay) | 8 reads | ~5985 tok |
| 00:01 | Edited boards/shields/charybdis_dongle/charybdis_dongle.overlay | modified 08() | ~199 |
| 00:05 | Edited build.yaml | modified TEMP() | ~71 |
| 00:01 | Edited build.yaml | modified TEMP() | ~77 |
| 00:03 | Diagnóstico display FECHADO por isolamento: flush LVGL trava MCU (USB morre pós-enumeração). Sem OLED = estável. Fix em teste: i2c1 nrf-twi→nrf-twim + concat-buf 1100. Build disparado | charybdis_dongle.overlay, buglog | ok | ~700 |
| 00:03 | Session end: 30 writes across 6 files (charybdis_right_dongle.conf, build.yaml, charybdis_pmw3610.dtsi, charybdis_hardware_setup.md, charybdis_dongle.overlay) | 8 reads | ~6347 tok |
| 00:11 | Edited build.yaml | 5→4 lines | ~46 |
| 00:07 | Edited build.yaml | 7→6 lines | ~52 |
| 00:07 | Session end: 32 writes across 6 files (charybdis_right_dongle.conf, build.yaml, charybdis_pmw3610.dtsi, charybdis_hardware_setup.md, charybdis_dongle.overlay) | 8 reads | ~6445 tok |
| 00:09 | Session end: 32 writes across 6 files (charybdis_right_dongle.conf, build.yaml, charybdis_pmw3610.dtsi, charybdis_hardware_setup.md, charybdis_dongle.overlay) | 8 reads | ~6445 tok |
| 00:10 | Session end: 32 writes across 6 files (charybdis_right_dongle.conf, build.yaml, charybdis_pmw3610.dtsi, charybdis_hardware_setup.md, charybdis_dongle.overlay) | 8 reads | ~6445 tok |
| 00:18 | Edited boards/shields/charybdis_dongle/charybdis_dongle.overlay | modified RAIZ() | ~162 |
| 00:18 | Edited boards/shields/charybdis_dongle/charybdis_dongle.overlay | inline fix | ~8 |
| 00:19 | Edited boards/shields/charybdis_dongle/charybdis_dongle.conf | modified TICO() | ~149 |
| 00:19 | Edited build.yaml | modified TEMP() | ~71 |
| 00:23 | Edited build.yaml | modified TEMP() | ~77 |
| 00:20 | Causa raiz display: UI na system work queue bloqueia USB/BLE (ref englmaxi/zmk-dongle-display). Fix: WORK_QUEUE_DEDICATED + stack 4096 + LV pool 16384 + VDB 100; TWIM revertido; prechargep 0x22. Build disparado | charybdis_dongle.{conf,overlay}, buglog | ok | ~800 |
| 00:21 | Session end: 37 writes across 7 files (charybdis_right_dongle.conf, build.yaml, charybdis_pmw3610.dtsi, charybdis_hardware_setup.md, charybdis_dongle.overlay) | 9 reads | ~7161 tok |
| 00:22 | Edited build.yaml | 5→4 lines | ~46 |
| 00:22 | Edited build.yaml | 7→6 lines | ~52 |
| 00:22 | Session end: 39 writes across 7 files (charybdis_right_dongle.conf, build.yaml, charybdis_pmw3610.dtsi, charybdis_hardware_setup.md, charybdis_dongle.overlay) | 9 reads | ~7259 tok |
| 00:24 | Session end: 39 writes across 7 files (charybdis_right_dongle.conf, build.yaml, charybdis_pmw3610.dtsi, charybdis_hardware_setup.md, charybdis_dongle.overlay) | 9 reads | ~7259 tok |
| 00:26 | Session end: 39 writes across 7 files (charybdis_right_dongle.conf, build.yaml, charybdis_pmw3610.dtsi, charybdis_hardware_setup.md, charybdis_dongle.overlay) | 9 reads | ~7259 tok |
| 00:30 | Session end: 39 writes across 7 files (charybdis_right_dongle.conf, build.yaml, charybdis_pmw3610.dtsi, charybdis_hardware_setup.md, charybdis_dongle.overlay) | 9 reads | ~7259 tok |
| 00:34 | Edited boards/shields/charybdis_dongle/charybdis_dongle.conf | modified BISECT() | ~128 |
| 00:34 | Edited build.yaml | modified TEMP() | ~71 |
| 00:34 | Edited build.yaml | modified TEMP() | ~77 |
| 00:34 | Session end: 42 writes across 7 files (charybdis_right_dongle.conf, build.yaml, charybdis_pmw3610.dtsi, charybdis_hardware_setup.md, charybdis_dongle.overlay) | 9 reads | ~7544 tok |
| 00:38 | Edited build.yaml | 5→4 lines | ~46 |
| 00:38 | Edited build.yaml | 7→6 lines | ~52 |
| 00:38 | Bisect display: multímetro provou bus saudável (SDA/SCL 3.23V idle) com dongle travado → crash de software entre criação da tela e 1º flush. Build sem widgets (layer/battery/output =n) pronto pra teste | charybdis_dongle.conf, build.yaml | ok | ~400 |
| 00:38 | Session end: 44 writes across 7 files (charybdis_right_dongle.conf, build.yaml, charybdis_pmw3610.dtsi, charybdis_hardware_setup.md, charybdis_dongle.overlay) | 9 reads | ~7642 tok |
| 00:41 | Edited boards/shields/charybdis_dongle/charybdis_dongle.conf | widget() → logging() | ~60 |
| 00:41 | Edited local-build/build_setup.sh | "true" → "false" | ~28 |
| 00:41 | Edited build.yaml | modified TEMP() | ~71 |
| 00:41 | Edited build.yaml | modified TEMP() | ~77 |
| 00:45 | Session end: 48 writes across 8 files (charybdis_right_dongle.conf, build.yaml, charybdis_pmw3610.dtsi, charybdis_hardware_setup.md, charybdis_dongle.overlay) | 10 reads | ~11844 tok |
| 00:50 | Edited build.yaml | 5→4 lines | ~46 |
| 00:54 | Edited build.yaml | 7→6 lines | ~52 |
| 00:50 | Session end: 50 writes across 8 files (charybdis_right_dongle.conf, build.yaml, charybdis_pmw3610.dtsi, charybdis_hardware_setup.md, charybdis_dongle.overlay) | 10 reads | ~11942 tok |
| 00:54 | Edited boards/shields/charybdis_dongle/charybdis_dongle.conf | modified FINAL() | ~93 |
| 00:54 | Edited build.yaml | modified TEMP() | ~71 |
| 00:54 | Edited build.yaml | modified TEMP() | ~77 |
| 00:58 | Bisect display: widgets, USB logging, work queue, TWI/TWIM TODOS descartados. Bus idle saudável no multímetro. Último bisect firmware: ZMK_DISPLAY=n (driver init sem LVGL). Suspeita: módulo clone eletricamente patológico em bursts | charybdis_dongle.conf, buglog | ok | ~600 |
| 00:58 | Edited build.yaml | 5→4 lines | ~46 |
| 00:58 | Edited build.yaml | 7→6 lines | ~52 |
| 00:58 | Session end: 55 writes across 8 files (charybdis_right_dongle.conf, build.yaml, charybdis_pmw3610.dtsi, charybdis_hardware_setup.md, charybdis_dongle.overlay) | 10 reads | ~12288 tok |
| 01:01 | Edited boards/shields/charybdis_dongle/charybdis_dongle.overlay | modified D5() | ~525 |
| 01:01 | Edited boards/shields/charybdis_dongle/charybdis_dongle.conf | 6→5 lines | ~46 |
| 01:01 | Edited build.yaml | modified TEMP() | ~71 |
| 01:01 | Edited build.yaml | modified TEMP() | ~77 |
| 01:02 | Session end: 59 writes across 8 files (charybdis_right_dongle.conf, build.yaml, charybdis_pmw3610.dtsi, charybdis_hardware_setup.md, charybdis_dongle.overlay) | 10 reads | ~13277 tok |
| 01:15 | Edited boards/shields/charybdis_dongle/charybdis_dongle.overlay | 5→6 lines | ~60 |
| 01:17 | Session end: 60 writes across 8 files (charybdis_right_dongle.conf, build.yaml, charybdis_pmw3610.dtsi, charybdis_hardware_setup.md, charybdis_dongle.overlay) | 10 reads | ~13342 tok |
| 01:20 | Session end: 60 writes across 8 files (charybdis_right_dongle.conf, build.yaml, charybdis_pmw3610.dtsi, charybdis_hardware_setup.md, charybdis_dongle.overlay) | 10 reads | ~13342 tok |
| 01:24 | Session end: 60 writes across 8 files (charybdis_right_dongle.conf, build.yaml, charybdis_pmw3610.dtsi, charybdis_hardware_setup.md, charybdis_dongle.overlay) | 10 reads | ~13342 tok |
| 01:25 | Session end: 60 writes across 8 files (charybdis_right_dongle.conf, build.yaml, charybdis_pmw3610.dtsi, charybdis_hardware_setup.md, charybdis_dongle.overlay) | 10 reads | ~13342 tok |
| 01:25 | Session end: 60 writes across 8 files (charybdis_right_dongle.conf, build.yaml, charybdis_pmw3610.dtsi, charybdis_hardware_setup.md, charybdis_dongle.overlay) | 10 reads | ~13342 tok |
| 01:25 | Session end: 60 writes across 8 files (charybdis_right_dongle.conf, build.yaml, charybdis_pmw3610.dtsi, charybdis_hardware_setup.md, charybdis_dongle.overlay) | 10 reads | ~13342 tok |
| 01:26 | Session end: 60 writes across 8 files (charybdis_right_dongle.conf, build.yaml, charybdis_pmw3610.dtsi, charybdis_hardware_setup.md, charybdis_dongle.overlay) | 10 reads | ~13342 tok |
| 01:26 | Session end: 60 writes across 8 files (charybdis_right_dongle.conf, build.yaml, charybdis_pmw3610.dtsi, charybdis_hardware_setup.md, charybdis_dongle.overlay) | 10 reads | ~13342 tok |
| 01:26 | Session end: 60 writes across 8 files (charybdis_right_dongle.conf, build.yaml, charybdis_pmw3610.dtsi, charybdis_hardware_setup.md, charybdis_dongle.overlay) | 10 reads | ~13342 tok |
| 01:26 | Session end: 60 writes across 8 files (charybdis_right_dongle.conf, build.yaml, charybdis_pmw3610.dtsi, charybdis_hardware_setup.md, charybdis_dongle.overlay) | 10 reads | ~13342 tok |
| 01:26 | Session end: 60 writes across 8 files (charybdis_right_dongle.conf, build.yaml, charybdis_pmw3610.dtsi, charybdis_hardware_setup.md, charybdis_dongle.overlay) | 10 reads | ~13342 tok |
| 01:26 | Session end: 60 writes across 8 files (charybdis_right_dongle.conf, build.yaml, charybdis_pmw3610.dtsi, charybdis_hardware_setup.md, charybdis_dongle.overlay) | 10 reads | ~13342 tok |
| 01:27 | Session end: 60 writes across 8 files (charybdis_right_dongle.conf, build.yaml, charybdis_pmw3610.dtsi, charybdis_hardware_setup.md, charybdis_dongle.overlay) | 10 reads | ~13342 tok |
| 01:27 | Session end: 60 writes across 8 files (charybdis_right_dongle.conf, build.yaml, charybdis_pmw3610.dtsi, charybdis_hardware_setup.md, charybdis_dongle.overlay) | 10 reads | ~13342 tok |
| 01:27 | Session end: 60 writes across 8 files (charybdis_right_dongle.conf, build.yaml, charybdis_pmw3610.dtsi, charybdis_hardware_setup.md, charybdis_dongle.overlay) | 10 reads | ~13342 tok |
| 01:27 | Session end: 60 writes across 8 files (charybdis_right_dongle.conf, build.yaml, charybdis_pmw3610.dtsi, charybdis_hardware_setup.md, charybdis_dongle.overlay) | 10 reads | ~13342 tok |
| 01:27 | Session end: 60 writes across 8 files (charybdis_right_dongle.conf, build.yaml, charybdis_pmw3610.dtsi, charybdis_hardware_setup.md, charybdis_dongle.overlay) | 10 reads | ~13342 tok |
| 01:27 | Session end: 60 writes across 8 files (charybdis_right_dongle.conf, build.yaml, charybdis_pmw3610.dtsi, charybdis_hardware_setup.md, charybdis_dongle.overlay) | 10 reads | ~13342 tok |
| 01:28 | Session end: 60 writes across 8 files (charybdis_right_dongle.conf, build.yaml, charybdis_pmw3610.dtsi, charybdis_hardware_setup.md, charybdis_dongle.overlay) | 10 reads | ~13342 tok |
| 01:28 | Session end: 60 writes across 8 files (charybdis_right_dongle.conf, build.yaml, charybdis_pmw3610.dtsi, charybdis_hardware_setup.md, charybdis_dongle.overlay) | 10 reads | ~13342 tok |
| 01:28 | Session end: 60 writes across 8 files (charybdis_right_dongle.conf, build.yaml, charybdis_pmw3610.dtsi, charybdis_hardware_setup.md, charybdis_dongle.overlay) | 10 reads | ~13342 tok |
| 01:28 | Edited build.yaml | 5→4 lines | ~46 |
| 01:28 | Edited build.yaml | 7→6 lines | ~52 |
| 01:29 | Session end: 62 writes across 8 files (charybdis_right_dongle.conf, build.yaml, charybdis_pmw3610.dtsi, charybdis_hardware_setup.md, charybdis_dongle.overlay) | 10 reads | ~13440 tok |
| 10:23 | Edited boards/shields/charybdis_dongle/charybdis_dongle.conf | modified BISECT() | ~114 |
| 10:23 | Edited build.yaml | modified TEMP() | ~71 |
| 10:27 | Edited build.yaml | modified TEMP() | ~77 |
| 10:26 | Bisect display continua: bitbang gpio-i2c TAMBÉM trava (periférico I2C inocentado!). ZMK upstream 29/06 confirmado. Prospector excluído do build (sem sources). Novo bisect: STATUS_SCREEN_CUSTOM=y sem impl → isola tema/fontes vs render/flush | charybdis_dongle.conf, overlay | ok | ~500 |
| 10:27 | Session end: 65 writes across 8 files (charybdis_right_dongle.conf, build.yaml, charybdis_pmw3610.dtsi, charybdis_hardware_setup.md, charybdis_dongle.overlay) | 10 reads | ~13710 tok |
| 10:31 | Edited build.yaml | 5→4 lines | ~46 |
| 10:31 | Edited build.yaml | 7→6 lines | ~52 |
| 10:31 | Session end: 67 writes across 8 files (charybdis_right_dongle.conf, build.yaml, charybdis_pmw3610.dtsi, charybdis_hardware_setup.md, charybdis_dongle.overlay) | 10 reads | ~13808 tok |
| 11:18 | Edited boards/shields/charybdis_dongle/charybdis_dongle.conf | modified FINAL() | ~97 |
| 11:18 | Edited build.yaml | modified TEMP() | ~71 |
| 11:18 | Edited build.yaml | modified TEMP() | ~77 |
| 11:20 | Bisect final: tema inocente (custom-null screen sobrevive). Crash = render/flush. Delta final vs referência: LV_COLOR_DEPTH_1 + BITS_PER_PIXEL=1 (16bpp em glue mono = overflow). Build 1bpp disparado | charybdis_dongle.conf, buglog | ok | ~500 |
| 11:20 | Session end: 70 writes across 8 files (charybdis_right_dongle.conf, build.yaml, charybdis_pmw3610.dtsi, charybdis_hardware_setup.md, charybdis_dongle.overlay) | 10 reads | ~14060 tok |
| 11:26 | Edited build.yaml | 5→4 lines | ~46 |
| 11:26 | Edited build.yaml | 7→6 lines | ~52 |
| 11:26 | Session end: 72 writes across 8 files (charybdis_right_dongle.conf, build.yaml, charybdis_pmw3610.dtsi, charybdis_hardware_setup.md, charybdis_dongle.overlay) | 10 reads | ~14158 tok |
| 11:58 | 🏆 BUG-024 RESOLVIDO: LV_COLOR_DEPTH_1 + BITS_PER_PIXEL=1. Widgets na tela + teclado funcionando. Display e módulo inocentes o tempo todo | charybdis_dongle.conf, buglog, cerebrum | ok | ~1k |
| 12:00 | Edited boards/shields/charybdis_dongle/charybdis_dongle.overlay | modified BLE() | ~309 |
| 12:00 | Edited boards/shields/charybdis_dongle/charybdis_dongle.conf | 4→2 lines | ~18 |
| 12:00 | Edited boards/shields/charybdis_dongle/charybdis_dongle.conf | 5→3 lines | ~35 |
| 12:00 | Edited boards/shields/charybdis_right_dongle/charybdis_right_dongle.conf | inline fix | ~10 |
| 12:02 | Edited ../../.claude/projects/-home-bgarciamoura-projects-zmk-charybdis/memory/charybdis_hardware_setup.md | inline fix | ~119 |
| 12:02 | Edited ../../.claude/projects/-home-bgarciamoura-projects-zmk-charybdis/memory/charybdis_hardware_setup.md | modified FICAM() | ~142 |
| 12:02 | Edited ../../.claude/projects/-home-bgarciamoura-projects-zmk-charybdis/memory/MEMORY.md | inline fix | ~76 |
| 12:03 | Session end: 79 writes across 9 files (charybdis_right_dongle.conf, build.yaml, charybdis_pmw3610.dtsi, charybdis_hardware_setup.md, charybdis_dongle.overlay) | 11 reads | ~14917 tok |
| 12:25 | Session end: 79 writes across 9 files (charybdis_right_dongle.conf, build.yaml, charybdis_pmw3610.dtsi, charybdis_hardware_setup.md, charybdis_dongle.overlay) | 11 reads | ~14917 tok |
| 12:33 | SESSÃO ENCERRADA COM SUCESSO TOTAL: trackball (bug-023) + display (bug-024/025) resolvidos e validados. 3 commits pushados (ad66393, 50995ac, 0e1c92c). Matriz completa buildada limpa | tudo | 🏆 | ~500 |
| 12:33 | Session end: 79 writes across 9 files (charybdis_right_dongle.conf, build.yaml, charybdis_pmw3610.dtsi, charybdis_hardware_setup.md, charybdis_dongle.overlay) | 11 reads | ~14917 tok |
| 12:35 | Session end: 79 writes across 9 files (charybdis_right_dongle.conf, build.yaml, charybdis_pmw3610.dtsi, charybdis_hardware_setup.md, charybdis_dongle.overlay) | 11 reads | ~14917 tok |
| 12:39 | Session end: 79 writes across 9 files (charybdis_right_dongle.conf, build.yaml, charybdis_pmw3610.dtsi, charybdis_hardware_setup.md, charybdis_dongle.overlay) | 11 reads | ~14917 tok |
| 12:40 | Session end: 79 writes across 9 files (charybdis_right_dongle.conf, build.yaml, charybdis_pmw3610.dtsi, charybdis_hardware_setup.md, charybdis_dongle.overlay) | 11 reads | ~14917 tok |
| 12:49 | Created config/keymaps/qwerty.keymap | — | ~3412 |
| 12:49 | Edited build.yaml | modified TEMP() | ~71 |
| 12:49 | Edited build.yaml | modified TEMP() | ~77 |
| 12:51 | Session end: 82 writes across 10 files (charybdis_right_dongle.conf, build.yaml, charybdis_pmw3610.dtsi, charybdis_hardware_setup.md, charybdis_dongle.overlay) | 12 reads | ~21022 tok |
| 12:53 | Edited build.yaml | 5→4 lines | ~46 |
| 12:53 | Edited build.yaml | 7→6 lines | ~52 |
| 12:57 | Keymap do Vial (Charybdis_vial_0.5.vil) portado pro qwerty.keymap: 6 camadas 1:1, HRM em S-G/H-;, macros→LC(LS()), USER→tog 6/7, SLOW/SCROLL preservadas. Build dongle OK | config/keymaps/qwerty.keymap, build.yaml | ok | ~2k |
| 12:54 | Session end: 84 writes across 10 files (charybdis_right_dongle.conf, build.yaml, charybdis_pmw3610.dtsi, charybdis_hardware_setup.md, charybdis_dongle.overlay) | 12 reads | ~21120 tok |
| 12:59 | Session end: 84 writes across 10 files (charybdis_right_dongle.conf, build.yaml, charybdis_pmw3610.dtsi, charybdis_hardware_setup.md, charybdis_dongle.overlay) | 12 reads | ~21120 tok |
| 13:02 | Edited config/keymaps/qwerty.keymap | inline fix | ~38 |
| 13:02 | Edited config/keymaps/qwerty.keymap | inline fix | ~27 |
| 13:02 | Edited config/keymaps/qwerty.keymap | inline fix | ~26 |
| 13:02 | Edited config/keymaps/qwerty.keymap | inline fix | ~23 |
| 13:02 | Edited config/keymaps/qwerty.keymap | inline fix | ~25 |
| 13:06 | Edited config/keymaps/qwerty.keymap | inline fix | ~25 |
| 13:03 | Session end: 90 writes across 10 files (charybdis_right_dongle.conf, build.yaml, charybdis_pmw3610.dtsi, charybdis_hardware_setup.md, charybdis_dongle.overlay) | 12 reads | ~21293 tok |
| 13:05 | Session end: 90 writes across 10 files (charybdis_right_dongle.conf, build.yaml, charybdis_pmw3610.dtsi, charybdis_hardware_setup.md, charybdis_dongle.overlay) | 12 reads | ~21293 tok |
| 13:08 | Keymap Vial validado pelo usuário (thumbs corrigidos: BSPC/L2, SPC/L1, LCLK | DEL/L1, RET/L2). Build final da matriz completa disparado; commit+push na sequência | config/keymaps/qwerty.keymap | ok | ~300 |
| 13:08 | Session end: 90 writes across 10 files (charybdis_right_dongle.conf, build.yaml, charybdis_pmw3610.dtsi, charybdis_hardware_setup.md, charybdis_dongle.overlay) | 12 reads | ~21293 tok |
