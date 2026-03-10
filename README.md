## Description

Implementation of a distributed communication system between a **Mothership** and multiple **rovers**, featuring a reliable **UDP-based** mission management protocol, a **TCP-based telemetry** channel, and a **Ground Control** interface for real-time monitoring and control.

## Context

This project was developed as part of the **Computer Communications** course at the **University of Minho**.

The system simulates a space mission in which:
- the **Mothership** coordinates and monitors multiple rovers;
- the **rovers** request missions, execute tasks, and report progress;
- critical communication is handled through the **MissionLink (ML)** protocol over **UDP**;
- continuous telemetry is sent through the **TelemetryStream (TS)** protocol over **TCP**;
- the **Ground Control** consumes an observation API and displays the system state in real time.

## Main features

- **MissionLink** application-layer protocol over UDP
  - mission assignment
  - progress updates
  - completion confirmation
  - ACKs, timeouts, retransmissions, and duplicate detection

- **TelemetryStream** over TCP
  - continuous telemetry transmission
  - support for multiple rovers in parallel
  - structural message validation

- **Ground Control**
  - real-time rover state visualization
  - mission and progress tracking
  - manual priority mission assignment
  - communication with the Mothership through WebSocket

- **CORE integration**
  - multi-hop topology
  - latency and packet loss simulation
  - testing under multiple network scenarios

## Architecture

The system is divided into three main components:

### 1. Mothership
Central entity responsible for:
- receiving mission requests from rovers;
- assigning missions;
- receiving telemetry;
- maintaining the global system state;
- exposing data to Ground Control.

### 2. Rover
Each rover:
- requests missions from the Mothership;
- executes simulated missions;
- sends progress updates through MissionLink;
- sends periodic telemetry through TelemetryStream.

### 3. Ground Control
Monitoring client that:
- consumes the system state;
- displays rover and mission information;
- allows manual mission assignment to specific rovers.

## Protocols

### MissionLink (ML) — UDP
Application-layer protocol responsible for mission-critical communication.

#### Message types
- `READY` — rover available for a new mission
- `MISSION` — mission assigned by the Mothership
- `PROGRESS` — mission progress update
- `DONE` — mission completed
- `ACK` — explicit acknowledgment
- `NOMISSION` — no mission available

#### Reliability mechanisms
Since transport is handled over UDP, application-layer reliability mechanisms were implemented to ensure robustness:
- sequence numbering;
- explicit ACKs;
- timeout-based retransmissions;
- duplicate detection;
- idempotent retransmission of pending missions;
- retry limits to avoid indefinite blocking.

### TelemetryStream (TS) — TCP
Protocol responsible for the continuous transmission of rover monitoring data.

## Technologies used

- **Python**
- **UDP sockets**
- **TCP sockets**
- **WebSockets**
- **JSON**
- **CORE Network Emulator**

#Portugues
## Descrição

Implementação de um sistema distribuído de comunicação entre uma **Nave-Mãe** e múltiplos **rovers**, com um protocolo fiável sobre **UDP** para gestão de missões, um canal de **telemetria sobre TCP**, e uma interface **Ground Control** para observação e controlo em tempo real.

## Contexto

Este projeto foi desenvolvido no âmbito da unidade curricular de **Comunicações por Computador** da **Universidade do Minho**.

O sistema simula uma missão espacial em que:
- a **Nave-Mãe** coordena e monitoriza vários rovers;
- os **rovers** solicitam missões, executam tarefas e reportam progresso;
- a comunicação crítica é feita através do protocolo **MissionLink (ML)** sobre **UDP**;
- a telemetria contínua é enviada através do protocolo **TelemetryStream (TS)** sobre **TCP**;
- o **Ground Control** consome uma API de observação e apresenta o estado do sistema em tempo real.

## Principais funcionalidades

- Protocolo aplicacional **MissionLink** sobre UDP
  - atribuição de missões
  - atualizações de progresso
  - confirmação de conclusão
  - ACKs, timeouts, retransmissões e deteção de duplicados

- Protocolo **TelemetryStream** sobre TCP
  - envio contínuo de telemetria
  - suporte para múltiplos rovers em paralelo
  - validação estrutural das mensagens

- **Ground Control**
  - visualização em tempo real do estado dos rovers
  - acompanhamento de missões e progresso
  - atribuição manual de missões prioritárias
  - comunicação com a Nave-Mãe via WebSocket

- Integração com **CORE**
  - topologia com múltiplos saltos
  - simulação de latência e perda de pacotes
  - testes com vários cenários de rede

## Arquitetura

O sistema está dividido em três componentes principais:

### 1. Nave-Mãe
Entidade central responsável por:
- receber pedidos de missão dos rovers;
- atribuir missões;
- receber telemetria;
- manter o estado global do sistema;
- disponibilizar dados ao Ground Control.

### 2. Rover
Cada rover:
- solicita missões à Nave-Mãe;
- executa missões simuladas;
- envia atualizações de progresso via MissionLink;
- envia telemetria periódica via TelemetryStream.

### 3. Ground Control
Cliente de observação que:
- consome o estado do sistema;
- mostra informação de rovers e missões;
- permite enviar missões manuais para rovers específicos.

## Protocolos

### MissionLink (ML) — UDP
Protocolo aplicacional responsável pela comunicação crítica relacionada com missões.

#### Tipos de mensagens
- `READY` — rover disponível para nova missão
- `MISSION` — missão atribuída pela Nave-Mãe
- `PROGRESS` — atualização de progresso da missão
- `DONE` — missão concluída
- `ACK` — confirmação explícita
- `NOMISSION` — ausência de missão disponível

#### Mecanismos de fiabilidade
Como o transporte é feito sobre UDP, foram implementados mecanismos aplicacionais para garantir robustez:
- numeração de sequência;
- ACKs explícitos;
- retransmissões por timeout;
- deteção de duplicados;
- reenvio idempotente de missões pendentes;
- limite de tentativas para evitar bloqueios indefinidos.

### TelemetryStream (TS) — TCP
Protocolo responsável pela transmissão contínua de dados de monitorização do rover.

## Tecnologias utilizadas

- **Python**
- **UDP sockets**
- **TCP sockets**
- **WebSockets**
- **JSON**
- **CORE Network Emulator**
