# SpeedTest-Tracker

O [speedtest-tracker](https://docs.speedtest-tracker.dev/) é uma aplicação que utiliza a API do **Speedtest by Ookla** para fazer testes de velocidade na sua rede, gerando assim um histórico de como sua rede anda se comportando. 

Conta com uma interface web para administração e pode utilizar agendamentos cron para executar os testes em determinados horários automaticamente.


## Sumário
- [SpeedTest-Tracker](#speedtest-tracker)
  - [Sumário](#sumário)
  - [Requisitos e Dependências](#requisitos-e-dependências)
  - [Instalação](#instalação)
    - [Diretórios](#diretórios)
    - [Docker-Compose](#docker-compose)
      - [Portas](#portas)
      - [Volumes](#volumes)
      - [Rede](#rede)
      - [Proxy Reverso](#proxy-reverso)


## Requisitos e Dependências

- [Docker e Docker-Compose](https://docs.docker.com/)

## Instalação

### Diretórios

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

### Docker-Compose

#### Portas

```bash
# (docker-compose|stack.docker-compose).yml (Em services.app)

# Descomente (e/ou altere) as portas/serviços que você deseja oferecer.

ports:
# Porta Web (HTTP)
  - 80:80
```

Obs: não recomendado o uso da **Porta Web** via HTTP, use um proxy reverso no local com HTTPS. Por isso, só descomente essa instrução se realmente souber o que está fazendo.

#### Volumes

```bash
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

#### Rede

```bash 
# (docker-compose|stack.docker-compose).yml (Em networks.speedtest-net.ipam)

# Altere o valor caso necessário. 

config:
# Endereço da rede
  - subnet: '172.18.0.0/28'
```

#### Proxy Reverso

```bash
# (docker-compose|stack.docker-compose).yml (Em networks)

# Ajuste o campo "name" para ingressar na rede do seu proxy reverso.

reverse-proxy:
  name: 'reverse-proxy'
  external: true
```