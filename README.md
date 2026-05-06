# EletroUni

Dashboard web para gestao de consumo IoT com simulador de telemetria e integracao via Make (webhooks).

## Visao geral
- Login e cadastro com envio para Make (URL_GESTAO)
- Cadastro de equipamentos com calculo de custo e KPIs
- Monitoramento com IA Insight (Make + Gemini)
- Simulador de telemetria para testes
- Persistencia local (localStorage)
- UX: filtros, busca, desfazer, atalhos e status de sincronizacao

## Estrutura
- index.html: app completa (HTML, CSS e JS)

## Como usar
1) Abra o arquivo index.html no navegador.
2) Use o login de admin para ver o simulador:
   - Email: admin@teste.com
3) Crie uma conta nova com nome, email e senha.
4) Cadastre dispositivos e use o simulador.

## Configuracao Make
No topo do JS em index.html:
- URL_GESTAO: webhook do Make para login/cadastro/equipamento
- URL_TELEMETRIA: webhook do Make para telemetria + IA

Exemplo (trecho no arquivo):
- const URL_GESTAO = 'https://hook.us2.make.com/...';
- const URL_TELEMETRIA = 'https://hook.us2.make.com/...';

## Payloads principais
### Login
- acao: "login"
- email, senha

### Cadastro de usuario
- acao: "cadastro_user"
- nome, email, senha
- idempotency_key

### Cadastro de equipamento
- acao: "cadastro_equip"
- email, nome, tensao, comodo, potencia_w, timestamp
- idempotency_key

### Telemetria (simulador)
- tipo: "telemetria_iot"
- email, dispositivo, voltagem, consumo_w, status, timestamp
- idempotency_key
- metadata: origem, corrente_a, fator_potencia, kwh_estimado_hora

## Resposta esperada do Make (IA)
O app tenta ler campos como:
- analisar (preferencial)
- insight, message, texto, resultado, output, text

## Atalhos de teclado
- Alt+D: Meus Dispositivos
- Alt+N: Novo Aparelho
- Alt+M: Monitoramento (admin)
- Alt+S: Simulador (admin)
- /: focar busca
- Esc: fechar modal de recuperacao

## Observacoes
- Para evitar duplicacao em caso de retry, os payloads possuem idempotency_key.
- Os dados sao persistidos no navegador via localStorage.

## Licenca
Defina a licenca conforme sua necessidade.
