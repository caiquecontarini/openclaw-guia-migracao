# 06 — Arquitetura Avancada: Claude Code Local + OpenClaw na VPS

Esta e a arquitetura de dois agentes se sincronizando em tempo real via Git.

## Visao Geral

Local (PC/Mac):
- Claude Code rodando no terminal
- Clone do repositorio em ~/segundo-cerebro
- Skills: /cerebro, /rotina, /salve
- Hook SessionStart: git pull automatico ao abrir

VPS (OpenClaw):
- Servidor Linux com OpenClaw
- Mesmo repositorio clonado
- ~60 crons agendados
- Integracoes: Telegram, Gmail, Slack, Supabase
- 1Password CLI para credenciais

A Ponte = GitHub (repositorio privado)
Ambos puxam e empurram para o mesmo repo.

## Como o Sync Funciona

1. Voce abre o Claude Code
   -> brain-boot.sh roda
   -> git pull (pega o que o agente fez na VPS)
   -> contexto carregado

2. Voce trabalha, toma decisoes
   -> roda /salve
   -> git push
   -> VPS pega na proxima rodada do cron

3. Na VPS, o agente:
   -> executa crons (analytics, reports, content ops)
   -> escreve memory/sessions/YYYY-MM-DD.md
   -> faz push a cada 30min

CHAVE DA ARQUITETURA:
O Git e o protocolo de comunicacao entre os dois.
Nao tem API, nao tem fila — so arquivos commitados. Simples e resiliente.

## Como Montar do Zero

### Passo 1: Criar repo privado no GitHub
Estrutura: memory/ skills/ scripts/ content/

### Passo 2: Configurar o local
git clone https://github.com/SEU_USUARIO/SEU_REPO ~/segundo-cerebro
# Instalar skills, configurar hook SessionStart

### Passo 3: Provisionar VPS
# Opcoes: DigitalOcean, Hetzner, AWS
# Instalar: Claude Code CLI, Node.js, Python, Git, 1Password CLI
# Configurar Tailscale para acesso seguro

### Passo 4: Clonar repo na VPS
git clone https://github.com/SEU_USUARIO/SEU_REPO /root/workspace

### Passo 5: Configurar crons
0 9 * * 1-5 claude --no-interactive "execute /skill-name" >> /var/log/agent.log 2>&1

### Passo 6: Sync bidirecional (a cada 30min na VPS)
*/30 * * * * cd /root/workspace && git pull --rebase && git add . && git commit -m "sync: auto" && git push

### Passo 7: Conectar integracoes
# Gmail via OAuth, Slack via webhook, Telegram via bot token
# Credenciais via 1Password CLI: op read "op://Vault/Item/field"

## Nivel de Dificuldade

Medio / Avancado. Nao recomendado para iniciantes.

## Duvidas Frequentes

Q: So funciona com GitHub?
A: Da para usar outras ferramentas (ex: Obsidian), mas o GitHub e o mais recomendado.

Q: Qual o beneficio?
A: Dois agentes trabalhando: voce usa Claude no PC + OpenClaw na VPS autonomamente ao mesmo tempo.

---

*Proximo: 07-visao-de-futuro.md*