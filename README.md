Projeto: Sistema de Controle de LED e Monitoramento de Luminosidade com ESP32 e MQTT
Descrição
Este projeto utiliza um ESP32 para se conectar a uma rede Wi-Fi e a um broker MQTT. O objetivo é controlar o estado de um LED onboard (ligado/desligado) remotamente e monitorar a luminosidade de um ambiente através de um sensor de luminosidade (potenciômetro). As leituras e o estado do LED são enviados para o broker MQTT em tópicos específicos, permitindo a interação com o dispositivo via MQTT.

Funcionalidades
Controle Remoto do LED: Permite ligar e desligar o LED onboard do ESP32 via comandos MQTT.
Monitoramento de Luminosidade: O valor da luminosidade é lido de um potenciômetro e enviado periodicamente ao broker MQTT.
Reconexão Automática: Se o ESP32 perder a conexão Wi-Fi ou MQTT, ele tentará reconectar automaticamente.
Indicação de Estado do LED: O estado do LED é enviado constantemente ao broker MQTT.
Componentes Utilizados
ESP32
LED onboard (pino D4)
Potenciômetro (pino 34)
Broker MQTT (Mosquitto ou outro)
Configurações de Rede e MQTT
O código utiliza as seguintes configurações:

SSID: Nome da rede Wi-Fi (Wokwi-GUEST)
Senha: Senha da rede Wi-Fi (nesse caso, vazio)
Broker MQTT: IP do broker MQTT (4.236.177.132)
Porta MQTT: Porta utilizada pelo broker MQTT (1883)
Tópicos MQTT:
/TEF/lamp001/cmd: Tópico de subscrição para comandos de controle do LED.
/TEF/lamp001/attrs: Tópico para publicar o estado atual do LED.
/TEF/lamp001/attrs/l: Tópico para publicar o valor de luminosidade.
Fluxo do Projeto
O ESP32 se conecta à rede Wi-Fi especificada.
O ESP32 se conecta ao broker MQTT.
O LED onboard pisca 10 vezes para indicar a inicialização bem-sucedida.
O ESP32 publica o estado inicial do LED como "ligado" no tópico /TEF/lamp001/attrs.
O ESP32 se mantém em um loop que:
Verifica as conexões Wi-Fi e MQTT.
Envia o estado atual do LED ao broker.
Lê a luminosidade do potenciômetro e publica o valor no tópico /TEF/lamp001/attrs/l.
Comandos MQTT
Os comandos MQTT aceitos para o controle do LED são:

Ligar LED: lamp001@on|
Desligar LED: lamp001@off|
Como Usar
Faça o upload do código para o ESP32 utilizando a IDE Arduino.
Certifique-se de que o broker MQTT esteja funcionando e acessível pelo IP configurado.
Abra o monitor serial na IDE para verificar as mensagens de debug.
Utilize um cliente MQTT para enviar os comandos de controle do LED e receber os valores de luminosidade.
Dependências
Este projeto utiliza as seguintes bibliotecas:

WiFi.h: Para conectar o ESP32 à rede Wi-Fi.
PubSubClient.h: Para realizar a comunicação via protocolo MQTT.
