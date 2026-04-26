# Guia Completo: Migrando e Turbinando seu OpenClaw

Guia pratico, em PT-BR, para migrar seu agente OpenClaw para qualquer LLM e deixar o setup no maximo de performance.

Organizado e melhorado pelo ecossistema Visual Brain.

Baseado na metodologia de Bruno Okamoto (okjpg).

---

## O Que Voce Encontra Aqui

Este repositorio e dividido em 8 guias praticos:

| Guia | Descricao |
|:---|:---|
| 01-configurar-gpt.md | Como conectar ChatGPT/GPT-5.5 ao OpenClaw |
| 02-melhorar-gpt.md | Bloco SOUL para eliminar respostas corporativas e melhorar performance |
| 03-reindexacao-forcada.md | Playbook completo para restaurar contexto apos troca de modelo |
| 04-strict-agentic.md | Prompt para ativar modo Strict Agentic no OpenClaw 4.24 |
| 05-skill-audit.md | Como revisar e melhorar suas skills para funcionar com qualquer LLM |
| 06-arquitetura-vps.md | Arquitetura avancada: Claude Code local + OpenClaw na VPS via Git |
| 07-visao-de-futuro.md | Analise do mercado de agentes e onde investir seu tempo |
| 08-sugestoes-llm.md | LLMs recomendadas por caso de uso (planejamento, codigo, crons) |

---

## Por Que Isso Foi Criado?

Em abril de 2026, a Anthropic encerrou o suporte ao OpenClaw. Muitos usuarios ficaram perdidos sobre como continuar usando seus agentes.

Este guia responde:
- Como migrar para ChatGPT, Gemini ou outra LLM sem perder contexto
- Como recuperar a performance do agente apos a migracao
- Como montar uma arquitetura resiliente que funciona com qualquer LLM

---

## Para Quem E Este Guia?

- Usuarios do OpenClaw que precisam migrar de LLM
- Pessoas que querem melhorar a performance dos seus agentes
- Devs que querem montar uma arquitetura avancada com VPS + Git sync

Nivel: Intermediario / Avancado

---

## Como Usar

1. Leia primeiro o guia 01 para conectar sua nova LLM
2. Aplique o guia 02 para melhorar a qualidade das respostas
3. Se o agente ficou "confuso" apos a migracao, execute o guia 03
4. Para setups avancados com VPS, consulte o guia 06

---

## Creditos

- Metodologia original: Bruno Okamoto (https://github.com/okjpg)
- Curadoria, traducao e organizacao: Caique Contarini (https://github.com/caiquecontarini)
- Ecossistema: Visual Brain

---

Padrão Visual Brain | PT-BR sem bugs de encoding | Abril 2026