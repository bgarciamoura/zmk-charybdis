# Trackball PMW3610 — Bastardkb Elite-C Holder 2.1 stock + nice!nano

> **Quando aplicar:** se você tem o conjunto `Bastardkb Elite-C Holder 2.1 stock` + `nice!nano` (ou clone SuperMini nRF52840) + um sensor `PMW3610-Module` (módulo redondo 32mm chinês, vendido em AliExpress como "PMW3610-Module 20240425" ou similar), e quer integrar o trackball ao Charybdis Wireless.
>
> O `charybdis_pmw3610.dtsi` original desse repo foi feito pros PCBs forkados ([`olidacombe/Elite-C-holder@nicenano`](https://github.com/olidacombe/Elite-C-holder/tree/nicenano) + [`victorlucachi/charybdis-pmw3610-breakout@nicenano`](https://github.com/victorlucachi/charybdis-pmw3610-breakout/tree/nicenano)), que reroteiam os sinais SPI pra `D1/D2/D3` do nice!nano. Este guia adapta pro hardware **stock + módulo chinês**, usando `D15/D16` do header padrão + 3 jumpers diretos.

---

## Resumo do problema

A `Bastardkb Elite-C Holder 2.1 stock` foi desenhada pro Elite-C (ATmega32U4), que tem mais pinos GPIO que o nice!nano. Resultado:

1. **CS** do header `J8` (silk `CS`) roteia pro pad `F0` do Elite-C, que **não existe** no nice!nano. Sensor nunca é selecionado.
2. O header oferece **MOSI e MISO separados** (4-wire SPI), mas o PMW3610 é **3-wire** (SDIO único bidirecional). MISO fica sem usar.
3. Pino `5V` do header é VBUS direto (5V quando USB conectado). Pad `VDDIO` do PMW3610 só aceita **1.7–3.3V** — conectar 5V queima o chip.
4. Sensor não tem pino `IRQ` exposto pelo header da holder. Pra modo IRQ (mais eficiente que polled), precisa jumper direto.

Solução: usar **3 dos 6 pads do header** (`MOSI`, `SCLK`, `GND`) + **3 jumpers diretos** (VDDIO+VDD, NCS, MOT).

---

## Parte 1 — Hardware

### Material necessário

- 1 sensor `PMW3610-Module 20240425` (módulo redondo 32mm, com regulador 2.0V LDO onboard)
- 3 fios finos isolados (AWG 30 ou similar), ~5–8 cm cada
- 6 fios pro header (~10 cm cada)
- Ferro de solda + estanho
- Multímetro (continuidade)
- Pulseira ESD (recomendado — nRF52840 é sensível)

### Pinout do sensor (PMW3610-Module 20240425)

```
       ┌────────────────────────┐
       │      PMW3610-Module    │
       │       20240425         │
       │                        │
       │  ┌──┐         ┌──┬──┐  │
SDIO ──┤  │  │         │V │  │  ├── GND
SCLK ──┤  │  │         │D │  │  │
 NCS ──┤  │  │         │D │  │  │
NRESET─┤  │  │         │IO│  │  │
 MOT ──┤  │  │         ├──┼──┤  ├── GND
       │  └──┘         │V │  │  │
       │               │D │  │  │
       │               │D │  │  │
       │               └──┴──┘  │
       └────────────────────────┘
                Lente
```

**Operating conditions (datasheet do vendedor):**

| Symbol | Min | Typical | Max | Função |
|---|---|---|---|---|
| VDD | 1.7V | 2V | **6.0V** | Power do core (passa pelo LDO 2.0V onboard) |
| VDDIO | 1.7V | 2V | **3.3V** | Power dos pinos I/O (lógica SPI) |

### Pinout do header `J8` da holder (lido do schematic KiCad oficial)

```
 J8 (lado direito da holder, header 1×6)
 ┌──────┐
 │ 5V   │ ← VBUS (não usar com PMW3610)
 │ CS   │ ← vai pro F0 (não existe no nice!nano)
 │ MOSI │ ← P0.10 (silk D16 do Pro Micro)
 │ SCLK │ ← P1.13 (silk D15)
 │ MISO │ ← P1.11 (silk D14) — não usar (3-wire)
 │ GND  │ ← GND
 └──────┘
```

### Onde soldar cada fio

| # | Pad do sensor | Conecta em | Caminho | nRF52840 GPIO destino |
|---|---|---|---|---|
| 1 | **GND** | `GND` do header J8 | fio normal | — |
| 2 | **SDIO** | `MOSI` do header J8 | fio normal | P0.10 |
| 3 | **SCLK** | `SCLK` do header J8 | fio normal | P1.13 |
| 4 | **VDDIO** | pad `VCC` do nice!nano (3.3V) | **jumper direto** ⚠️ | — (3.3V regulado) |
| 5 | **VDD** | pad `VCC` do nice!nano (no mesmo fio do VDDIO) | jumper direto | — (3.3V regulado) |
| 6 | **NCS** | pad `D3` (silk `3`/`SCL`/`020`) do nice!nano | **jumper direto** | P0.20 |
| 7 | **MOT** | pad `D0` (silk `0`/`RX1`/`006`) do nice!nano | **jumper direto** | P0.06 |
| 8 | **NRESET** | — | **não conectar** (sensor tem reset interno) | — |

> **Crítico:** VDDIO e VDD são pads SEPARADOS do sensor — não fazer solder bridge entre eles. Soldar 2 fios separados no mesmo pad `VCC` do nice!nano (ou um Y de fios).

### Localização dos pads no nice!nano

#### nice!nano original (silk Pro Micro: `0`, `1`, `2`, `3`, `4`, `5`...)

```
                    USB-C
                  ┌─────────┐
              B-  │ ●     ● │  B+
       D1/TX0 ►1  │ ●     ● │  RAW
       D0/RX1 ►0  │ ●     ● │  GND        ◄── (D0 = MOT)
              GND │ ●     ● │  RST
              GND │ ●     ● │  VCC        ◄── (VCC = VDDIO+VDD)
        D2/SDA►2  │ ●     ● │  21
        D3/SCL►3  │ ●     ● │  20         ◄── (D3 = NCS)
                 ...
```

#### Clone SuperMini nRF52840 (silk com GPIO numbers diretos: `006`, `008`, `017`, `020`...)

```
                    USB-C
                  ┌─────────┐
              B-  │ ●     ● │  B+
              008 │ ●     ● │  RAW
            ►006  │ ●     ● │  GND        ◄── 006 = nice!nano D0 = MOT
              GND │ ●     ● │  RST
              GND │ ●     ● │  VCC        ◄── VCC = VDDIO+VDD (3.3V)
              017 │ ●     ● │  031
            ►020  │ ●     ● │  029        ◄── 020 = nice!nano D3 = NCS
                 ...
```

**Equivalência clone ↔ nice!nano:**
| Silk clone | nice!nano silk | nRF52840 GPIO |
|---|---|---|
| `006` | `0` / RX | P0.06 |
| `008` | `1` / TX | P0.08 |
| `017` | `2` / SDA | P0.17 |
| `020` | `3` / SCL | P0.20 |
| `010` | `16` / MOSI | P0.10 |
| `113` | `15` / SCK | P1.13 |
| `111` | `14` / MISO | P1.11 |

### Procedimento de soldagem

1. Desconecta a half do USB e desconecta a bateria (JST).
2. Remove ou cobre a lente do PMW3610 com Kapton antes de soldar (proteção contra fluxo/sujeira).
3. Solda os 6 fios no sensor primeiro, deixando ~7cm sobrando.
4. Solda no header `J8` da holder: `GND`, `MOSI`, `SCLK` (3 fios). Os outros 3 pinos do header (`5V`, `CS`, `MISO`) ficam intactos.
5. Solda os 3 jumpers diretos no nice!nano: VDDIO+VDD no mesmo pad `VCC`, NCS no `D3` (`020`), MOT no `D0` (`006`).
6. **Verifica com multímetro antes de energizar:**
   - Continuidade: pad `SDIO` do sensor → pad `MOSI` do header → pad `010` do nice!nano
   - Continuidade: pad `SCLK` do sensor → pad `SCLK` do header → pad `113` do nice!nano
   - Continuidade: pad `NCS` do sensor → pad `020` do nice!nano (NÃO o `CS` do header)
   - Continuidade: pad `MOT` do sensor → pad `006` do nice!nano
   - Continuidade: pads `VDDIO` e `VDD` do sensor → pad `VCC` do nice!nano (deve medir ~3.3V quando USB conectado)
   - SEM continuidade: qualquer fio → GND ou VCC (curto)
   - SEM continuidade: pad `VDDIO` do sensor → pino `5V` do header (confirma que jumper não pegou em pad errado)

---

## Parte 2 — Firmware

### 2.1. Pinctrl em `boards/shields/charybdis_trackball/charybdis_pmw3610.dtsi`

Trocar os pinos SPI pra bater com o roteamento da holder stock:

```diff
 spi0_default: spi0_default {
     group1 {
-        psels = <NRF_PSEL(SPIM_SCK, 0, 8)>,
-            <NRF_PSEL(SPIM_MOSI, 0, 17)>,
-            <NRF_PSEL(SPIM_MISO, 0, 17)>;
+        psels = <NRF_PSEL(SPIM_SCK, 1, 13)>,    /* D15 silk → P1.13 (header SCLK) */
+            <NRF_PSEL(SPIM_MOSI, 0, 10)>,        /* D16 silk → P0.10 (header MOSI = SDIO) */
+            <NRF_PSEL(SPIM_MISO, 0, 10)>;        /* mesmo pino — sensor é 3-wire */
     };
 };
```

(`spi0_sleep` idem.)

`cs-gpios = <&gpio0 20 GPIO_ACTIVE_LOW>` (P0.20 = D3) e `irq-gpios = <&gpio0 6 ...>` (P0.06 = D0) já estão corretos — batem com os jumpers.

### 2.2. Reativar trackball no `charybdis_right_dongle.conf`

Se as configs estiverem como TEMP (desabilitadas pra diagnóstico), restaurar:

```diff
-CONFIG_PMW3610_ALT=n
+CONFIG_PMW3610_ALT=y
...
-# CONFIG_PMW3610_ALT_SMART_ALGORITHM=y
+CONFIG_PMW3610_ALT_SMART_ALGORITHM=y
...
-# CONFIG_PMW3610_ALT_REPORT_INTERVAL_MIN=12
+CONFIG_PMW3610_ALT_REPORT_INTERVAL_MIN=12
... (idem pros REST/RUN_DOWNSHIFT)
```

### 2.3. Reativar nodes no `charybdis_right_dongle.overlay`

```diff
 &trackball {
-  status = "disabled";
+  status = "okay";
 };

 &trackball_split {
-  status = "disabled";
+  device = <&trackball>;
+  status = "okay";
 };
```

---

## Parte 3 — Build

```bash
cd local-build && docker-compose run --rm builder
```

Pra acelerar só o right_dongle, comentar temporariamente os outros em `build.yaml`.

> **Atenção (bug-010, 2026-05-16):** se o build falhar com `error: Your local changes to the following files would be overwritten by checkout` em algum módulo west, é mode-bit drift do `chmod -R 777` em build anterior. Antes de rebuildar:
>
> ```bash
> for m in zmk zephyr modules zmk-pmw3610-driver prospector-zmk-module; do
>   git -C "$m" -c safe.directory=* checkout .
> done
> ```

---

## Parte 4 — Flash e teste

1. Settings reset primeiro (limpa bond residual): flash `firmwares/settings_reset.uf2` na half direita.
2. Flash `firmwares/.../charybdis_right_dongle.uf2` na half direita.
3. Liga half + dongle, abre Notepad, **testa as 21 teclas direitas** primeiro (confirma matrix OK e pareamento OK).
4. **Move a esfera** — cursor deve responder. Se não:
   - Driver crashea em loop e nice!nano entra em DFU automático (single-tap reset monta drive `NICENANO`)? → ver Troubleshooting abaixo.
   - Cursor inverte X/Y ou troca eixos? → editar `swap-xy`, `invert-x`, `invert-y` no dtsi.

### Troubleshooting

| Sintoma | Causa provável | Ação |
|---|---|---|
| Half boota mas single-tap reset monta `NICENANO` | Driver PMW3610 falhou init e crashou; bootloader Adafruit detectou loop e ficou em DFU automático | SPI sem comunicação. Multímetro: continuidade SS sensor → P0.20; SCLK sensor → P1.13; SDIO sensor → P0.10. Conferir VDDIO em 3.3V. |
| Half pareia, teclas funcionam, trackball não responde | Init OK mas cursor não move | Verificar IRQ MOT no P0.06. Se polled mode for desejado, omitir `irq-gpios` no dtsi. |
| Cursor anda mas trêmulo / pula | Frequência SPI alta demais ou ruído | Reduzir `spi-max-frequency` pra 1000000 no dtsi. |
| Cursor inverte ou troca eixos | Orientação do sensor no holder | Toggle `swap-xy` / `invert-x` / `invert-y` no dtsi. |

---

## Apêndice — Por que NÃO usar o `5V` do header pra alimentar o VDD do sensor

Tecnicamente o PMW3610-Module aceita VDD até 6.0V (LDO 2.0V onboard reduz). Então o pino `5V` do header J8 (que vem do VBUS / RAW) poderia alimentar o VDD do sensor sem queimar.

Mas:
1. VDDIO **continua precisando ser 3.3V máx** — já precisa de jumper.
2. Quando estiver em bateria (sem USB), VBUS = 0V → sensor desliga.
3. LDO chinês de qualidade variável; mais um ponto de falha potencial.

Solução mais simples e segura: amarrar VDD e VDDIO no mesmo fio que vai pra `VCC` do nice!nano (3.3V regulado, sempre presente em USB ou bateria). LDO onboard fica ocioso.

---

## Apêndice — Histórico de pinout neste repo

| Versão `charybdis_pmw3610.dtsi` | SCK | SDIO | NCS | IRQ | Pra qual hardware |
|---|---|---|---|---|---|
| Original (até 2026-05-17) | P0.08 (D1) | P0.17 (D2) | P0.20 (D3) | P0.06 (D0) | Forks `olidacombe` holder + `victorlucachi` breakout |
| Atual (2026-05-17+) | **P1.13 (D15)** | **P0.10 (D16)** | P0.20 (D3) | P0.06 (D0) | Bastardkb Elite-C Holder 2.1 **stock** + PMW3610-Module chinês |

Se você usar os PCBs forkados, reverta o pinctrl pro original (git history).
