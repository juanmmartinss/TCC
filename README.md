# Sistema Integrado de CanSat: Aquisição de Dados e Telecomando via LoRa

![Status](https://img.shields.io/badge/Status-Concluído-green)
![TCC](https://img.shields.io/badge/TCC-Ciência%20da%20Computação-blue)

Este repositório contém o código-fonte e os conjuntos de dados do Trabalho de Conclusão de Curso (TCC) em Ciência da Computação pela Universidade Federal de São Paulo (UNIFESP).

O projeto consiste em um sistema integrado (Hardware/Software) para aquisição de telemetria e envio de telecomandos para um protótipo de microssatélite (CanSat), utilizando comunicação LoRa para o enlace de dados em tempo real.

## Visão Geral do Sistema

O sistema é composto por três componentes principais:

1.  **Firmware do CanSat (C++):** Embarcado no ESP32, coleta dados de múltiplos sensores (GPS, BME280, MPU6050, HMC5883L), formata os pacotes de telemetria e os transmite via LoRa. Também é responsável por receber e executar telecomandos (ex: acionar servo).
2.  **Hardware Receptor (ESP32):** Atua como uma ponte (bridge), recebendo os pacotes LoRa e retransmitindo-os via comunicação serial (USB) para a estação base.
3.  **Estação de Controle Terrena (GSW):** Uma aplicação Python (Flask) que lê a porta serial, processa os dados, armazena a telemetria em um banco de dados PostgreSQL e os exibe em uma interface web com gráficos em tempo real (Chart.js).

## Pilha de Tecnologias

| Área | Tecnologias Utilizadas |
| :--- | :--- |
| **Hardware** | Heltec WiFi LoRa 32 (ESP32), NEO-6M, BME280, MPU6050, HMC5883L, Servo SG90 |
| **Firmware** | C++ (Arduino Framework / PlatformIO) |
| **Backend (GSW)** | Python, Flask, Pyserial, SQLAlchemy |
| **Banco de Dados**| PostgreSQL |
| **Frontend (GSW)**| HTML, CSS, JavaScript, Chart.js |

## Como Executar o Projeto

### 1. Hardware e Firmware

1.  Monte os circuitos do CanSat (Sender) e do Receptor (Receiver) conforme os esquemáticos.
2.  Abra os diretórios `/firmware/` na sua IDE (ex: PlatformIO ou Arduino IDE).
3.  Instale as bibliotecas de hardware necessárias (listadas nos arquivos).
4.  Compile e envie o código `cansat_sender` para o CanSat e `gsw_receiver` para a estação receptora.

### 2. Software (Estação de Controle Terrena)

1.  Certifique-se de ter o **Python 3.9+** e o **PostgreSQL** instalados e em execução.
2.  Clone este repositório e navegue até a pasta `/software`:
    ```bash
    git clone [https://github.com/](https://github.com/)[seu-usuario]/[seu-repositorio].git
    cd [seu-repositorio]/software/
    ```
3.  Crie e ative um ambiente virtual:
    ```bash
    python -m venv venv
    source venv/bin/activate  # (ou venv\Scripts\activate no Windows)
    ```
4.  Instale as dependências:
    ```bash
    pip install -r requirements.txt
    ```
5.  Configure sua string de conexão com o banco de dados no arquivo `config.py`.
6.  Conecte o hardware receptor na porta USB.
7.  Execute o leitor serial (ajuste a porta COM/tty no script, se necessário):
    ```bash
    python3 serial_reader.py
    ```
8.  Em um segundo terminal, inicie o servidor web:
    ```bash
    python app.py
    ```
9.  Acesse a GSW em `localhost:8000`.

## Conjunto de Dados (Dataset)

A pasta `/datasets` contém os dados brutos (.csv) de telemetria coletados durante os testes de campo, que podem ser utilizados para análise e validação.

## Autoria e Contexto Acadêmico

* **Autor:** Juan Marcos Martins
* **Orientador:** Prof. Dr. André Marcorin de Oliveira
* **Coorientador:** Prof. Dr. Lauro Paulo da Silva Neto

Trabalho de Conclusão de Curso apresentado à Universidade Federal de São Paulo (UNIFESP), 2025.

## Licença

Este projeto está licenciado sob a Licença MIT. Veja o arquivo `LICENSE.txt` para mais detalhes.
