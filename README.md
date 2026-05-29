# ☀️ SolarShield — Simulador de Proteção Contra Tempestades Solares

> **Protótipo Arduino de monitoramento térmico e energético inspirado na proteção de data centers contra anomalias solares**

---

## 🌌 Contexto do Projeto

Tempestades solares (ejeções de massa coronal) podem induzir **correntes parasitas na rede elétrica**, causando superaquecimento de equipamentos, danos a transformadores e UPS, e até blecautes em data centers — gerando prejuízos de milhões de dólares por hora.

Este projeto simula, em escala reduzida com Arduino, o comportamento de um sistema de monitoramento e resposta automática a esse tipo de evento:

- 🌡️ O **sensor de temperatura** representa o aquecimento anômalo que uma tempestade solar pode causar na infraestrutura
- ☀️ O **painel solar (LDR)** representa a disponibilidade de energia renovável no momento do evento
- 💡 Os **LEDs e buzzer** representam os alertas automáticos acionados pelo sistema
- 📟 O **display LCD** representa o painel de status do data center em tempo real

---

## 🛠️ Hardware Utilizado

| Componente | Quantidade | Pino Arduino |
|---|---|---|
| Arduino Uno | 1 | — |
| Display LCD 16x2 (I2C) | 1 | SDA/SCL |
| Sensor de temperatura TMP36 | 1 | A2 |
| LDR (fotoresistor) | 1 | A1 |
| LED vermelho | 1 | 8 |
| LED amarelo | 1 | 9 |
| LED verde | 1 | 6 |
| LED azul (painel solar) | 1 | 10 |
| Buzzer | 1 | 7 |
| Resistores 220Ω | 4 | — |

---

## ⚙️ Como Funciona

### 🌡️ Monitoramento de Temperatura (Simulação da Tempestade Solar)

O sensor TMP36 lê a temperatura ambiente e classifica em três estados:

```
temperatura > 32°C   →  🔴 TEMP CRÍTICA   — LED vermelho + buzzer + painel desligado
27°C < temp < 32°C   →  🟡 TEMP ELEVADA   — LED amarelo + atenção
temperatura ≤ 27°C   →  🟢 TEMP NORMAL    — LED verde + operação recomendada
```

> 💡 Simule uma "tempestade solar" aquecendo o sensor com os dedos ou um sopro quente — o sistema responde em tempo real.

### ☀️ Controle do Painel Solar

O painel só entra em operação quando **duas condições são atendidas simultaneamente**:

```
luminosidade > 50%   E   temperatura < 85°C   →   PAINEL LIGADO
caso contrário                                →   PAINEL DESLIGADO / CRÍTICO
```

Isso simula a lógica de um data center que só ativa fontes de energia renovável quando as condições ambientais são seguras.

### 📟 Display LCD — Painel de Status

O LCD exibe o estado atual do sistema em tempo real, alternando entre as mensagens de temperatura e status do painel solar.

---

## 📊 Diagrama de Estados

```
                    ┌─────────────────────────────┐
                    │       LEITURA DOS SENSORES      │
                    │  Temperatura (A2) + LDR (A1)   │
                    └──────────────┬──────────────┘
                                   │
               ┌───────────────────┼───────────────────┐
               ▼                   ▼                   ▼
        temp > 32°C          27 < temp < 32        temp ≤ 27°C
        🔴 CRÍTICA            🟡 ELEVADA             🟢 NORMAL
        LED vermelho          LED amarelo            LED verde
        Buzzer ON             Buzzer OFF             Buzzer OFF
        Painel OFF            —                      —
               │                   │                   │
               └───────────────────┼───────────────────┘
                                   │
                    ┌──────────────▼──────────────┐
                    │    luminosidade > 50%?        │
                    │    temperatura < 85°C?        │
                    └──────────────┬──────────────┘
                          ┌────────┴────────┐
                          ▼                 ▼
                    SIM → PAINEL         NÃO → PAINEL
                        LIGADO              DESLIGADO
```

---

## 🚀 Como Reproduzir

1. **Monte o circuito** conforme a tabela de pinos acima
2. **Instale a biblioteca** `LiquidCrystal_I2C` na Arduino IDE
   - Sketch → Incluir Biblioteca → Gerenciar Bibliotecas → buscar `LiquidCrystal I2C`
3. **Carregue o código** `solarshield.ino` na placa
4. **Abra o Monitor Serial** (opcional) para debug
5. **Teste o sistema:**
   - Cubra o LDR → painel desliga por baixa luminosidade
   - Aqueça o TMP36 → sistema entra em modo crítico com buzzer
   - Ilumine o LDR com luminosidade > 50% e temperatura normal → painel liga

---

## 🔗 Conexão com a Proposta Real

Este protótipo é a prova de conceito física de uma solução maior:

| Protótipo Arduino | Sistema Real |
|---|---|
| Sensor TMP36 | Satélites DSCOVR + SWPC monitorando vento solar |
| LDR | Medidores de disponibilidade de energia renovável |
| LEDs + buzzer | Alertas para operadores + sistemas EPMS/DCIM |
| LCD | Dashboard de monitoramento do data center |
| Lógica de desligar o painel | Desconexão seletiva da rede + migração de workloads de IA |

A ideia central é a mesma: **agir antes do dano, não depois.**

---

## 👥 Equipe

| Nome | RA |
|---|---|
| Esther dos Santos de Almeida Tozzo | 570860 |
| Felipe de Oliveira Zimmermann | 570863 |
| Izabela Pordeus de Almeida | 570316 |
| João Victor Santos Souza | 569949 |
| Matheus Lopes Lima | 571458 |

---

## 📄 Licença

Projeto acadêmico de livre uso para fins educacionais.

---

<div align="center">
  <sub>Feito com ☀️ e muito Arduino</sub>
</div>
