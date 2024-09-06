## Projeto: Sistema de Controle de LED e Monitoramento de Luminosidade com ESP32 e MQTT
## Link youtube 
https://www.youtube.com/watch?v=2uKJQkGXOCA
### Descrição
![image](https://github.com/user-attachments/assets/343d4040-2ff6-4cd4-bdb5-741a46d6a83a)

Este projeto utiliza um ESP32 para conectar a uma rede Wi-Fi e a um broker MQTT. O objetivo é controlar remotamente o estado de um LED onboard (ligado/desligado) e monitorar a luminosidade do ambiente por meio de um sensor (potenciômetro). As leituras de luminosidade e o estado do LED são publicados em tópicos MQTT, permitindo interação remota.

### Funcionalidades

- **Controle Remoto do LED**: Liga e desliga o LED onboard via comandos MQTT.
- **Monitoramento de Luminosidade**: Lê e publica periodicamente o valor da luminosidade.
- **Reconexão Automática**: Tenta reconectar à rede Wi-Fi e ao broker MQTT em caso de perda de conexão.
- **Indicação de Estado do LED**: O estado atual do LED é publicado no broker MQTT.

### Componentes Utilizados

- **ESP32**
- **LED onboard (pino D4)**
- **Potenciômetro (pino 34)**
- **Broker MQTT (Mosquitto ou outro)**

### Configurações de Rede e MQTT

- **SSID**: Nome da rede Wi-Fi (`Wokwi-GUEST`)
- **Senha**: Senha da rede Wi-Fi (vazia neste exemplo)
- **Broker MQTT**: IP do broker MQTT (`4.236.177.132`)
- **Porta MQTT**: Porta do broker MQTT (`1883`)
- **Tópicos MQTT**:
  - **/TEF/lamp001/cmd**: Tópico para controle do LED.
  - **/TEF/lamp001/attrs**: Tópico para o estado do LED.
  - **/TEF/lamp001/attrs/l**: Tópico para o valor da luminosidade.

### Fluxo do Projeto

1. O ESP32 se conecta à rede Wi-Fi configurada.
2. Conecta-se ao broker MQTT.
3. O LED onboard pisca 10 vezes para sinalizar a inicialização.
4. O ESP32 publica o estado inicial do LED como "ligado" no tópico `/TEF/lamp001/attrs`.
5. No loop principal:
   - Verifica as conexões Wi-Fi e MQTT.
   - Envia o estado do LED ao broker.
   - Lê a luminosidade do potenciômetro e publica no tópico `/TEF/lamp001/attrs/l`.

### Comandos MQTT

Os seguintes comandos podem ser enviados via MQTT para controlar o LED:

- **Ligar LED**: `lamp001@on|`
- **Desligar LED**: `lamp001@off|`

### Como Usar

1. Faça o upload do código no ESP32 através da IDE Arduino.
2. Certifique-se de que o broker MQTT está rodando e acessível no IP configurado.
3. Abra o monitor serial da IDE Arduino para visualizar as mensagens de debug.
4. Use um cliente MQTT (como o MQTT.fx ou o Mosquitto CLI) para enviar comandos e visualizar os dados publicados.

### Dependências

- **WiFi.h**: Biblioteca para conectar o ESP32 ao Wi-Fi.
- **PubSubClient.h**: Biblioteca para comunicação via protocolo MQTT.

### Publicação de Exemplo

A mensagem publicada com o valor da luminosidade segue o formato JSON:

```json
{
  "l": 75
}
