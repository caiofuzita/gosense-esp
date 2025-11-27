# ESP32-CAM Web Server com WiFiManager e mDNS

Este projeto implementa um servidor de streaming de vídeo utilizando o módulo **ESP32-CAM (Modelo AI-Thinker)**. 

O grande diferencial deste código é a integração com o **WiFiManager**, que elimina a necessidade de gravar o nome da rede (SSID) e a senha diretamente no código (hardcoding). Se a câmera não conseguir se conectar, ela cria automaticamente um Ponto de Acesso para que você configure a rede via celular ou PC.

Além disso, utiliza **mDNS**, permitindo o acesso via URL amigável (`http://esp32cam.local`) sem precisar descobrir o IP.

## 📋 Funcionalidades

- **Streaming de Vídeo:** Servidor HTTP dedicado para transmissão de imagens.
- **WiFiManager (Captive Portal):** Cria uma rede `ConfigurarCameraESP32` para configuração inicial de WiFi sem reprogramar a placa.
- **mDNS:** Acesso facilitado via endereço `http://esp32cam.local`.
- **Ajuste Automático:** Detecta se há PSRAM disponível para ajustar a qualidade e resolução (UXGA vs SVGA) automaticamente.

## 🛠️ Hardware Necessário

- 1x Módulo ESP32-CAM (Modelo AI-Thinker).
- 1x Conversor USB-TTL (FTDI) para programação.
- Fonte de alimentação 5V estável.

## 💻 Dependências de Software

Para compilar este código na **Arduino IDE**, certifique-se de ter instalado:

1. **Pacote de Placas ESP32:**
   - Adicione no *Preferences*: `https://raw.githubusercontent.com/espressif/arduino-esp32/gh-pages/package_esp32_index.json`
   - Instale via *Boards Manager*.

2. **Biblioteca WiFiManager:**
   - Autor: *tzapu*
   - Instale via *Library Manager* (Sketch > Include Library > Manage Libraries).

3. **Arquivo Auxiliar:**
   - O arquivo `camera_pins.h` deve estar na mesma pasta do seu sketch (`.ino`) com as definições dos pinos do modelo AI-Thinker.

## ⚙️ Configuração da IDE

Ao carregar o código, utilize as seguintes configurações em **Tools**:

- **Board:** AI Thinker ESP32-CAM
- **CPU Frequency:** 240MHz (WiFi/BT)
- **Flash Frequency:** 80MHz
- **Partition Scheme:** Huge APP (3MB No OTA/1MB SPIFFS) *(Essencial para evitar erros de espaço)*.

## 🚀 Como Usar

### 1. Upload do Código
1. Conecte o **GPIO 0** ao **GND** no ESP32-CAM.
2. Conecte o adaptador FTDI e faça o upload.
3. Após o upload, **remova a conexão entre GPIO 0 e GND**.
4. Pressione o botão **RESET** na placa.

### 2. Primeiro Acesso (Configuração WiFi)
Como não há senha gravada, o ESP32 entrará em modo de configuração:

1. No seu celular ou PC, procure por uma rede WiFi chamada: `ConfigurarCameraESP32`.
2. Conecte-se a ela. Uma página deve abrir automaticamente (se não, acesse `192.168.4.1` no navegador).
3. Clique em **Configure WiFi**, selecione sua rede local e insira a senha.
4. O ESP32 irá salvar, reiniciar e conectar automaticamente à sua rede.

### 3. Acessando a Câmera
Após a reinicialização, verifique o Monitor Serial ou simplesmente acesse no navegador:

> **http://esp32cam.local**

Caso o mDNS não funcione no seu dispositivo (comum em alguns Androids), verifique o IP no Monitor Serial (ex: `192.168.1.15`).

## ⚠️ Solução de Problemas

- **Erro "Brownout detector was triggered":** A fonte de energia é insuficiente. O WiFi e a Câmera consomem picos de energia. Troque o cabo USB ou use uma fonte externa de 5V/2A.
- **Falha na Câmera (Erro 0x...):** Verifique se o cabo flat da câmera está bem encaixado e travado no conector.
