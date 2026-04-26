# 03 — Reindexacao Forcada (pos-troca de modelo)

## Quando Usar?

Sempre que trocar de modelo (ex: Claude -> GPT). O agente pode apresentar:
- Perda de continuidade
- Menor aderencia ao contexto
- Piora na execucao de tarefas

## Por Que Acontece?

O problema nao e so o modelo novo. Ha desalinhamento entre:
- Indexacao atual da memoria
- Retrieval semantico do novo modelo
- Boot de contexto
- Memoria recente da sessao

## Prompt 1 — Cole no Agente

Quero que voce avalie e aplique um playbook para restaurar o contexto de um agente OpenClaw apos troca de modelo.

Cenario:
Existe um agente que usa memoria persistente + GitHub como segundo cerebro. Apos trocar de modelo, ele passou a demonstrar perda de continuidade, menor aderencia ao contexto e piora na execucao.

Playbook:

1. Reindexacao forcada
   Executar: openclaw memory index --force
   Objetivo: reprocessar todos os arquivos, recriar embeddings do zero, recalibrar espaco vetorial.

2. Warm-up do agente
   Conversar alguns minutos apos a troca, injetar contexto real, relembrar projetos e decisoes.

3. Revisao do boot
   Verificar se o agente le corretamente os arquivos-base no inicio da sessao.

4. Revisao do GitHub como fonte de verdade
   Verificar fluxo: pull -> leitura -> execucao -> validacao -> registro -> push

5. Revisao do flush antes da compactacao
   Verificar se decisoes, licoes, projetos e pendencias estao sendo salvos.

Entregue: diagnostico tecnico claro, checklist de correcao e quick wins imediatos.

---

## Checklist de Correcao

- [ ] openclaw memory index --force
- [ ] Warm-up: conversar 5min injetando contexto atual
- [ ] Verificar boot dos arquivos-base
- [ ] Garantir fluxo GitHub: pull > execucao > push
- [ ] Garantir flush antes da compactacao

## Quick Wins

- Rode o index --force imediatamente apos trocar de modelo
- Faca warm-up ANTES de qualquer tarefa critica
- Revise o boot dos arquivos-base

---

*Proximo: 04-strict-agentic.md*