📂 02-controle-luminosidade/README.md

# Job 2 – Controle de Luminosidade de um LED

## 🎯 Objetivo
Utilizar um potenciômetro para controlar a intensidade luminosa de um LED conectado à plataforma Arduino.

## 🧩 Materiais Utilizados
- 1 × Placa Arduino UNO  
- 1 × Potenciômetro (Trimpot 10kΩ)  
- 1 × Resistor de 330Ω  
- 1 × LED amarelo  
- 1 × Protoboard (matriz de contatos)  
- Jumpers (fios de conexão)

## ⚡ Montagem do Circuito
O potenciômetro é conectado ao pino analógico A0 do Arduino. O LED é conectado ao pino digital 13, em série com o resistor de 330Ω.

## 💻 Código (Sketch)

```cpp
int sensorPin = 0;     // Pino analógico A0 conectado ao potenciômetro
int ledPin = 13;       // LED conectado ao pino digital 13
int sensorValue;       // Variável para armazenar a leitura

void setup() {
  pinMode(ledPin, OUTPUT);  // Configura pino 13 como saída
}

void loop() {
  sensorValue = analogRead(sensorPin);  // Lê valor do potenciômetro
  digitalWrite(ledPin, HIGH);           // Liga LED
  delay(sensorValue);                   // Mantém ligado proporcionalmente
  digitalWrite(ledPin, LOW);            // Desliga LED
  delay(sensorValue);                   // Mantém desligado proporcionalmente
}

🔎 Observações

O valor lido no pino analógico A0 varia entre 0 e 1023, correspondendo a 0V até 5V.

Quanto menor o valor lido, mais rápido o LED pisca.

Quanto maior o valor lido, mais lento o LED pisca.


---
