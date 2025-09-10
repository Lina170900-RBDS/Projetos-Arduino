📂 03-controle-de-oito-LEDs

🎯 Objetivo

Este projeto consiste em criar sequências rítmicas de controle de LEDs utilizando a plataforma Arduino UNO.
O objetivo é exercitar o uso de saídas digitais, loops, matrizes de pinos e variações de lógica para acender e apagar LEDs de diferentes formas.


---

🔧 Materiais utilizados

1 × Plataforma Arduino UNO

4 × LEDs vermelhos

4 × LEDs amarelos

8 × Resistores de 330 Ω

1 × Matriz de contatos (protoboard)

Jumpers para conexões



---

⚡ Esquema de montagem

Cada LED é conectado a uma porta digital do Arduino (pinos 2 a 9), cada um com seu resistor de 330 Ω em série.
As diferentes lógicas de controle estão implementadas nos sketches abaixo.


---

💻 Sketches disponíveis

🔹 Sketch 1 – Sequência simples acendendo LEDs

int ledPins[] = {2,3,4,5,6,7,8,9};
int index;

void setup() {
  for(index = 0; index <= 7; index++) {
    pinMode(ledPins[index], OUTPUT);
  }
}

void loop() {
  oneAfterAnotherNoLoop();
}

void oneAfterAnotherNoLoop() {
  int delayTime = 100;

  digitalWrite(ledPins[0], HIGH); delay(delayTime);
  digitalWrite(ledPins[1], HIGH); delay(delayTime);
  digitalWrite(ledPins[2], HIGH); delay(delayTime);
  digitalWrite(ledPins[3], HIGH); delay(delayTime);
  digitalWrite(ledPins[4], HIGH); delay(delayTime);
  digitalWrite(ledPins[5], HIGH); delay(delayTime);
  digitalWrite(ledPins[6], HIGH); delay(delayTime);
  digitalWrite(ledPins[7], HIGH); delay(delayTime);

  // Agora apaga na ordem inversa
  digitalWrite(ledPins[7], LOW); delay(delayTime);
  digitalWrite(ledPins[6], LOW); delay(delayTime);
  digitalWrite(ledPins[5], LOW); delay(delayTime);
  digitalWrite(ledPins[4], LOW); delay(delayTime);
  digitalWrite(ledPins[3], LOW); delay(delayTime);
  digitalWrite(ledPins[2], LOW); delay(delayTime);
  digitalWrite(ledPins[1], LOW); delay(delayTime);
  digitalWrite(ledPins[0], LOW); delay(delayTime);
}


---

🔹 Sketch 2 – Loop sequencial

int ledPins[] = {2,3,4,5,6,7,8,9};
int index;
int delayTime = 100;

void setup() {
  for(index = 0; index <= 7; index++) {
    pinMode(ledPins[index], OUTPUT);
  }
}

void loop() {
  oneAfterAnotherLoop();
}

void oneAfterAnotherLoop() {
  for(index = 0; index <= 7; index++) {
    digitalWrite(ledPins[index], HIGH);
    delay(delayTime);
  }

  for(index = 7; index >= 0; index--) {
    digitalWrite(ledPins[index], LOW);
    delay(delayTime);
  }
}


---

🔹 Sketch 3 – Acendendo um por vez

int ledPins[] = {2,3,4,5,6,7,8,9};
int index;
int delayTime = 100;

void setup() {
  for(index = 0; index <= 7; index++) {
    pinMode(ledPins[index], OUTPUT);
  }
}

void loop() {
  oneOnAtATime();
}

void oneOnAtATime() {
  for(index = 0; index <= 7; index++) {
    digitalWrite(ledPins[index], HIGH);
    delay(delayTime);
    digitalWrite(ledPins[index], LOW);
  }
}


---

🔹 Sketch 4 – Ping Pong

int ledPins[] = {2,3,4,5,6,7,8,9};
int index;
int delayTime = 100;

void setup() {
  for(index = 0; index <= 7; index++) {
    pinMode(ledPins[index], OUTPUT);
  }
}

void loop() {
  pingPong();
}

void pingPong() {
  for(index = 0; index <= 7; index++) {
    digitalWrite(ledPins[index], HIGH);
    delay(delayTime);
    digitalWrite(ledPins[index], LOW);
  }

  for(index = 7; index >= 0; index--) {
    digitalWrite(ledPins[index], HIGH);
    delay(delayTime);
    digitalWrite(ledPins[index], LOW);
  }
}


---

🔹 Sketch 5 – Marquee (vermelho e amarelo intercalados)

int ledPins[] = {2,3,4,5,6,7,8,9};
int index;
int delayTime = 200;

void setup() {
  for(index = 0; index <= 7; index++) {
    pinMode(ledPins[index], OUTPUT);
  }
}

void loop() {
  marquee();
}

void marquee() {
  for(index = 0; index <= 3; index++) {
    digitalWrite(ledPins[index], HIGH);    // Liga LEDs amarelos
    digitalWrite(ledPins[index+4], HIGH);  // Liga LEDs vermelhos
  }
  delay(delayTime);

  for(index = 0; index <= 3; index++) {
    digitalWrite(ledPins[index], LOW);
    digitalWrite(ledPins[index+4], LOW);
  }
  delay(delayTime);
}


---

🔹 Sketch 6 – LEDs aleatórios

int ledPins[] = {2,3,4,5,6,7,8,9};
int index;
int delayTime = 100;

void setup() {
  for(index = 0; index <= 7; index++) {
    pinMode(ledPins[index], OUTPUT);
  }
}

void loop() {
  randomLED();
}

void randomLED() {
  index = random(0, 8);  // escolhe LED aleatório
  digitalWrite(ledPins[index], HIGH);
  delay(delayTime);
  digitalWrite(ledPins[index], LOW);
}


---

📌 Observações

Todos os sketches foram escritos para o Arduino UNO.

As portas utilizadas vão do pino 2 ao 9.

O delay pode ser ajustado para aumentar/diminuir a velocidade das sequências.

É possível expandir para mais LEDs ou alterar padrões de piscada.
