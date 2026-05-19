# Cerebrum

> OpenWolf's learning memory. Updated automatically as the AI learns from interactions.
> Do not edit manually unless correcting an error.
> Last updated: 2026-05-08

## User Preferences

<!-- How the user likes things done. Code style, tools, patterns, communication. -->

## Key Learnings

- **Project:** zmk-charybdis
- **Description:** [![.github/workflows/build.yml](https://github.com/280Zo/charybdis-wireless-mini-zmk-firmware/actions/workflows/build.yml/badge.svg)](https://github.com/280Zo/charybdis-wireless-mini-zmk-firmware/acti

### Trackball sensor — alternativas PMW3360 (pesquisado 2026-05-07)

Repo atual usa `zmk-pmw3610-driver` (declarado em `config/west.yml`, comportamento em `config/trackball/charybdis_pointer.dtsi` com `compatible = "pixart,pmw3610"`).

**Não há driver PMW3360 no ZMK upstream.** PR #1163 (Luberry, PMW33XX genérico) foi fechado por inatividade em abril/2026 — mantenedor declarou que não mergeia mais drivers de pointer até a infraestrutura HID/event estabilizar.

**Módulos out-of-tree para PMW3360:**
- `george-norton/zmk-driver-pmw3360` — mais polido. Polled ou IRQ, CPI/orientação configuráveis, thread dedicada opcional. **Primeira escolha se for migrar.**
- `KOHSUK/zmk-pmw3360-driver` (branch `pmw3360`) — "fork to play", experimental. Fork do bullwinkle3000/pmw3610.
- `zmkfirmware/zmk` PR #1163 — base para patch local se necessário.

**Cuidado:** `trentrand/zmk-pmw3360-driver` apesar do nome é driver PMW3610 (fork do badjeff). Não serve para 3360.

**Custo de migrar 3610 → 3360:** consumo de bateria significativamente maior — motivo pelo qual o ecossistema ZMK adotou 3610. Mudanças necessárias: trocar módulo em `west.yml`, mudar `compatible` em `charybdis_pointer.dtsi`, ajustar Kconfig (`CONFIG_PMW3610` → `CONFIG_PMW3360`).

**Linhagem dos drivers:** `ufan` → `bullwinkle3000` → forks atuais. QMK unificou 3360/3389 (diferem só em blobs SROM e get/set de CPI).

### Hardware atual do usuário (2026-05-07)

- **Halves:** nice!nano v2 (esquerda + direita).
- **Dongle:** XIAO-nRF52840 (XIAO BLE), atualmente sem display.
- **Display planejado:** Waveshare 1.69" Round LCD com Touch (compatível com Prospector via ST7789V2).
- **Sem APDS9960:** o sensor de luz ambiente opcional do Prospector não foi adquirido.
- **Grupo de build ativo:** `dongle_standard_xiao` (criado 2026-05-07). Ao receber o display, trocar para `dongle_prospector_xiao_no_sensor` (já no build.yaml comentado).

**Verificado:** o shield `charybdis_dongle` é MCU-agnóstico — overlay só usa abstrações (kscan-mock, BLE central, split inputs, &i2c1). Não tem dependência de pinos do nice!nano, então roda em XIAO BLE sem mudanças.

**Build confirmado em 2026-05-07:** o grupo `dongle_standard_xiao` compila os 3 alvos (left/right dongle em nice_nano, dongle em xiao_ble) + settings_reset em 11m39s no docker local. Uso de memória do dongle xiao_ble: FLASH 35% (286 KB / 788 KB), RAM 38% (100 KB / 256 KB). Halves nice_nano: FLASH ~24%, RAM ~14%.

### Bastardkb TBK Mini — matrix pinout (2026-05-08)

A TBK Mini (FLEX PCB, design 2022 Quentin Lebastard) compartilha o **mesmo pinout** do Charybdis Wireless Mini quando montada no Elite-C Holder. Confirmado cruzando `keyboards/bastardkb/tbkmini/promicro/keyboard.json` (QMK) com `boards/shields/charybdis_right_bt/charybdis_right_bt.overlay` deste repo.

**Tamanho da matriz:** 4 rows × 6 cols (3 keyboard rows + 1 thumb row, layout `LAYOUT_split_3x6_3` = 3 keys no thumb cluster). Total 42 keys (21 por lado).

**Diode direction:** `row2col` (QMK `ROW2COL`).

**Pin mapping AVR (Elite-C/Pro Micro silkscreen) → ZMK `&pro_micro N`:**

| QMK AVR pin | Pro Micro silkscreen | ZMK `&pro_micro N` |
|-------------|----------------------|--------------------|
| F4 | A3 / D21 | 21 |
| F5 | A2 / D20 | 20 |
| F6 | A1 / D19 | 19 |
| F7 | A0 / D18 | 18 |
| B1 | D15 (SCK) | 15 |
| B3 | D14 (MISO) | 14 |
| B2 | D16 (MOSI) | 16 |
| B6 | D10 | 10 |
| B5 | D9  | 9 |
| B4 | D8  | 8 |
| E6 | D7  | 7 |
| D7 | D6  | 6 |
| C6 | D5  | 5 |
| D4 | D4  | 4 |
| D0 | D3 (SCL) | 3 |
| D1 | D2 (SDA) | 2 |
| D3 | D1 (TX1) | 1 |
| D2 | D0 (RX1) | 0 |

**TBK Mini cols (left→right no lado ESQUERDO):** F6, F5, B6, D7, E6, B4 → ZMK: `19, 20, 10, 6, 7, 8`
**TBK Mini rows (top→bottom):** F7, C6, D4, B5 → ZMK: `18, 5, 4, 9`
**Lado direito:** mesmos pinos físicos (split mirror é feito no firmware via matrix transform com `col-offset = <6>`).

**Sem encoders, sem OLED, sem trackball** no design original da TBK Mini (é o "Charybdis sem trackball"). RGB underglow é via WS2812 no pin D3 (`&pro_micro 3`) com 21 LEDs por lado, mas ZMK pode omitir/desabilitar.

Fontes: github.com/qmk/qmk_firmware/tree/master/keyboards/bastardkb/tbkmini, github.com/Bastardkb/TBK-Mini, github.com/Bastardkb/Elite-C-holder.

### PMW3610-Module 20240425 chinês (AliExpress) — datasheet do vendedor (2026-05-17)

Módulo redondo 32mm de diâmetro com sensor PMW3610 + LDO onboard. Pinout (do datasheet enviado pelo vendedor):

**Lado esquerdo (5 pads vertical):**
- SDIO, SCLK, NCS, NRESET, MOT

**Lado direito (4 pads em bloco 2×2):**
- Linha de cima: VDDIO, GND
- Linha de baixo: VDD, GND

**Voltagens recomendadas:**
| Symbol | Min | Typical | Max |
|---|---|---|---|
| VDD (core, via LDO 2.0V) | 1.7V | 2V | **6.0V** |
| VDDIO (logic) | 1.7V | 2V | **3.3V** |

**Insights:**
- VDD aceita até 6V (LDO 2.0V onboard reduz). Pode ser alimentado por +5V do USB/VBUS.
- VDDIO é o que comunica com o MCU — DEVE ser 3.3V quando lógica do MCU for 3.3V (nice!nano case). **Não pode receber 5V — queima o sensor.**
- VDD e VDDIO são pads SEPARADOS — não fazer solder bridge entre eles.
- Os dois GND do bloco direito são iguais — usar só um.
- NRESET pode ficar flutuante (sensor tem reset interno).
- MOT é o pino de motion interrupt (active low). Driver `zmk-pmw3610-driver` suporta polled OU IRQ — se conectado, ativa modo IRQ (mais eficiente).
- 3-wire SPI: SDIO único bidirecional (não tem MOSI/MISO separados).

**Mapeamento sensor → Bastardkb Elite-C Holder 2.1 stock + nice!nano:**
| Pad sensor | Conexão | Pino físico nice!nano |
|---|---|---|
| VDD | header J8 pino 1 (+5V) OU jumper pro VCC | RAW (5V) ou VCC (3.3V) |
| VDDIO | **jumper direto** | VCC pad (3.3V) |
| GND | header J8 pino 6 | GND |
| SDIO | header J8 pino 3 (mosi_r) | D16 silk = P0.10 |
| SCLK | header J8 pino 4 (sc_r) | D15 silk = P1.13 |
| NCS | **jumper direto** (pino 2 do J8 vai pra F0 inexistente) | D3 silk = P0.20 |
| MOT | **jumper direto** | D0 silk = P0.06 |
| NRESET | NÃO CONECTAR | — |

Pinctrl no firmware (`charybdis_pmw3610.dtsi`) precisa ser ajustado: SCK em P1.13, SDIO em P0.10 (MOSI+MISO no mesmo pino). CS em P0.20 e IRQ em P0.06 já estão corretos.

**CONFIRMADO FUNCIONAL 2026-05-17:** pinctrl SCK=P1.13/MOSI=P0.10/MISO=P0.10 + cs-gpios=P0.20 + irq-gpios=P0.06 ACTIVE_LOW+PULL_UP funciona. Driver `zmk-pmw3610-driver` (badjeff fork em 280Zo) inicializa via `pmw3610_async_init`, ativa LED VCSEL, e stream contínuo de `pmw3610_report_data: x/y: N/N` chega ao input subsystem. Confirmado também: `force-awake` + `force-awake-4ms-mode` + `CONFIG_PMW3610_ALT_SMART_ALGORITHM=y` rodam sem warnings. Tempo de init total: ~1-3 segundos pós-boot até primeira leitura.

### Bastardkb Elite-C Holder 2.1 stock + nice!nano — pegadinha do CS (2026-05-08)

A Bastardkb Elite-C Holder 2.1 stock roteia o pad **CS** do header SPI do trackball para o pino **F0** do footprint Elite-C. **F0 não existe no nice!nano** (pad exclusivo Elite-C). Resultado: CS solto, sensor SPI nunca selecionado.

**Pinout SPI da holder 2.1 stock (J8 trackball header, lido do schematic KiCad oficial 2026-05-17):**

J8 é um header 1×6 fêmea. Ordem dos pinos (top→bottom, y crescente no schematic):

| Pino J8 | Net | Pad Elite-C | Pro Micro silk | nice!nano GPIO |
|---|---|---|---|---|
| 1 (topo) | **+5V** | RAW | RAW | VBUS (5V via USB) |
| 2 | ss_r (CS) | 29 (F0) | **(não existe)** | — flutuante |
| 3 | mosi_r | 14 (B2) | D16 | P0.10 |
| 4 | sc_r (SCK) | 16 (B1) | D15 | P1.13 |
| 5 | miso_r | 15 (B3) | D14 | P1.11 |
| 6 | GND | GND | GND | — |

J7 = trackball header esquerdo (espelhado, nets ss_l/mosi_l/miso_l/sc_l). Charybdis padrão usa só J8 (trackball na direita).

**Solução comunitária:** fork `olidacombe/Elite-C-holder@nicenano` que reroteia CS pra um pino que existe no nice!nano. É o que o build guide do 280Zo (autor desse repo) linka.

**Workaround sem trocar holder:** jumper wire do pad SS do sensor PMW3360 PCB Rev 2.0 até um GPIO livre do nice!nano (ex: D3 = P0.20). Documentado em `TRACKBALL_MOD.md` na raiz do repo.

**Sensor:** Bastardkb PMW3360 Sensor PCB Rev 2.0. Pinout: GND, MISO, SCK, MOSI, SS, 3.3V. **NÃO expõe MOTION/IRQ** — driver tem que usar polled mode.

### ZMK split BLE — descobertas críticas (2026-05-08)

**1. Central scaneia por UUID, não por nome:**
- O `local-name = "charybdis_left/right"` no `charybdis_dongle.overlay` é APENAS um label/identificador interno do slot
- O central scaneia por `ZMK_SPLIT_BT_SERVICE_UUID` (128 bits)
- Half precisa anunciar com esse UUID + advertising tipo `BT_DATA_UUID128_ALL`
- Verificado em `zmk/app/src/split/bluetooth/central.c` (split_central_eir_parse) e `zmk/app/src/split/bluetooth/peripheral.c` (zmk_ble_ad)

**2. Half com bond residual faz directed advertising e fica INVISÍVEL pra scanners genéricos:**
- Em `peripheral.c:60-72`, se há bond presente, peripheral usa `BT_LE_ADV_CONN_DIR(&central_addr)` ao invés de `BT_LE_ADV_CONN_FAST_2 + UUID128`
- Directed adv é filtrado pelo controller — só o central específico vê
- Sintoma: half some completamente do nRF Connect mesmo "rodando"
- Fix: settings_reset (passa `bt_unpair(BT_ID_DEFAULT, NULL)`)

**3. ZMK limita BT_DEVICE_NAME_MAX=16 (não Zephyr default 28):**
- `zmk/app/Kconfig:247` força default 16, comentário cita constraint de advertising data
- Assert em `hci_core.c:4440` é estrito `<`, então **máximo efetivo é 15 chars**
- Tentar 16 chars (ex: "charybdis dongle") → falha de build com `BUILD_ASSERT(DEVICE_NAME_LEN < CONFIG_BT_DEVICE_NAME_MAX)`

### CONFIG_ZMK_SPLIT_ROLE_CENTRAL — bug crítico do 280Zo repo (2026-05-08)

**Bug original do repo:** `boards/shields/charybdis_right_dongle/charybdis_right_dongle.conf` NÃO declarava `CONFIG_ZMK_SPLIT_ROLE_CENTRAL=n`. ZMK upstream defaulta pra **central** quando não explícito → half scaneia ao invés de advertise → invisível pro mundo BLE.

**Comparação com left_dongle:** `charybdis_left_dongle.conf` tem a linha explícita `CONFIG_ZMK_SPLIT_ROLE_CENTRAL=n`. Right não tinha.

**Sintoma:** Half boota OK (LED 1Hz), `nRF Connect` mostra dongle mas não a half, dongle scan logs nunca capturam a half (zero `split_central_device_found`).

**Fix aplicado:** linha `CONFIG_ZMK_SPLIT_ROLE_CENTRAL=n` adicionada em `charybdis_right_dongle.conf`. Verificado funcional em placa de teste — half passou a aparecer no scanner.

### PMW3610 driver instabilidade quando sensor real é 3360 com CS solto (2026-05-08)

Driver `CONFIG_PMW3610_ALT=y` (do `280Zo/zmk-pmw3610-driver`) **panica/crash em loop** quando tenta init e o sensor não responde (porque é PMW3360 não 3610, ou porque CS está solto). Resultado: half boota, driver crashea, watchdog reset, bootloader Adafruit detecta múltiplos crashes consecutivos e fica em DFU mode automaticamente.

**Sintoma classico:** single-tap reset → drive `NICENANO` aparece sozinho (auto-DFU). Normalmente nice!nano só entra em DFU com double-tap.

**Workaround pra debug isolado:** `CONFIG_PMW3610_ALT=n` + override em overlay:
```
&trackball { status = "disabled"; };
&trackball_split { status = "disabled"; };
```
Sem o segundo override, o linker falha com `undefined reference to __device_dts_ord_NNN` porque `input_split.c` referencia o trackball device por ordinal, e sem driver compilado o symbol não existe.

### Adafruit nRF52 bootloader — auto-DFU on app failure (2026-05-08)

Quando o app crasha múltiplas vezes em sequência (watchdog reset rápido), o bootloader Adafruit detecta o loop e fica em DFU mode automaticamente, sem precisar de double-tap.

**Sinal**: single-tap reset monta drive UF2 (`NICENANO`) ao invés de bootar app. Comportamento normal seria double-tap obrigatório.

**Útil como diagnóstico:** se vê single-tap mostrando drive, app está crashando logo após boot.

### USB CDC logging — gotchas (2026-05-08, atualizado 2026-05-16)

**`CONFIG_LOG_DEFAULT_LEVEL=4`** liga DEBUG em TODOS os módulos, incluindo MPU, USB driver, OS scheduler — log fica saturado de noise irrelevante. Para debugar BT/ZMK específico:
- Manter `LOG_DEFAULT_LEVEL=1` (só ERROR)
- Setar individualmente: `CONFIG_BT_LOG_LEVEL_DBG=y`
- ZMK_LOG_LEVEL=4 já vem do snippet `zmk-usb-logging`

**Snippet `zmk-usb-logging`** (ativado via `ENABLE_USB_LOGGING="true"` em `local-build/build_setup.sh`):
- Aplica a TODOS os targets do build matrix
- Auto-desabilita `studio-rpc-usb-uart` em targets que normalmente teriam (charybdis_dongle, charybdis_right_bt) → ZMK Studio não conecta enquanto isso
- Adiciona ~80 KB ao firmware (USB CDC + LOG stack)
- Para reverter: setar `false` e rebuildar

**Sintomas confirmados quando USB_LOGGING=true no dongle (bug-009, 2026-05-16):**
- **ZMK Studio (browser) trava e fecha** ao conectar: Studio abre a porta esperando RPC binário (MessagePack/protobuf), mas o dongle responde com texto de log (`[00:00:01.234,000] <dbg> bt_hci: ...`). Parser binário entra em loop tentando decodificar lixo, satura UI thread.
- **Tera Term trava** logo após abrir a porta: boot do dongle com `BT_LOG_LEVEL_DBG=y` + buffer 16K despeja burst gigante de logs (scan, GAP, advertising, connection params), Tera Term em modo VT tenta parsear/colorizar e congela.

**Pra ler logs sem travar terminal:** usar `tio /dev/ttyACM0 -b 115200` ou `cat /dev/ttyACM0` (raw, não interpretam VT100/ANSI).

### Solda fria em diodos da matrix — sintoma "doubling" + falso negativo do multímetro (2026-05-17)

**Sintoma:** uma única tecla emite dois caracteres no host. Sempre o mesmo par e sempre nas mesmas colunas (ex: pressionar U **ou** I dispara "iu"; J **ou** K dispara "kj"). Quando o par calha em positions de combo, o output muda — ex: M+vírgula = positions 31+32 = combo_app_windows = `LA(GRAVE)` = backtick `` ` ``.

**Causa:** solda fria num ou mais diodos da matrix (cols envolvidas). O contato intermitente de alta impedância permite que o GPIO scan da kscan leia "high" pra mais de uma coluna quando a row strobea, porque a perna do diodo encosta levemente em algo (pad vizinho, perna de outro diodo, trilha) sem soldagem efetiva.

**Pista decisiva:** *passar o dedo sobre os diodos da região faz o sintoma sumir temporariamente* — a pressão mínima do dedo reassenta a perna no pad.

**Por que multímetro em continuidade dá falso negativo:** modo continuidade injeta corrente alta (mA); a junta fria é capaz de conduzir µA suficientes pro ADC/GPIO read mas falha sob carga maior. Continuidade entre os pads do MCU não acusa nada. **Teste melhor:** continuidade direto entre cátodos dos diodos suspeitos, ou inspeção visual com lupa procurando solda fosca/côncava sem menisco brilhante.

**Por que ZMK Studio não corrige:** Studio edita binding numa `(row,col)` lógica. O doubling acontece na camada **kscan**, antes do keymap rodar. A kscan reporta dois eventos `(row,col)` distintos pra um único press físico, e o Studio não tem acesso a essa camada.

**Fix:** reflow dos diodos suspeitos (340-360°C, ~1-2s no pino+pad, flux fresco se a solda parecer ressecada). Se voltar após reflow → pad lifted ou diodo internamente fraturado → trocar o componente.

### Hardware ESD damage — sintomas (2026-05-08)

Em uma das placas montadas pelo usuário, o nRF52840 mostrou comportamento errático após soldagem:
- BT_DEVICE_NAME advertise com caracteres aleatórios (RAM corrompida sendo lida)
- BLE advertising intermitente (placa "aparece e some" no scanner)
- USB CDC não enumera (mas DFU mode via bootloader USB ainda funciona)
- Settings_reset duplo + flash limpo não resolve
- Mesmo firmware funciona perfeitamente em outra placa do mesmo modelo

**Diagnóstico:** ESD damage durante soldagem (ferro de solda sem aterramento, dedos sem pulseira ESD). Solução: trocar o módulo nice!nano. Holder, fios, sensor, matrix tipicamente continuam OK.

**Prevenção pra próximas montagens:**
- Pulseira ESD aterrada (ou tocar metal aterrado antes de manusear)
- Ferro com temperatura controlada (~350°C, max 30s no pino)
- Não força stress mecânico nos pads do nRF52840
- Manter umidade ambiente acima de 40% se possível

## Do-Not-Repeat

<!-- Mistakes made and corrected. Each entry prevents the same mistake recurring. -->
<!-- Format: [YYYY-MM-DD] Description of what went wrong and what to do instead. -->

- ~~[2026-05-07] Docker / docker-compose NÃO estão disponíveis no shell do assistente~~ **REVOGADO em 2026-05-16**: Docker 29.4.3 (`/usr/bin/docker`) + docker-compose (`/usr/local/bin/docker-compose`) agora disponíveis no shell WSL2. Pode invocar `docker-compose run --rm builder` em `local-build/` diretamente. Build leva ~12min — rodar em background com `run_in_background: true` e usar Read no log file pra checar progresso, ou aguardar a notificação de conclusão.
- [2026-05-07] **Não pipe direto comandos que podem falhar** (`cmd | tail -N`) — o exit code do pipeline é o do último comando, então erro 127 do `cmd` vira exit 0 do `tail`. Usar `cmd 2>&1; echo "exit=$?"` ou bash `-o pipefail`, ou rodar o comando puro e checar o output depois. **Reincidente 2026-05-16:** rodei `docker-compose run --rm builder 2>&1 | tee /tmp/zmk-build.log` em background — west update falhou mas tee deu exit 0, mascarou erro. Pra captura de log de build longo: usar `cmd > arquivo.log 2>&1` (sem pipe) ou `set -o pipefail; cmd | tee arquivo.log`.
- [2026-05-08] **Nunca setar `CONFIG_LOG_DEFAULT_LEVEL=4`** pra debug — fica saturado de MPU/USB/OS noise. Sempre usar log levels específicos (ex: `CONFIG_BT_LOG_LEVEL_DBG=y`) e manter DEFAULT em 1 (ERROR).
- [2026-05-08] **`local-name` no dongle overlay NÃO É filtro de scan BLE** — é só label do slot do peripheral. ZMK split central scaneia por UUID 128-bit (`ZMK_SPLIT_BT_SERVICE_UUID`). Não tentar setar nomes BLE pra fazer matching.
- [2026-05-08] **Limite ZMK BT_DEVICE_NAME_MAX é 15 chars (não 16, não 28)** — assert estrito `<` em `hci_core.c:4440`. Nomes ≥16 chars quebram build com `BUILD_ASSERT`.
- [2026-05-08] **Quando desabilitar driver de device tree, desabilitar TAMBÉM os nós que usam ele.** Se `&device { status = "okay" }` mas driver não compila, linker falha com `undefined reference to __device_dts_ord_NNN`. Override pra `disabled` no shield overlay.

- [2026-05-16] **Build local ZMK falha em runs subsequentes por mode-bit drift dos módulos west.** `local-build/build_setup.sh:62` faz `chmod -R 777 .west zmk zephyr modules zmk-pmw3610-driver prospector-zmk-module` (necessário pra usuário poder deletar artefatos criados como root pelo container). Isso muda mode bits 644→755 em todo arquivo dos módulos. `git` registra como modified. No próximo build, `west update` faz fetch+checkout dos módulos; se houver novos commits upstream, checkout falha com `error: Your local changes to the following files would be overwritten by checkout`. **Workaround manual antes do build:** `for m in zmk zephyr modules zmk-pmw3610-driver prospector-zmk-module; do git -C $m -c safe.directory=* checkout .; done`. **Fix durável (não aplicado ainda):** adicionar `git -C <mod> config core.filemode false` no build_setup.sh pra cada módulo antes do west update, ou mover o `chmod 777` pra dentro de gitignore/ignored paths apenas (build/, firmwares/).

- [2026-05-17] **Edits ao `charybdis_pmw3610.dtsi` podem ser revertidos silenciosamente entre builds.** Cheguei a editar o pinctrl pra P1.13/P0.10 numa sessão, fui buildar, o build incluiu o driver mas no boot NENHUM log do `PMW3610_ALT` saía (driver init silencioso). Re-checkei o arquivo e estava com os pinos ANTIGOS (P0.08/P0.17). Edit foi revertido entre sessões — provavelmente por algum hook do OpenWolf que não conheço bem, ou edit não foi flushed antes do build começar. **Regra:** sempre confirmar com `Read` ou `grep` os arquivos críticos do device tree DEPOIS de editar e ANTES de iniciar build longo. Se driver inicializa sem nenhum log mas o build incluiu o módulo, suspeitar do pinctrl primeiro.

## Decision Log

<!-- Significant technical decisions with rationale. Why X was chosen over Y. -->

### Layer order canônico (verificado 2026-05-17)

`config/keymaps/*.keymap` definem **8 layers**, nesta ordem:

| Idx | Nome     |
| --- | -------- |
| 0   | BASE     |
| 1   | NUM      |
| 2   | NAV      |
| 3   | SYM      |
| 4   | GAME     |
| 5   | EXTRAS   |
| 6   | SLOW     |
| 7   | SCROLL   |

**Não existe layer MOUSE** — o CLAUDE.md original listava "MOUSE" entre EXTRAS e SLOW, mas estava incorreto. Corrigido em 2026-05-17.

Índices referenciados por:
- `config/trackball/charybdis_pointer.dtsi` — usa SLOW (6) e SCROLL (7) pra overrides de input processor
- Combos em `config/keymap_features/combos.dtsi` — campo `layers`

**Não reordene** sem atualizar todos esses arquivos.

Referência completa de edição: `KEYMAP_EDITING.md` na raiz.
