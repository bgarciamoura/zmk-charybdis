# Editando o keymap

Referência de quais arquivos editar pra cada tipo de mudança no keymap. Tudo
no `nvim` direto — não precisa de editor GUI.

## TL;DR — qual arquivo pra qual mudança

| Quero mudar...                            | Edito...                                                         |
| ----------------------------------------- | ---------------------------------------------------------------- |
| Qual tecla faz o quê numa layer           | `config/keymaps/<layout>.keymap`                                 |
| HRM / tap-dance / layer-tap customizado   | `config/keymap_features/behaviors.dtsi`                          |
| Combos (2+ teclas simultâneas)            | `config/keymap_features/combos.dtsi`                             |
| Macros (sequências, parametrizados)       | `config/keymap_features/macros.dtsi`                             |
| Velocidade / scroll / precisão trackball  | `config/trackball/charybdis_pointer.dtsi`                        |
| Posição física das teclas (Studio/drawer) | `config/charybdis-layouts.dtsi`                                  |
| Qual layout vai pro firmware              | `build.yaml` (campo `keymap:`)                                   |

## Keymaps disponíveis

Vivem em `config/keymaps/` — um arquivo `.keymap` por layout:

- `qwerty.keymap`
- `colemak_dh.keymap`
- `canary.keymap`
- `focal.keymap`
- `graphite.keymap`

Cada um inclui automaticamente `behaviors.dtsi`, `combos.dtsi` e `macros.dtsi`
de `config/keymap_features/`, então features compartilhadas valem pra todos.

## Layers (índices canônicos)

**Ordem fixa em todos os keymaps** — vários arquivos referenciam por índice,
**não reordene**:

| Idx | Layer    | Pra que serve                                  |
| --- | -------- | ---------------------------------------------- |
| 0   | `BASE`   | Letras + thumbs principais                     |
| 1   | `NUM`    | Números e símbolos numéricos                   |
| 2   | `NAV`    | Setas, navegação, edição                       |
| 3   | `SYM`    | Símbolos                                       |
| 4   | `GAME`   | Layout sem HRMs pra jogos                      |
| 5   | `EXTRAS` | BT, output, ext_power, reset, bootloader       |
| 6   | `SLOW`   | Trackball em modo precisão (CPI reduzido)      |
| 7   | `SCROLL` | Trackball em modo scroll                       |

> `SLOW` e `SCROLL` são referenciados por índice em
> `config/trackball/charybdis_pointer.dtsi`. Se a ordem mudar lá, mude aqui também.

## Numeração das posições (key positions)

Charybdis 3x6 + 3+2 thumbs = 41 posições. Mesma indexação em todos os keymaps,
combos e masks:

```
╭──────┬──────┬──────┬──────┬──────┬──────╮  ╭──────┬──────┬──────┬──────┬──────┬──────╮
   00     01     02     03    04      05        06     07     08     09     10     11
├──────┼──────┼──────┼──────┼──────┼──────┤  ├──────┼──────┼──────┼──────┼──────┼──────┤
   12     13     14     15    16      17        18     19     20     21     22     23
├──────┼──────┼──────┼──────┼──────┼──────┤  ├──────┼──────┼──────┼──────┼──────┼──────┤
   24     25     26     27    28      29        30     31     32     33     34     35
╰──────┴──────┴──────┼──────┼──────┼──────┤  ├──────┼──────┼──────┴──────┴──────┴──────╯
                        36     37     38        39     40
                     ╰──────┴──────┴──────╯  ╰──────┴──────╯
```

Masks pré-definidas em `behaviors.dtsi`:

- `KEYS_L` — mão esquerda (sem polegar): `0 1 2 3 4 5 12 13 14 15 16 17 24 25 26 27 28 29 36 37 38`
- `KEYS_R` — mão direita (sem polegar): `6 7 8 9 10 11 18 19 20 21 22 23 30 31 32 33 34 35 39 40`
- `THUMBS` — todos os polegares: `36 37 38 39 40`

## O que mora em cada arquivo

### `config/keymaps/<layout>.keymap`

Bindings por layer. Cada layer tem `bindings = < ... >;` com 41 entradas (uma por
posição). Behaviors customizados (`&ht_left`, `&td_layers`, `&mm_cm_sc`, etc.) são
definidos em `behaviors.dtsi` ou `macros.dtsi` — você só usa aqui.

Exemplo de behaviors usados na BASE do qwerty:
- `&kp <KEY>` — keypress simples
- `&ht_left <MOD> <KEY>` / `&ht_right <MOD> <KEY>` — home-row mod
- `&ht_left_tp <MOD> <KEY>` / `&ht_right_tp <MOD> <KEY>` — HRM com timing pra polegar
- `&td_layers` — tap-dance que muda de layer
- `&td_esc_scrl_slow`, `&td_clk`, `&td_bs`, `&td_space_nav` — tap-dances dos polegares
- `&mm_cm_sc`, `&mm_pr_col`, `&mm_qm_ex` — mod-morphs (caractere muda com shift)
- `&clip_hist` — macro de clipboard

### `config/keymap_features/behaviors.dtsi`

- Masks `KEYS_L`, `KEYS_R`, `THUMBS`
- Definições de home-row mods (`ht_left`, `ht_right`, `ht_left_tp`, `ht_right_tp`)
- Tap-dances dos polegares e do trackball
- Mod-morphs (símbolos que mudam com shift)
- Timings (`tapping-term-ms`, `quick-tap-ms`, etc.)

