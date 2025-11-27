ESP32-CAM Web Server com WiFiManager
Este projeto implementa um servidor de streaming de vídeo utilizando o módulo ESP32-CAM (Modelo AI-Thinker). O diferencial deste código é a integração com o WiFiManager, que permite conectar a câmera a diferentes redes WiFi sem a necessidade de reprogramar o código (hardcoding) com o SSID e a senha.

Além disso, o projeto utiliza mDNS, permitindo acessar a câmera através de uma URL amigável (http://esp32cam.local) em vez de depender do endereço IP.

📋 Funcionalidades
Streaming de Vídeo: Transmissão de vídeo via protocolo HTTP.

Gerenciador de WiFi (Captive Portal): Se o ESP32 não conseguir conectar a uma rede conhecida, ele cria um Ponto de Acesso (AP) para configuração.

mDNS: Acesso facilitado via http://esp32cam.local.

Configuração Automática de Qualidade: Ajusta a resolução e o buffer baseada na presença de PSRAM.

🛠️ Hardware Necessário
Módulo ESP32-CAM (Modelo AI-Thinker).

Módulo Conversor USB-TTL (FTDI) para programação.

Jumpers.

Fonte de alimentação 5V (recomendado) ou 3.3V.

💻 Dependências de Software
Para compilar este código na Arduino IDE, você precisará das seguintes bibliotecas e pacotes:

Pacote ESP32:

Vá em File > Preferences e adicione a URL no Gerenciador de Placas: https://raw.githubusercontent.com/espressif/arduino-esp32/gh-pages/package_esp32_index.json

Vá em Tools > Board > Boards Manager, busque por esp32 e instale (por Espressif Systems).

Biblioteca WiFiManager:

Vá em Sketch > Include Library > Manage Libraries.

Busque por WiFiManager (por tzapu) e instale a versão mais recente.

Nota: Certifique-se de que o arquivo camera_pins.h está presente na mesma pasta do seu projeto (.ino), contendo as definições de pinos para o modelo AI-Thinker.

🚀 Como Instalar e Carregar
Conexão para Upload:

Conecte o pino GPIO 0 ao GND (isso coloca o ESP32 em modo de flash).

Conecte o conversor USB-TTL aos pinos U0R (RX) e U0T (TX).

Configuração da IDE:

Board: AI Thinker ESP32-CAM

CPU Frequency: 240MHz (WiFi/BT)

Flash Frequency: 80MHz

Partition Scheme: Huge APP (3MB No OTA/1MB SPIFFS) - Importante para caber o código da câmera.

Upload:

Clique em "Upload" na Arduino IDE.

Assim que terminar ("Done uploading"), remova o jumper entre GPIO 0 e GND.

Pressione o botão de RESET no módulo.

📡 Como Usar (Primeiro Acesso)
Como não há senha de WiFi gravada no código, siga os passos abaixo na primeira vez que ligar:

Modo de Configuração:

Abra o Monitor Serial (Baud Rate 115200) para acompanhar o status.

O ESP32 tentará conectar. Se falhar, criará uma rede WiFi chamada: ConfigurarCameraESP32

Conectando ao Portal:

Use seu celular ou PC para conectar na rede WiFi ConfigurarCameraESP32.

Uma janela deve abrir automaticamente (Captive Portal). Se não abrir, acesse 192.168.4.1 no navegador.

Clique em Configure WiFi, selecione sua rede doméstica e digite a senha.

Acessando a Câmera:

O ESP32 irá reiniciar e conectar à sua rede.

No navegador do seu PC/Celular (conectado à mesma rede), acesse:

URL: http://esp32cam.local

Alternativa: Verifique o IP impresso no Monitor Serial (ex: http://192.168.1.15).

⚠️ Solução de Problemas Comuns
Erro "Brownout detector was triggered": Geralmente causado por cabo USB de má qualidade ou porta USB que não fornece corrente suficiente. Tente usar uma fonte externa de 5V.

Falha na inicialização da câmera (0x...): Verifique se o módulo da câmera está bem encaixado no slot.

mDNS não funciona (não abre .local): O mDNS funciona nativamente no Mac, iPhone e Windows 10/11 (com Bonjour). Em alguns Androids ou Windows antigos, pode ser necessário usar o endereço IP direto.
