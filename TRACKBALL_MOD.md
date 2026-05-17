# Trackball Mod — PMW3360 em Bastardkb Elite-C Holder 2.1 (stock) + nice!nano

> **Quando aplicar:** se você tem o conjunto `Bastardkb Elite-C Holder 2.1 stock` + `nice!nano` (ou clone nRF52840 form-factor Elite-C) + sensor `Bastardkb PMW3360 Sensor PCB Rev 2.0`, e o trackball não funciona porque o CS do header SPI da holder vai pra um pino que **não existe** no nice!nano.
>
> **Status do repo:** o config atual (`charybdis_pmw3610.dtsi`) assume a holder forkada `olidacombe/Elite-C-holder@nicenano` + sensor PMW3610. Esse documento descreve como adaptar pra hardware stock + PMW3360.

---

## Resumo do problema

A Bastardkb Elite-C Holder 2.1 stock roteia o pad **CS** do header SPI do trackball para o pino **F0** do footprint Elite-C. **F0 não existe no nice!nano** (e em nenhum nRF52840 em form-factor Pro Micro). Resultado: o sinal CS termina no holder e nunca chega ao MCU. O sensor recebe SCK/MOSI/MISO mas nunca é selecionado, e portanto nunca responde.

```
PMW3360 sensor CS  →  fio branco  →  Holder header "CS"  →  pad F0  →  ❌ vazio (não há pino físico)
```

Solução proposta neste documento: adicionar **um único jumper wire** do pad CS do sensor até um GPIO livre do nice!nano, e ajustar o firmware pra usar esse GPIO + driver de PMW3360.

---

## Parte 1 — Hardware mod

### Material necessário

- 1 fio fino isolado (AWG 30 ou similar), ~5 cm
- Ferro de solda + estanho
- Multímetro (recomendado pra confirmar continuidade depois)

### Onde soldar

**Origem do jumper:** pad **SS** do PMW3360 Sensor PCB Rev 2.0 (Bastardkb).
- Localização: na borda do PCB redondo, é o 5º pad de cima pra baixo na fileira lateral marcada `GND / MISO / SCK / MOSI / SS / 3.3V`.
- Esse pad já tem um fio branco soldado indo pra holder. **Não remova esse fio.** Solde o jumper em paralelo (em cima do mesmo pad ou no fio mesmo).

**Destino do jumper:** pino **D3** (silk Pro Micro) do nice!nano.
- Localização: lado direito do nice!nano (visto com USB-C pra cima), 4º pad de cima pra baixo.
- nRF52840 GPIO correspondente: **P0.20**.
- Ele está exposto no nice!nano (não é um pad exclusivo Elite-C).
- **Verificar antes de soldar:** D3 não pode estar sendo usado pelo matrix da half. Confira no `boards/shields/charybdis_right_dongle/charybdis_right_dongle.overlay`. As `col-gpios`/`row-gpios` listam `pro_micro 19, 20, 10, 6, 7, 8` (cols) e `pro_micro 18, 5, 4, 9` (rows). **D3 não está nessa lista — está livre.**

### Procedimento

1. Desconecta a half do USB.
2. Desliga a bateria (se já estiver montada — desconecta o JST).
3. Estanha as duas pontas do fio.
4. Solda uma ponta no pad **SS** do sensor (em paralelo com o fio existente).
5. Passa o fio por baixo da half (ou pelo melhor caminho mecânico que não atrapalhe a esfera).
6. Solda a outra ponta no pad **D3** do nice!nano.
7. Verifica com multímetro: continuidade entre pad SS do sensor e pad D3 do nice!nano. Sem continuidade entre o fio jumper e GND/3.3V (curto).

### Consideração: por que não trocar pelo olidacombe fork?

Trocar pra `olidacombe/Elite-C-holder@nicenano` evitaria o jumper, mas exige:
- Encomendar PCB nova (fab + frete)
- Dessoldar o nice!nano da holder atual
- Ressoldar na holder nova
- Reconectar todos os fios da matrix, sensor, OLED etc

Pra resolver UM pino faltando, jumper é dramaticamente mais rápido e tem mesmo resultado funcional.

---

## Parte 2 — Firmware changes

### 2.1. `config/west.yml` — trocar driver

Substituir `zmk-pmw3610-driver` pelo `george-norton/zmk-driver-pmw3360`:

```yaml
manifest:
  remotes:
    - name: zmkfirmware
      url-base: https://github.com/zmkfirmware
    - name: 280Zo
      url-base: https://github.com/280Zo
    - name: george-norton
      url-base: https://github.com/george-norton

  projects:
    - name: zmk
      remote: zmkfirmware
      revision: main
      import: app/west.yml
    - name: zmk-driver-pmw3360       # ← novo
      remote: george-norton
      revision: main
    # - name: zmk-pmw3610-driver     # ← remover/comentar
    #   remote: 280Zo
    #   revision: main
    - name: prospector-zmk-module
      remote: 280Zo
      revision: main

  self:
    path: config
```

### 2.2. Criar `boards/shields/charybdis_trackball/charybdis_pmw3360.dtsi`

