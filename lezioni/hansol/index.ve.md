# HAN SOLOminer e Nerdminer: Introduzion al mining Bitcoin

## Introduzion
HAN SOLOminer e Nerdminer xe dispositivi educativi che permet de imparar i concetti base del mining Bitcoin attraverso un "gioco" divertente e istruttivo. In questa lezion esploreremo come funzionano e come configurarli.

## Cossa xe il mining Bitcoin?

### Concetti base
- **Validazion**: Verifica de le transazioni
- **Consenso**: Accord tra i nodi de la rete
- **Sicurezza**: Protezion da attacchi
- **Incentivi**: Premio par i miner

### Come funziona
1. Le transazioni vengono racolte in un blocco
2. I miner competono par trovar un hash valido
3. Il primo che trova la soluzion riceve il premio
4. Il blocco viene aggiunto alla blockchain

## HAN SOLOminer

### Caratteristiche
- **Hardware**: ESP32
- **Display**: OLED 128x64
- **Algoritmo**: SHA256
- **Scopo**: Educativo

### Funzionalità
- Mining simulato
- Visualizazion de hash
- Statistiche in tempo reale
- Connession WiFi

### Hardware supportato
- **LILYGO T-Display S3**: Display integrato
- **ESP32 DevKit**: Display esterno
- **M5-StampS3**: Formato compatto

## Nerdminer

### Caratteristiche
- **Hardware**: ESP32-S3
- **Display**: TFT color
- **Algoritmo**: SHA256
- **Scopo**: Educativo e decorativo

### Funzionalità
- Mining simulato avanzato
- Interfaccia grafica
- Statistiche dettagliate
- Connession WiFi

### Hardware supportato
- **LILYGO T-Display S3**: Display integrato
- **ESP32-S3 DevKit**: Display esterno
- **M5-StampS3**: Formato compatto

## Installazion

### Metodo 1: Web Flasher
1. Vai su https://nerdminer.tech
2. Scegli il tuo hardware
3. Clicca "Flash"
4. Segui le istruzion

### Metodo 2: PlatformIO
```bash
# Clona il repository
git clone https://github.com/BitMaker-hub/NerdMiner_v2
cd NerdMiner_v2

# Installa PlatformIO
pip install platformio

# Compila e flash
pio run -t upload
```

### Metodo 3: Arduino IDE
1. Apri Arduino IDE
2. Installa ESP32 board manager
3. Apri il file .ino
4. Compila e upload

## Configurazion

### WiFi
```cpp
// Configura WiFi
const char* ssid = "Tua_Rete_WiFi";
const char* password = "Tua_Password";
```

### Mining Pool
```cpp
// Configura pool
const char* poolUrl = "stratum+tcp://pool.example.com:3333";
const char* wallet = "Tua_Wallet_Address";
const char* workerName = "HAN_SOLOminer";
```

### Display
```cpp
// Configura display
#define SCREEN_WIDTH 128
#define SCREEN_HEIGHT 64
#define OLED_RESET -1
```

## Funzionalità avanzate

### Statistiche
- Hash rate in tempo reale
- Tempo di mining
- Blocchi trovati
- Temperatura

### Connession
- WiFi automatico
- Web interface
- API REST
- MQTT support

### Personalizazion
- Temi display
- Animazioni
- Suoni
- LED RGB

## Esempi de codice

### Setup base
```cpp
#include <WiFi.h>
#include <Wire.h>
#include <Adafruit_GFX.h>
#include <Adafruit_SSD1306.h>

// Configurazion display
Adafruit_SSD1306 display(SCREEN_WIDTH, SCREEN_HEIGHT, &Wire, OLED_RESET);

void setup() {
    Serial.begin(115200);
    
    // Inizializa display
    if(!display.begin(SSD1306_SWITCHCAPVCC, 0x3C)) {
        Serial.println(F("SSD1306 allocation failed"));
        for(;;);
    }
    
    // Connession WiFi
    WiFi.begin(ssid, password);
    while (WiFi.status() != WL_CONNECTED) {
        delay(500);
        Serial.print(".");
    }
    
    // Avvia mining
    startMining();
}
```

### Loop principale
```cpp
void loop() {
    // Aggiorna display
    updateDisplay();
    
    // Mining loop
    mineBlock();
    
    // Verifica connession
    checkConnection();
    
    delay(100);
}
```

### Funzion mining
```cpp
void mineBlock() {
    // Genera nonce casuale
    uint32_t nonce = random(0xFFFFFFFF);
    
    // Calcola hash
    String hash = calculateHash(blockHeader + nonce);
    
    // Verifica difficoltà
    if (hash.startsWith("000")) {
        blockFound();
    }
    
    hashCount++;
}
```

## Troubleshooting

### Problemi comuni
- **Display non funziona**: Verifica connession I2C
- **WiFi non si connette**: Verifica credenziali
- **Mining lento**: Verifica CPU e memoria

### Debug
```cpp
// Abilita debug
#define DEBUG 1

#ifdef DEBUG
    Serial.println("Debug: " + message);
#endif
```

## Progetti avanzati

### Cluster mining
- Multipli dispositivi
- Coordinazion via WiFi
- Statistiche aggregate

### Web interface
- Dashboard web
- Controllo remoto
- Monitoraggio

### Integrazion con pool
- Connession reali
- Statistiche pool
- Pagamenti

## Conclusione
HAN SOLOminer e Nerdminer xe ottimi strumenti par imparar il mining Bitcoin. Anche se non producono Bitcoin reali, forniscono na comprension pratica de come funziona il processo de mining e la rete Bitcoin. 