Mexa aqui pra ajustar **comportamento** das teclas especiais. Mudanças afetam
todos os layouts.

### `config/keymap_features/combos.dtsi`

Combos do tipo "aperta X+Y juntos = Z". Cada combo define:
- `key-positions` — quais posições disparam (usa os índices da figura acima)
- `bindings` — o que acontece quando ativa
- `layers` — em quais layers o combo é válido (omitir = todas)
- `timeout-ms` — janela de tempo

### `config/keymap_features/macros.dtsi`

Macros (sequências) e macros parametrizados. Tudo que começa com `&` no keymap
e não é behaviour padrão ZMK provavelmente está aqui ou em `behaviors.dtsi`.

### `config/trackball/charybdis_pointer.dtsi`

Configuração de input processor do PMW3610 com overrides por layer:
- Velocidade / sensitivity base
- Layer SCROLL (7) — converte movimento em scroll
- Layer SLOW (6) — reduz CPI pra precisão

Se mudar a **ordem das layers** nos keymaps, atualize as referências `<7>` e
`<6>` aqui também.

### `config/charybdis-layouts.dtsi`

Posição física X/Y/W/H de cada tecla. Usado por:
- ZMK Studio (renderiza o teclado na UI)
- `keymap-drawer` (gera os SVG/PNG em `keymap-drawer/`)

**Não afeta o que cada tecla faz** — só onde ela aparece desenhada.

## Trocando o keymap ativo no firmware

`build.yaml` controla. O firmware é flashado com o(s) `keymap:` listado(s) em
cada entry. Pra trocar de `qwerty` pra `colemak_dh`:

```yaml
- name: dongle_standard_xiao
  board: xiao_ble//zmk
  keymap:
    - qwerty           # ← comentar
    - colemak_dh       # ← descomentar
```

Pode listar múltiplos — gera um `.uf2` por combinação de shield × keymap.

> O build copia `config/keymaps/<name>.keymap` pra `config/<target>.keymap` antes
> de invocar o `west build`. Você nunca edita `config/<target>.keymap` direto —
> ele é regenerado.

**Estado atual do build matrix** (2026-05-17): só `settings_reset` e
`dongle_standard_xiao` ativos. Os outros grupos (`bt`, `dongle_standard_nano`,
todos os Prospector) estão comentados — descomente quando for usar.

## Fluxo típico de edição

```bash
# 1. Editar o keymap
nvim config/keymaps/qwerty.keymap

# 2. (Opcional) Mexer em features compartilhadas
nvim config/keymap_features/behaviors.dtsi
nvim config/keymap_features/combos.dtsi
nvim config/keymap_features/macros.dtsi

# 3. Build local
cd local-build
docker-compose run --rm builder

# 4. Flashar — os .uf2 ficam em firmwares/<format>/<keymap>/
```

Pra debug do build:

```bash
cd local-build
docker-compose run --rm --entrypoint bash builder
# dentro do container: west build ... manualmente
```

Pra logging USB (caro em bateria, off por padrão): editar
`local-build/build_setup.sh` e setar `ENABLE_USB_LOGGING="true"`.

## Renderização visual (keymap-drawer)

Diagramas em `keymap-drawer/` são **auto-gerados** pelo workflow
`.github/workflows/draw_keymaps.yml` em todo push pra `main`. **Não edite à
mão** os SVG/PNG em `keymap-drawer/all_layers/` ou `keymap-drawer/stacked/`.

Tuning de aparência:
- `keymap-drawer/configs/config-stacked.yaml` — estilo dos diagramas empilhados
- `keymap-drawer/configs/config-all-layers.yaml` — estilo das layers completas
- `keymap-drawer/configs/config-combo.yaml` — estilo dos combos
- `keymap-drawer/stacked/composite-template.html` — template HTML do render composto

Pra rodar localmente, veja `keymap-drawer/README.md`.

## Gotchas

- **Não reordene as layers.** SLOW=6 e SCROLL=7 são referenciados por índice no
  trackball. Se inverter, o trackball vai entrar em modo errado.
- **Não edite `config/<target>.keymap`.** É gerado pelo build a partir de
  `config/keymaps/<name>.keymap`. Suas mudanças são sobrescritas.
- **Não use `#include` com paths de subdiretório** em `config/charybdis/*.conf`.
  ZMK só busca no topo de `${ZMK_CONFIG}`. O build copia esses arquivos pra
  `config/` antes de chamar o `west build`.
- **`settings_reset` é especial** — shield upstream do ZMK, não nosso. O
  artefato fica em `firmwares/settings_reset.uf2` (na raiz, sem subpasta) pra
  aparecer limpo nos releases.
- **`studio-rpc-usb-uart` é automático.** Não adicione manualmente em
  `build.yaml` — o `build_setup.sh` injeta sozinho pros targets USB-central
  (`charybdis_right_bt`, `charybdis_dongle`). É desativado quando USB logging
  está on (mesma porta CDC).

## Onde **não** mexer pra mudar keymap

- `boards/shields/charybdis_*/` — hardware (matrix, GPIOs, sensor). Mexer aqui
  quebra o hardware, não muda o keymap.
- `config/west.yml` — dependências (ZMK upstream, driver PMW3610, prospector).
- `config/charybdis/*.conf` — Kconfig de runtime (BT, sleep, deep sleep, etc.),
  não bindings.
- `firmwares/` — output do build. Sobrescrito a cada build.