Arquivo novo, derivado do `charybdis_pmw3610.dtsi` com:
- 4-wire SPI (MOSI e MISO em pinos separados)
- `compatible = "pixart,pmw3360"`
- Sem `irq-gpios` (Bastardkb sensor PCB Rev 2.0 não expõe MOTION; modo polled)
- Pinout que casa com o caminho real dos fios

```dts
&pinctrl {
    spi0_default: spi0_default {
        group1 {
            psels = <NRF_PSEL(SPIM_SCK, 1, 13)>,    /* D15 silk → P1.13 */
                <NRF_PSEL(SPIM_MOSI, 0, 10)>,       /* D16 silk → P0.10 */
                <NRF_PSEL(SPIM_MISO, 1, 11)>;       /* D14 silk → P1.11 */
        };
    };

    spi0_sleep: spi0_sleep {
        group1 {
            psels = <NRF_PSEL(SPIM_SCK, 1, 13)>,
                <NRF_PSEL(SPIM_MOSI, 0, 10)>,
                <NRF_PSEL(SPIM_MISO, 1, 11)>;
            low-power-enable;
        };
    };
};

#include <zephyr/dt-bindings/input/input-event-codes.h>

&spi0 {
    status = "okay";
    compatible = "nordic,nrf-spim";
    pinctrl-0 = <&spi0_default>;
    pinctrl-1 = <&spi0_sleep>;
    pinctrl-names = "default", "sleep";
    cs-gpios = <&gpio0 20 GPIO_ACTIVE_LOW>;          /* D3 silk → P0.20 (jumper wire) */

    trackball: trackball@0 {
        status = "okay";
        compatible = "pixart,pmw3360";
        reg = <0>;
        spi-max-frequency = <2000000>;
        /* irq-gpios deliberately omitted — sensor PCB Rev 2.0 doesn't expose MOTION,
           george-norton driver falls back to polled mode automatically. */

        cpi = <800>;
        evt-type = <INPUT_EV_REL>;
        x-input-code = <INPUT_REL_X>;
        y-input-code = <INPUT_REL_Y>;

        /* Confirmar empiricamente; ajustar se cursor invertido */
        /* swap-xy; */
        /* invert-x; */
        /* invert-y; */
    };
};

/ {
    split_inputs {
        #address-cells = <1>;
        #size-cells = <0>;

        trackball_split: trackball_split@0 {
            compatible = "zmk,input-split";
            reg = <0>;
        };
    };

    trackball_listener: trackball_listener {
        compatible = "zmk,input-listener";
        status = "disabled"; // overridden on central
        device = <&trackball_split>;
    };
};
```

**Observações sobre os pinos SPI:**

| Função | Pino físico | nice!nano GPIO | Justificativa |
|---|---|---|---|
| SCK | D15 (Pro Micro silk) | P1.13 | Já é onde o header SPI da holder roteia. Não precisa mudar fiação. |
| MOSI | D16 | P0.10 | Idem. |
| MISO | D14 | P1.11 | Idem. |
| CS | D3 (jumper) | P0.20 | **Adicionado pelo jumper.** Não usa o roteamento da holder. |

### 2.3. Atualizar `boards/shields/charybdis_right_dongle/charybdis_right_dongle.overlay`

Trocar a linha do include:

```diff
 #include "../charybdis_common/charybdis.dtsi"
-#include "../charybdis_trackball/charybdis_pmw3610.dtsi"
+#include "../charybdis_trackball/charybdis_pmw3360.dtsi"
 #include "../../config/trackball/charybdis_pointer.dtsi"
```

(Faça o mesmo em `charybdis_right_bt/charybdis_right_bt.overlay` se for usar o build BT puro um dia.)

### 2.4. Reescrever `boards/shields/charybdis_right_dongle/charybdis_right_dongle.conf`

Trocar todas as configs PMW3610_ALT_* pelas equivalentes do george-norton driver:

```conf
CONFIG_ZMK_USB=n  # ZMK_USB só em central; right é peripheral

## PMW3360 Driver (george-norton/zmk-driver-pmw3360)
CONFIG_SPI=y
CONFIG_INPUT=y
CONFIG_ZMK_POINTING=y
CONFIG_INPUT_PIXART_PMW3360=y

## Threading: usa work queue dedicado (recomendado em ZMK)
CONFIG_INPUT_PIXART_PMW3360_USE_OWN_THREAD=y
CONFIG_INPUT_PIXART_PMW3360_THREAD_STACK_SIZE=1024
CONFIG_INPUT_PIXART_PMW3360_THREAD_PRIORITY=10

## Debug — só ligar se trackball não funcionar
# CONFIG_INPUT_PIXART_PMW3360_LOG_LEVEL_DBG=y
# CONFIG_SPI_LOG_LEVEL_DBG=y
```

> **Atenção:** os nomes exatos das opções de Kconfig (`CONFIG_INPUT_PIXART_PMW3360_*`) precisam ser confirmados lendo o Kconfig do `george-norton/zmk-driver-pmw3360`. Pode ser que sejam apenas `CONFIG_PMW3360=y` e variantes — leia o Kconfig do módulo antes de finalizar.

