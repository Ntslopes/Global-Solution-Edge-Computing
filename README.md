
# ☀️ Sistema de Monitoramento de Painel Solar com Arduino

<div align="center">

![Arduino](https://img.shields.io/badge/Arduino-00979D?style=for-the-badge&logo=arduino&logoColor=white)
![C++](https://img.shields.io/badge/C%2B%2B-00599C?style=for-the-badge&logo=c%2B%2B&logoColor=white)
![License](https://img.shields.io/badge/License-MIT-green?style=for-the-badge)
![Status](https://img.shields.io/badge/Status-Funcional-brightgreen?style=for-the-badge)

> 🔋 Projeto embarcado para monitoramento inteligente de temperatura e luminosidade em painéis solares, com alertas visuais, sonoros e exibição em display LCD I2C.

</div>

---

## 📋 Índice

- [Sobre o Projeto](#-sobre-o-projeto)
- [Funcionalidades](#-funcionalidades)
- [Hardware Necessário](#-hardware-necessário)
- [Pinagem](#-pinagem)
- [Lógica de Funcionamento](#-lógica-de-funcionamento)
- [Display LCD — Estados Possíveis](#-display-lcd--estados-possíveis)
- [Como Usar](#-como-usar)
- [Dependências](#-dependências)
- [Participantes](#-participantes)

---

## 🧠 Sobre o Projeto

Este projeto simula um sistema de controle e monitoramento para painéis solares fotovoltaicos utilizando um **Arduino**. Ele lê dados de um **sensor de luminosidade** (simulando o painel solar) e de um **sensor de temperatura (LM35)**, tomando decisões automáticas sobre o estado do sistema e comunicando ao usuário por meio de:

- 💡 **LEDs coloridos** (verde, amarelo e vermelho)
- 🔔 **Buzzer de alerta**
- 📺 **Display LCD I2C 16x2**

---

## ✅ Funcionalidades

| Funcionalidade | Descrição |
|---|---|
| 🌡️ Leitura de temperatura | Via sensor analógico LM35 (pino A2) |
| ☀️ Leitura de luminosidade | Simulando saída do painel solar (pino A1) |
| 🟢 LED Verde | Temperatura normal (≤ 27°C) |
| 🟡 LED Amarelo | Temperatura elevada (27°C < T < 32°C) |
| 🔴 LED Vermelho + Buzzer | Temperatura crítica (> 32°C) — painel desligado |
| 💡 LED Painel Solar | Liga quando luminosidade > 50% e temperatura < 85°C |
| 📺 LCD I2C | Exibe status em tempo real |

---

## 🔧 Hardware Necessário

- 1x Arduino Uno (ou compatível)
- 1x Display LCD I2C 16x2 (endereço `0x27`)
- 1x Sensor de temperatura **LM35** (ou potenciômetro simulando)
- 1x Sensor de luminosidade / LDR (ou potenciômetro simulando)
- 1x Buzzer ativo
- 1x LED Vermelho
- 1x LED Amarelo
- 1x LED Verde
- 1x LED Azul/Branco (painel solar)
- Resistores (220Ω para cada LED)
- Protoboard e jumpers

---

## 🔌 Pinagem

```
Arduino          Componente
─────────────────────────────────────
A1           →   Sensor Painel Solar (luminosidade)
A2           →   Sensor de Temperatura (LM35)
D6           →   LED Verde
D7           →   Buzzer
D8           →   LED Vermelho
D9           →   LED Amarelo
D10          →   LED Painel Solar
SDA (A4)     →   LCD I2C SDA
SCL (A5)     →   LCD I2C SCL
```

---

## ⚙️ Lógica de Funcionamento

### 🌡️ Temperatura (LM35)

A tensão lida no pino analógico é convertida para temperatura com a fórmula:

```
tensão    = leitura × (5.0 / 1023.0)
temperatura = (tensão - 0.5) × 100
```

| Faixa | Estado | LED | Buzzer |
|---|---|---|---|
| T ≤ 27°C | Normal | 🟢 Verde | OFF |
| 27°C < T < 32°C | Elevada | 🟡 Amarelo | OFF |
| T > 32°C | **Crítica** | 🔴 Vermelho | **ON** |

> ⚠️ Com temperatura crítica, o painel solar é **forçadamente desligado**.

### ☀️ Painel Solar

O valor bruto do sensor é mapeado para uma **porcentagem (0–100%)**.

| Condição | Estado do Painel |
|---|---|
| Luminosidade > 50% **e** Temperatura < 85°C | ✅ LIGADO |
| Luminosidade ≤ 50% | ❌ DESLIGADO |
| Temperatura ≥ 85°C | 🚨 CRÍTICO |

---

## 📺 Display LCD — Estados Possíveis

```
┌────────────────┐     ┌────────────────┐     ┌────────────────┐
│  TEMP CRITICA  │     │  TEMP ELEVADA  │     │  TEMP NORMAL   │
│  REFRIGERANDO  │     │    ATENCAO     │     │  RECOMENDADA   │
└────────────────┘     └────────────────┘     └────────────────┘

┌────────────────┐     ┌────────────────┐     ┌────────────────┐
│  PAINEL SOLAR  │     │  PAINEL SOLAR  │     │  PAINEL SOLAR  │
│     LIGADO     │     │   DESLIGADO    │     │    CRITICO     │
└────────────────┘     └────────────────┘     └────────────────┘
```

---

## 🚀 Como Usar

1. **Clone ou baixe** este repositório.
2. Abra o arquivo `.ino` na **Arduino IDE**.
3. Instale a biblioteca `LiquidCrystal_I2C` (via *Library Manager* ou manualmente).
4. Monte o circuito conforme a [pinagem](#-pinagem).
5. Selecione a placa correta (ex: *Arduino Uno*) e a porta COM.
6. Faça o **upload** do código.
7. Abra o **Monitor Serial** se quiser depurar (opcional).

---

## 📦 Dependências

```cpp
#include <LiquidCrystal_I2C.h>
```

- **LiquidCrystal_I2C** — disponível no Library Manager da Arduino IDE  
  🔗 [https://github.com/johnrickman/LiquidCrystal_I2C](https://github.com/johnrickman/LiquidCrystal_I2C)

---

## 👥 Participantes

<div align="center">

| Nome | RA |
|---|---|
| 👩‍💻 Esther dos Santos de Almeida Tozzo | `570860` |
| 👨‍💻 Felipe de Oliveira Zimmermann | `570863` |
| 👩‍💻 Izabela Pordeus de Almeida | `570316` |
| 👨‍💻 João Victor Santos Souza | `569949` |
| 👨‍💻 Leonardo Henrique Basseti | `574039` |
| 👨‍💻 Matheus Lopes Lima | `571458` |

</div>

---

<div align="center">

Feito com ☀️ e muito ☕ pelo grupo.

</div>
