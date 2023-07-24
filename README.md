# SpeedTest-Tracker

O [speedtest-tracker](https://docs.speedtest-tracker.dev/) é uma aplicação que utiliza a API do **Speedtest by Ookla** para fazer testes de velocidade na sua rede, gerando assim um histórico de como sua rede anda se comportando. 

Conta com uma interface web para administração e pode utilizar agendamentos **cron** para executar os testes em determinados horários automaticamente.


## Sumário
- [SpeedTest-Tracker](#speedtest-tracker)
  - [Sumário](#sumário)
  - [1. Requisitos e Dependências](#1-requisitos-e-dependências)
  - [2. Instalação](#2-instalação)
    - [2.1 Diretórios](#21-diretórios)
    - [2.2 Docker-Compose](#22-docker-compose)
      - [2.2.1 Portas](#221-portas)
      - [2.2.2 Volumes](#222-volumes)
      - [2.2.3 Rede](#223-rede)
      - [2.2.4 Proxy Reverso](#224-proxy-reverso)
  - [3. Configurando](#3-configurando)


## 1. Requisitos e Dependências

- [Docker e Docker-Compose](https://docs.docker.com/)
- Versões testadas: ***0.11.17***

## 2. Instalação

### 2.1 Diretórios

```bash
# Crie os diretórios

# Dir. Config
$ mkdir $(pwd)/config

# Dir. Web
$ mkdir $(pwd)/config/web
```

Sugestão (no Linux):

- Dir. Config: /var/lib/speedtest-tracker
- Dir. Web: /var/lib/speedtest-tracker/web

### 2.2 Docker-Compose

#### 2.2.1 Portas

```yml
# (docker-compose|stack.docker-compose).yml (Em services.app)

# Descomente (e/ou altere) as portas/serviços que você deseja oferecer.

ports:
# Porta Web (HTTP)
  - 80:80
```

> Obs: não recomendado o uso da **Porta Web** via HTTP, use um proxy reverso no local com HTTPS, como: [Nginx](https://github.com/nutecuneal/proxy-manager-deployer) ou [Traefik](https://doc.traefik.io/traefik/). Por isso, só descomente essa instrução se realmente souber o que está fazendo.

#### 2.2.2 Volumes

```yml
# (docker-compose|stack.docker-compose).yml (Em services.app)

# Aponte para as pastas criadas anteriormente.

# Antes
volumes:
  - $(pwd)/speedtest-tracker:/config
  - $(pwd)/speedtest-tracker/web:/etc/ssl/web

# Depois (exemplo)
volumes:
  - /var/lib/speedtest-tracker:/config
  - /var/lib/speedtest-tracker/web:/etc/ssl/web
```

#### 2.2.3 Rede

```yml 
# (docker-compose|stack.docker-compose).yml (Em networks.speedtest-net.ipam)

# Altere o valor caso necessário. 

config:
# Endereço da rede
  - subnet: '172.18.0.0/28'
```

#### 2.2.4 Proxy Reverso

```yml
# (docker-compose|stack.docker-compose).yml (Em networks)

# Ajuste o campo "name" para ingressar na rede do seu proxy reverso.

reverse-proxy:
  name: 'reverse-proxy'
  external: true
```

## 3. Configurando

> Clique aqui para ir ao guia de configuração