### 2.5. Considerar limpeza opcional

- O arquivo `boards/shields/charybdis_trackball/charybdis_pmw3610.dtsi` pode ficar no repo (não custa nada e serve de referência se um dia voltar pro PMW3610). Ou remover, se preferir.
- O fork `280Zo/zmk-pmw3610-driver` pode sair do `west.yml` (já comentado no diff acima).

---

## Parte 3 — Build

```bash
cd local-build
docker-compose run --rm builder
```

Espera ~10 minutos. Saída esperada:
- 4 firmwares como antes
- `firmwares/dongle_standard_xiao/qwerty/charybdis_right_dongle.uf2` agora compilado com driver PMW3360

Se der erro de compilação, provavelmente é nome de Kconfig do george-norton driver diferente do que está no `.conf`. Lê o erro, ajusta, rebuilda.

---

## Parte 4 — Flash e teste

1. **Flash da half direita:**
   - USB → double-tap reset → monta `NICENANO`
   - Arrasta `firmwares/dongle_standard_xiao/qwerty/charybdis_right_dongle.uf2`
2. **Power on:** USB ou bateria
3. **Pareamento:** dongle (já flashado) deve achar a half em ~10 s
4. **Teste de teclas:** abre Notepad, pressiona algumas teclas do lado direito → devem aparecer
5. **Teste de trackball:** mexe a esfera → cursor deve se mover
6. **Direção:** se o cursor andar invertido em X/Y ou trocar eixos:
   - Edita `charybdis_pmw3360.dtsi` descomentando `swap-xy`, `invert-x`, `invert-y` conforme necessário
   - Rebuilda + reflasha
7. **Sensibilidade:** ajustar `cpi = <800>` (range típico: 400-3600)

---

## Parte 5 — Como reverter

Se quiser voltar pro PMW3610 (pra usar o sensor antigo, ou se trocar pra holder olidacombe):

1. Reverte os 5 arquivos editados acima
2. Remove o jumper wire (dessolda)
3. Rebuilda

Os arquivos originais ainda estão no `git log` se precisar.

---

## Troubleshooting

| Sintoma | Causa provável | Ação |
|---|---|---|
| Half não pareia com dongle | Driver do trackball entrou em loop e está fazendo WDT reset | Tira o jumper temporariamente, verifica se half volta. Se sim, há problema de SPI. |
| Trackball não move, mas teclas funcionam | Driver init falhou silenciosamente. Pinout SPI errado, ou jumper sem continuidade. | Multímetro: testa continuidade SS sensor → P0.20 nice!nano. Confira solda. |
| Cursor inverte/troca eixos | Padrão de orientação do sensor | Edita `swap-xy`/`invert-x`/`invert-y` no dtsi. |
| Cursor anda mas trêmulo / pula | Frequência SPI alta demais ou ruído elétrico | Reduz `spi-max-frequency` pra 1000000. |
| `CONFIG_INPUT_PIXART_PMW3360 not found` no build | Kconfig do driver tem nome diferente | Lê o `Kconfig` do `zmk-driver-pmw3360` e usa o nome correto. |

---

## Apêndice A — Pinout completo do nice!nano nesta build

Pinos usados pelo matrix da half direita (`charybdis_right_dongle.overlay`):

| Função | Pro Micro silk | nRF52840 GPIO |
|---|---|---|
| col 0 | D-mais-alto (varia) | varia |
| ...   | ... | ... |

(Ver `charybdis_right_dongle.overlay:18-32` pra lista completa.)

Pinos do trackball (este mod):

| Função | Pro Micro silk | nRF52840 GPIO | Conexão física |
|---|---|---|---|
| SCK | D15 | P1.13 | Header SPI da holder |
| MOSI | D16 | P0.10 | Header SPI da holder |
| MISO | D14 | P1.11 | Header SPI da holder |
| CS | D3 | P0.20 | **Jumper wire** (sensor SS → nice!nano D3) |
| GND | GND | — | Header SPI da holder |
| 3.3V | VCC | — | Header SPI da holder (ou 3.3V do nice!nano) |

---

## Apêndice B — Por que polled mode é OK aqui

O PMW3360 tem um pino MOTION (active low quando há movimento detectado), mas a Bastardkb Sensor PCB Rev 2.0 **não expõe** esse pino — só os 6 padrões SPI. Sem MOTION, o driver tem que polar o sensor periodicamente em vez de esperar interrupção.

Custos:
- ~5-10 mA extra de consumo médio (significativo, mas suportável com bateria 1100 mAh+)
- Latência ligeiramente maior (depende do polling rate, default ~125 Hz)

Se um dia esse custo virar problema, dá pra:
1. Fazer um segundo jumper wire do pad MOTION do IC PMW3360 (pino físico do chip, não exposto na PCB Rev 2.0) até um GPIO do nice!nano. Hard mod, requer microscópio + estanho de precisão.
2. Trocar pra Bastardkb PMW3360 Sensor PCB Rev 3+ se um dia lançarem com MOTION exposto.
