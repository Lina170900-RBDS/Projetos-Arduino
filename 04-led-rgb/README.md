📂 04-led-rgb

🎯 Objetivo

Realizar a composição de cores com um LED RGB (Red-Green-Blue), explorando as cores primárias aditivas (vermelho, verde, azul) e suas combinações para gerar branco, ciano, magenta/roxo e amarelo. Também há um modo que varre o espectro gerando ~768 variações de cor.


---

🔧 Materiais

1 × Arduino UNO

1 × LED RGB (catodo comum ou anodo comum – ver observações)

3 × Resistores 330 Ω (um para cada canal: R, G, B)

1 × Protoboard e jumpers


> Pinos PWM no UNO: use saídas com ~ (3, 5, 6, 9, 10, 11).
Aqui usaremos 9 (R), 10 (G), 11 (B).




---

🔌 Ligações (catodo comum)

Catodo do LED → GND

R (vermelho) → resistor 330 Ω → pino 9

G (verde) → resistor 330 Ω → pino 10

B (azul) → resistor 330 Ω → pino 11


> Se o seu LED for anodo comum, conecte o anodo ao 5 V e inverta a lógica no código (ou use valorPWM = 255 - valorPWM antes do analogWrite).




---

🧠 Organização do código

O algoritmo está dividido em três funções principais:

mainColors() – mostra as 7 cores básicas: off, vermelho, verde, azul, amarelo, ciano, roxo e branco.

showSpectrum() – faz uma varredura de 0 a 767, chamando showRGB(x) para gerar a transição contínua.

showRGB(x) – converte um índice 0..767 em intensidades R, G, B (0..255), dividindo em 3 zonas de 256 passos.



---

💻 Código (catodo comum)

// ---------- Configuração de pinos (PWM) ----------
const int RED_PIN   = 9;   // R
const int GREEN_PIN = 10;  // G
const int BLUE_PIN  = 11;  // B

// Tempo base de exibição (ms)
const int DISPLAY_TIME = 10;

void setup() {
  pinMode(RED_PIN,   OUTPUT);
  pinMode(GREEN_PIN, OUTPUT);
  pinMode(BLUE_PIN,  OUTPUT);

  // Começa com todos apagados
  analogWrite(RED_PIN,   0);
  analogWrite(GREEN_PIN, 0);
  analogWrite(BLUE_PIN,  0);
}

void loop() {
  mainColors();     // Mostra as cores básicas
  showSpectrum();   // Varrimento suave de cores (0..767)
}

// --------- 1) Cores básicas (7 cores) ---------
void mainColors() {
  // OFF
  setRGB(0, 0, 0);        delay(1000);

  // Vermelho
  setRGB(255, 0, 0);      delay(1000);

  // Verde
  setRGB(0, 255, 0);      delay(1000);

  // Azul
  setRGB(0, 0, 255);      delay(1000);

  // Amarelo = R + G
  setRGB(255, 255, 0);    delay(1000);

  // Ciano = G + B
  setRGB(0, 255, 255);    delay(1000);

  // Roxo/Magenta = R + B
  setRGB(255, 0, 255);    delay(1000);

  // Branco = R + G + B
  setRGB(255, 255, 255);  delay(1000);
}

// --------- 2) Varredura completa do espectro ---------
void showSpectrum() {
  for (int x = 0; x < 768; x++) {  // 0..767
    showRGB(x);
    delay(DISPLAY_TIME);
  }
}

// --------- 3) Conversão índice (0..767) -> (R,G,B) ---------
void showRGB(int color) {
  int redIntensity;
  int greenIntensity;
  int blueIntensity;

  if (color <= 255) {
    // Zona 1: 0..255  (vermelho -> verde)
    redIntensity   = 255 - color;  // R vai diminuindo
    greenIntensity = color;        // G vai aumentando
    blueIntensity  = 0;            // B desligado
  } else if (color <= 511) {
    // Zona 2: 256..511 (verde -> azul)
    int c = color - 256;
    redIntensity   = 0;            // R desligado
    greenIntensity = 255 - c;      // G vai diminuindo
    blueIntensity  = c;            // B vai aumentando
  } else {
    // Zona 3: 512..767 (azul -> vermelho)
    int c = color - 512;
    redIntensity   = c;            // R vai aumentando
    greenIntensity = 0;            // G desligado
    blueIntensity  = 255 - c;      // B vai diminuindo
  }

  setRGB(redIntensity, greenIntensity, blueIntensity);
}

// --------- Utilitário para escrever PWM nos 3 canais ---------
void setRGB(int r, int g, int b) {
  // Se o LED for ANODO COMUM, descomente as 3 linhas abaixo:
  // r = 255 - r;
  // g = 255 - g;
  // b = 255 - b;

  analogWrite(RED_PIN,   r);
  analogWrite(GREEN_PIN, g);
  analogWrite(BLUE_PIN,  b);
}


---

✅ Dicas e observações

Se as cores parecerem “invertidas” ou fracas, verifique:

Se o LED é anodo comum (inverta a lógica no setRGB).

Se os resistores estão em série com cada canal.

Se os pinos são PWM (9/10/11 no UNO).


Para transições mais suaves, aumente DISPLAY_TIME.

Você pode trocar os pinos de R, G, B—só ajuste as ligações e as constantes.



---
