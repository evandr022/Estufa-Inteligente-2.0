# Estufa Inteligente 2.0

Este projeto consiste num sistema de monitorização e controlo automatizado para estufas, desenvolvido para a plataforma **Raspberry Pi Pico W**. O sistema utiliza o sistema operativo de tempo real **FreeRTOS** para gerir múltiplas tarefas simultâneas, garantindo eficiência na leitura de sensores, controlo de atuadores e conectividade sem fios.

## 📋 Funcionalidades

* **Monitorização Ambiental**: Leitura precisa de temperatura e humidade através do sensor AHT10 e medição de luminosidade via BH1750.
* **Controlo de Atuadores**: Gestão de um servo motor para abertura e fecho automatizado do teto da estufa com base na temperatura.
* **Interface Local**: Exibição de dados em tempo real num display LCD 16x2 via barramento I2C.
* **Conectividade IoT**: Envio periódico de telemetria via protocolo HTTP (JSON) para integração com dashboards como Node-RED.
* **Arquitetura Multitarefa**: Implementação baseada em FreeRTOS, utilizando Mutexes para garantir a integridade dos dados e evitar conflitos no barramento I2C compartilhado entre múltiplos dispositivos.

## 🛠️ Tecnologias Utilizadas

* **Microcontrolador**: Raspberry Pi Pico W.
* **Linguagem**: C++ (Padrão C++17).
* **RTOS**: FreeRTOS (Kernel v10+).
* **Pilha de Rede**: lwIP integrado com FreeRTOS.
* **Build System**: CMake e Ninja.

## 📂 Estrutura do Projeto

* `/include`: Ficheiros de cabeçalho (`.hpp`) e configurações do FreeRTOS e lwIP.
* `/src`: Implementação dos drivers dos sensores (AHT10, BH1750), LCD, Servo e lógica de rede.
* `main.cpp`: Ponto de entrada que inicializa o hardware e orquestra a criação das tarefas do FreeRTOS.
* `CMakeLists.txt`: Gestão de compilação e dependências do projeto.

## 🚀 Como Executar

### Pré-requisitos
1.  **Raspberry Pi Pico SDK** (versão 2.1.1 recomendada) instalado.
2.  Toolchain **arm-none-eabi-gcc** configurado.
3.  Utilitário **Ninja** para compilação rápida.

### Configuração e Compilação
1.  Clone o repositório:
    ```bash
    git clone [https://github.com/evandr022/Projeto_Estufa-Inteligente-2.0.git](https://github.com/evandr022/Projeto_Estufa-Inteligente-2.0.git)
    ```
2.  Configure as credenciais do Wi-Fi e o IP do servidor em `include/http_post.hpp`:
    ```cpp
    #define WIFI_SSID "Sua_Rede"
    #define WIFI_PASSWORD "Sua_Senha"
    #define HTTP_SERVER_IP "192.168.x.x"
    ```
3.  Compile o projeto:
    ```bash
    mkdir build && cd build
    cmake -G Ninja ..
    ninja
    ```
4.  Carregue o ficheiro `.uf2` resultante no Raspberry Pi Pico W.

## 📡 Integração de Dados
O sistema realiza o envio de dados via POST HTTP para o endpoint `/cofre-data` na porta `1880`, enviando o seguinte formato JSON:
```json
{
  "temperatura": 25.5,
  "umidade": 60.0,
  "status": "ABERTO"
}
```
## Video
https://drive.google.com/drive/folders/1kf4aFzvioK7A127l6sUpoVyXaascDTaU?usp=sharing

