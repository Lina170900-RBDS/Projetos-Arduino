# Projeto 01 - Pisca LED

Este é o projeto mais clássico de introdução ao *Arduino*: fazer um LED piscar em intervalos regulares.  
O objetivo é entender como configurar uma saída digital e controlar sinais *HIGH* (5V) e *LOW* (0V).

---

## 🔧 Materiais necessários
- 1 placa Arduino (UNO, Nano ou similar)  
- 1 LED vermelho  
- 1 resistor de 200Ω (ou próximo)  
- 1 protoboard  
- Jumpers (fios de conexão)  
- Cabo USB para upload do código  

---

## ⚡ Circuito
- O LED é conectado ao *pino digital 13* do Arduino, em série com o resistor de 200Ω.  
- O resistor limita a corrente, protegendo o LED.  
- O GND do Arduino deve estar conectado ao negativo do LED.  


---

## 📝 Código (Sketch)

```cpp
// Pisca LED - Blink
// Liga e desliga o LED do pino 13 em intervalos de 1 segundo

void setup() {
  pinMode(13, OUTPUT);   // Define o pino 13 como saída
}

void loop() {
  digitalWrite(13, HIGH);  // Acende o LED
  delay(1000);             // Espera 1 segundo
  digitalWrite(13, LOW);   // Apaga o LED
  delay(1000);             // Espera 1 segundo
}
