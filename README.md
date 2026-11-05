# Dashboard
Dashboard Python


🤖 Dashboard Infraestrutura - Bot Coletor CRM & Monitor

Este projeto é um robô de automação e monitoramento desenvolvido em Python. Ele atua como uma ponte inteligente entre o portal de chamados (CRM Fácil), o painel de indicadores (Looker Studio) e a comunicação da equipe (Google Chat).

O sistema possui uma interface gráfica construída com Flet e executa ciclos automáticos de extração, processamento de regras de negócio e disparo de notificações em tempo real.

🚀 Funcionalidades Principais

Extração Automática: Coleta o histórico completo e atualizado de chamados do CRM Fácil utilizando requisições de API e reaproveitamento de tokens de sessão (com fallback para headless scraping via Selenium).

Integração Google Sheets: Atualiza de forma autônoma uma base de dados dedicada no Google Sheets (sheets.googleapis.com), que serve de fonte direta para os dashboards do Looker Studio.

Autenticação Segura: Implementa o fluxo de autorização do Google (oauth2.googleapis.com) para obter e renovar tokens de acesso em segundo plano (via refresh_token), sem interromper a execução contínua.

Motor de Alertas (Google Chat): Monitoriza os chamados em aberto e interage diretamente com os analistas via API do Google Chat, enviando alertas sobre:

🚨 Chamados sem Trava: Identifica chamados nas etapas de Aguardando Execução (N1, N2 e N3) que estão sem responsável e notifica o nível correspondente.

📩 Retorno do Cliente: Alerta o analista responsável quando a última resposta de um chamado for do solicitante.

⚠️ Atenção/Segurança: Monitoriza etapas críticas e SLA.

🛠️ Tecnologias Utilizadas

Linguagem: Python 3.12+

Interface Gráfica: Flet (UI nativa multiplataforma)

APIs do Google: Google Sheets API v4, Google Chat API, OAuth 2.0

Web Scraping/Automação: Selenium WebDriver, Requests

Empacotamento: PyInstaller (Geração de executável .exe autônomo)

⚙️ Como Funciona o Fluxo

Autenticação Google: No primeiro uso, o robô abre o navegador para o usuário autorizar o app (Sheets_OAuth). O token.json é gerado e, a partir daí, renovado silenciosamente via requisição HTTP (porta 443).

Sessão CRM: O bot acessa o Portal CRM. Se houver um token válido em memória, ele o reutiliza. Caso contrário, invoca o Selenium em background para fazer login e extrair o accessToken do sistema.

Processamento e Escrita: Os chamados são limpos, formatados e gravados na aba BD_Looker da planilha.

Notificações: A classe GoogleChatNotifier cruza os responsáveis (usuarios.json) com as regras de negócio e dispara mensagens diretas aos analistas que precisam agir.

⚠️ Configuração e Instalação (Para Desenvolvedores)

Clone este repositório.

Instale as dependências:

pip install flet pyinstaller gspread requests google-auth google-auth-oauthlib google-api-python-client google-auth-httplib2 selenium webdriver-manager flask

Credenciais (Importante): Solicite ao administrador o arquivo credentials.json do Google Cloud Console e coloque-o na raiz do projeto. Este arquivo não está versionado por motivos de segurança.

Execute o script principal:

