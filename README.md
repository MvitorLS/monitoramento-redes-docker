<div align="center">

  <!-- ANIMATED TYPING HEADER -->
  <a href="https://github.com/MvitorLS/monitoramento-redes-docker">
    <img src="https://readme-typing-svg.demolab.com?font=Fira+Code&weight=600&size=24&pause=1000&color=00FF66&center=true&vCenter=true&width=650&height=65&lines=%F0%9F%93%A1+Infraestrutura+de+Monitoramento+de+Redes;Prometheus+%7C+Grafana+%7C+Blackbox+%7C+SNMP;Ping+RTT+%7C+Tr%C3%A1fego+RX%2FTX+%7C+Alertmanager" alt="Typing SVG" />
  </a>

  <p align="center">
    <b>Stack em Docker Compose para métricas de latência, disponibilidade de hosts e análise de tráfego de rede em tempo real.</b>
  </p>

  <p align="center">
    <img src="https://img.shields.io/badge/Prometheus-v2.54-E6522C?style=for-the-badge&logo=prometheus&logoColor=white"/>
    <img src="https://img.shields.io/badge/Grafana-v11.1-F46800?style=for-the-badge&logo=grafana&logoColor=white"/>
    <img src="https://img.shields.io/badge/Network_Probing-ICMP%2FHTTP%2FSNMP-00FF66?style=for-the-badge&logo=wireshark&logoColor=black"/>
  </p>

</div>

<img src="https://user-images.githubusercontent.com/73097560/115834477-dbab4500-a447-11eb-908a-139a6edaec5c.gif" width="100%" />

---

## 🛠️ Arquitetura da Infraestrutura de Rede

```mermaid
graph TD
    A[Roteadores / Switches / Servidores / IPs] -->|ICMP Ping / HTTP / TCP| B(Blackbox Exporter)
    C[Host Física & Placas de Rede] -->|Métricas do S.O.| D(Node Exporter)
    E[Containers Docker] -->|Consumo RX/TX| F(cAdvisor)
    G[Dispositivos SNMP] -->|SNMP OIDs| H(SNMP Exporter)

    B -->|Scrape 15s| I(Prometheus)
    D -->|Scrape 15s| I
    F -->|Scrape 15s| I
    H -->|Scrape 15s| I

    I -->|Disparo de Regras| J(Alertmanager)
    I -->|Painéis em Tempo Real| K(Grafana - Porta 3000)
```

---

## 📋 Componentes da Stack

<div align="center">

| Serviço | Função Principal na Rede | Porta | Access URL |
| :--- | :--- | :---: | :---: |
| 📊 **Grafana** | Dashboards interativos e mapas visuais | `3000` | `http://localhost:3000` |
| ⚡ **Prometheus** | Coleta de séries temporais e motor de busca PromQL | `9090` | `http://localhost:9090` |
| 🌐 **Blackbox Exporter** | Testes de latência ICMP Ping, HTTP Status e portas TCP | `9115` | `http://localhost:9115` |
| 💻 **Node Exporter** | Métricas de hardware e tráfego de interface (RX/TX Bytes/s) | `9100` | `http://localhost:9100` |
| 📡 **SNMP Exporter** | Leitura de métricas SNMP de ativos de rede | `9116` | `http://localhost:9116` |
| 🚨 **Alertmanager** | Gerenciador e roteador de alertas de indisponibilidade | `9093` | `http://localhost:9093` |
| 🐳 **cAdvisor** | Análise de tráfego e recursos dos containers Docker | `8080` | `http://localhost:8080` |

</div>

---

## ⚡ Início Rápido

```bash
# 1. Clone o repositório
git clone https://github.com/MvitorLS/monitoramento-redes-docker.git
cd monitoramento-redes-docker

# 2. Sobe toda a stack de monitoramento
./monitor up

# 3. Acesse o Grafana no navegador:
# http://localhost:3000 (Credenciais: admin / admin)
```

---

## 🎯 Adicionando Novos Alvos de Rede (IPs, Routers, Servidores)

Com a CLI `./monitor` você adiciona novos hosts diretamente no terminal:

```bash
# Adicionar teste de Ping ICMP em um Roteador/IP
./monitor add-target 192.168.1.1 ping

# Adicionar monitoramento HTTP em um Servidor/Site
./monitor add-target https://meusite.com http

# Recarregar as configurações do Prometheus
./monitor reload
```

---

<img src="https://user-images.githubusercontent.com/73097560/115834477-dbab4500-a447-11eb-908a-139a6edaec5c.gif" width="100%" />

<div align="center">
  <sub>Projetado e desenvolvido por <b>Matheus Vitor Lourenço Schionato</b></sub>
</div>
