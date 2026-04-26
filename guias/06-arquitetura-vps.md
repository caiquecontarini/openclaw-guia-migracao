# 06 - Arquitetura Avancada: Claude Code Local + OpenClaw na VPS

Esta e a arquitetura de dois agentes se sincronizando em tempo real via Git.
Baseada no setup real de Bruno Okamoto (Amora-COS).

---

## Diagrama da Arquitetura

Local (Mac/PC):
- Claude Code rodando no terminal
- Clone do repositorio em ~/segundo-cerebro/amora-cos
- Skills: ~/.claude/skills/ (/cerebro, /rotina, /salve)
- Hook SessionStart: toda vez que abre o Claude Code, roda git pull automaticamente

VPS (OpenClaw):
- Servidor Linux com acesso via ssh openclaw (usando Tailscale para VPN)
- Mesmo repositorio clonado em /root/.openclaw/workspace-amora-cos/
- Agente rodando de forma autonoma com ~60 crons agendados
- Integracoes ativas: Telegram, Slack, Gmail, Buffer, Stripe, Supabase
- 1Password CLI para credenciais

A Ponte:
- Repositorio privado no GitHub
- Ambos os lados puxam e empurram para o mesmo repo
- Local: git pull no boot + git push no /salve
- VPS: cron a cada 30min fazendo git add . && git commit && git push

---

## O Que Roda Onde

| Atividade | Local | VPS |
|:---|:---:|:---:|
| Decisoes estrategicas | X | |
| Geracao de conteudo interativo | X | |
| Analise e planejamento | X | |
| Crons automaticos | | X |
| Relatorios agendados | | X |
| Processamento de dados | | X |
| Sessoes de memoria | | X |
| Integracoes (Gmail, Slack, Telegram) | | X |

---

## Como o Sync Funciona na Pratica

1. Voce abre o Claude Code
   -> brain-boot.sh roda
   -> git pull (pega o que o agente fez na VPS durante a noite)
   -> contexto carregado

2. Voce trabalha, toma decisoes, atualiza arquivos
   -> roda /salve
   -> git push
   -> VPS pega na proxima rodada do cron (a cada 30min)

3. Na VPS, o agente autonomamente:
   -> executa crons (analytics, reports, content ops)
   -> escreve memory/sessions/YYYY-MM-DD.md
   -> faz push a cada 30min

CHAVE DA ARQUITETURA:
Os arquivos sao a memoria compartilhada.
Nenhum dos dois lados "envia mensagem" para o outro.
A comunicacao e via Git. Simples e resiliente.

---

## Como Montar do Zero

Mande este bloco para o seu Claude Code e peca para ele executar.

### Passo 1 - Criar o repositorio privado no GitHub
Estrutura de pastas: memory/ skills/ scripts/ content/
(Mesma ensinada no mini-curso OpenClaw)

### Passo 2 - Configurar o local
Clone o repo em ~/segundo-cerebro.
Configure a variavel SECOND_BRAIN_PATH.
Instale as skills (/cerebro, /rotina, /salve).
Configure o hook SessionStart com brain-boot.sh.

Referencia: Segundo-cerebro-kit (disponivel no Google Drive do curso)

### Passo 3 - Provisionar a VPS
Opcoes: DigitalOcean, Hetzner, AWS, qualquer servidor Linux.
Instalar: Claude Code CLI, Node.js, Python, Git, 1Password CLI.
Configure Tailscale para acesso seguro: ssh seuservidor

### Passo 4 - Clonar o repo na VPS
git clone https://github.com/SEU_USUARIO/SEU_REPO.git /root/workspace

### Passo 5 - Configurar o agente autonomo na VPS
Crie o SOUL.md (identidade do agente), CLAUDE.md (contexto), e os primeiros skills.
Configure crons via crontab -e:

0 9 * * 1-5 claude --no-interactive "execute /skill-name" >> /var/log/agent.log 2>&1

### Passo 6 - Configurar o sync bidirecional (cron a cada 30min na VPS)
*/30 * * * * cd /root/workspace && git pull --rebase && git add . && git commit -m "sync: auto" && git push

### Passo 7 - Conectar integracoes no VPS
- Gmail via OAuth
- Slack via webhook
- Telegram via bot token
- Todas as credenciais via 1Password CLI: op read "op://Vault/Item/field"

---

## O Que Torna Esse Setup Poderoso

Voce tem dois modos de uso simultaneos:

INTERATIVO (local):
Voce fala com o Claude Code diretamente, toma decisoes, gera conteudo, faz analises.
O contexto esta todo ali.

AUTONOMO (VPS):
Enquanto voce dorme, o agente roda crons, envia relatorios, processa dados,
mantem o segundo cerebro atualizado.
Na manha seguinte voce abre o Claude Code e o git pull traz tudo que o agente fez.

---

## Duvidas Frequentes

Q: Nao entendi nada. Por onde comecar?
A: Jogue este texto + o KIT do Google Drive para o seu agente e peca para ele montar.

Q: Qual o beneficio de fazer isso?
A: Dois agentes trabalhando ao mesmo tempo: voce usa Claude no PC + OpenClaw na VPS autonomamente.

Q: Qual o nivel de dificuldade?
A: Medio/Avancado. Se voce esta iniciando esta jornada, nao recomendo este caminho ainda.

Q: So funciona com GitHub?
A: Da para usar outras ferramentas (ex: Obsidian), mas o GitHub e o mais recomendado.

---

*Proximo: 07-visao-de-futuro.md*