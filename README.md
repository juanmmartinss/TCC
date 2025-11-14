# Sistema Integrado para Aquisição de Dados e Comando Remoto de Microssatélites em Tempo Real

![Status](https://img.shields.io/badge/Status-Concluído-green)
![TCC](https://img.shields.io/badge/TCC-Ciência%20da%20Computação-blue)

Este repositório contém o código-fonte e os conjuntos de dados do Trabalho de Conclusão de Curso (TCC) em Ciência da Computação pela Universidade Federal de São Paulo (UNIFESP).

O projeto consiste em um sistema integrado (Hardware/Software) para aquisição de telemetria e envio de telecomandos para um protótipo de microssatélite (CanSat), utilizando comunicação LoRa para o enlace de dados em tempo real.

## Estrutura do Repositório

* `/GSW_TCC`: O código-fonte da Estação de Controle Terrena (Backend e Frontend), configurada para rodar com Docker.
* `/ESP32`: Os firmwares em C (`sender.c` e `receiver.c`) para o CanSat e a estação receptora.
* `/data`: Conjuntos de dados (.csv) com os resultados dos testes de missão.
* `serial_reader.py`: Script host para ler a porta serial e alimentar o banco de dados da GSW.

## Como Executar o Projeto

Este projeto utiliza uma arquitetura híbrida: a Estação de Controle (GSW) roda via Docker, e o leitor serial roda no host para acessar a porta USB.

### 1. Hardware (Firmware)

1.  Navegue até a pasta `/ESP32`.
2.  Compile e envie `sender.c` para o hardware do CanSat.
3.  Compile e envie `receiver.c` para o hardware da estação receptora.

### 2. Estação de Controle (Docker)

1.  Conecte o hardware receptor na porta USB do seu computador.
2.  Na raiz do projeto, inicie o container da GSW (isso irá construir a imagem e iniciar o banco de dados e o backend):
    ```bash
    cd GSW_TCC
    sudo docker-compose up --build
    ```

### 3. Leitor Serial (Host)

1.  Em um **novo terminal**, na raiz do projeto, instale as dependências do leitor (ex: `pyserial`, `psycopg2-binary`).
2.  Ajuste a porta serial (ex: `/dev/ttyUSB0`) no arquivo `serial_reader.py`, se necessário.
3.  Execute o script:
    ```bash
    python3 serial_reader.py
    ```

### 4. Acesso

1.  Com tudo rodando, acesse a interface da GSW em: `http://localhost:8000`

## Pilha de Tecnologias

| Área | Tecnologias Utilizadas |
| :--- | :--- |
| **Hardware** | Heltec WiFi LoRa 32 (ESP32), NEO-6M, BME280, MPU6050, HMC5883L, Servo SG90 |
| **Firmware** | C/C++ (Arduino Framework) |
| **Backend (GSW)** | Python, Flask, Docker, Docker Compose |
| **Banco de Dados**| PostgreSQL |
| **Frontend (GSW)**| HTML, CSS, JavaScript, Chart.js |

## Autoria e Contexto Acadêmico

* **Autor:** Juan Marcos Martins
* **Orientador:** Prof. Dr. André Marcorin de Oliveira
* **Coorientador:** Prof. Dr. Lauro Paulo da Silva Neto

Trabalho de Conclusão de Curso apresentado à Universidade Federal de São Paulo (UNIFESP), 2025.
