# Configuração

## Sumário
- [Configuração](#configuração)
  - [Sumário](#sumário)
  - [1. Agendamento dos testes](#1-agendamento-dos-testes)
  - [2. Notificações](#2-notificações)
    - [2.1 Telegram](#21-telegram)

## 1. Agendamento dos testes

- No menu lateral, em ***settings*** clique em ***general***.
- Na área ***Site Settings***:
  - **Site name**: Define o nome que será exibido no painel lateral e na tela de login.
  - **Timezone**: Escolha a região e o horário que vai ser exibido os seus testes.
  - **Time format**: Define como será exibido o formato do tempo (default: mês,dia,ano,h,m,s). 
  - **Content width**: Escolha como o resultado vai se comportar na largura da janela.
- Na área ***Speedtest Settings***:
  - **Speedtest schedule**: Você define em um formato ***cron*** o período em que os testes devem ser realizados, você pode utilizar o [Cronhub](https://crontab.cronhub.io/) para auxiliar na configuração.
  - **Speedtest Server ID**: Você pode escolher um servidor fixo para realização dos testes (defaut: vazio para o teste escolher o server automaticamente).
- Com a configuração feita clique em salvar e verifique se tudo funciona como desejado.

## 2. Notificações

### 2.1 Telegram

Para poder ativar as notificações via telegram, você precisa ter uma conta no telegram e criar um bot para o serviço:

- No telegram utilize o [BotFather](https://t.me/BotFather) para criar seu bot.
- Após criado, adicione o **token** do bot no arquivo oculto de variáveis de ambiente ***.env*** na linha **TELEGRAM_BOT_TOKEN**, localizado no diretório ***.config.*** Se você montou as pastas em seu host, o arquivo esta lá. Ex.: ***/var/lib/speedtest-tracker/.env***
- Agora você precisa:
  -  Criar um grupo no telegram;
  -  Adicionar seu bot;
  -  E descobrir qual é o ID do grupo. Para descobrir o ID você pode utilizar o bot **@Get_Id_Bot**.
- Com o ID em mãos, acesse a interface de administração:
  - No menu lateral, em ***settings*** clique em ***notifications***.
  - Na área **Notifications** procure por telegram e clique em ***enable***:
    - Na área **Triggers** você pode escolher em que condições a notificação deve ser enviada.
    - Na área **Recipients** clique em ***Add to recipients***.
    - No campo **Telegram chat id** insira o ID do grupo adquirido nos passos anteriores.
    - Clique em **Test telegram channel**, se você conseguir receber uma mensagem de teste no seu grupo o bot foi configurado corretamente. Senão funcionar, verique se o ***ID*** e ***TELEGRAM_BOT_TOKEN*** foram inseridos corretamente. 
