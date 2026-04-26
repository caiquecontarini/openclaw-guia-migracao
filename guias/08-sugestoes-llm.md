# 08 — Sugestoes de LLMs por Caso de Uso

## Configuracao Recomendada (Abril 2026)

| Caso de Uso | LLM Recomendada |
|:---|:---|
| Planejamento estratégico | Claude Opus (API) |
| Dia a dia / produtividade | Kimi 2.5, Mimo.v2 ou Gemini 3.0 Preview |
| Codigo | GLM ou GPT 5.4 |
| Crons automaticos | Kimi/Mimo e GPT 5.1 Mini (se usar ChatGPT) |

## Economia de Tokens

Criar uma estrutura organizada de planejamento vs execucao vs codigo vs crons da para economizar bastante.

Exemplo de separacao:
- Planejamento: use o modelo mais inteligente (Opus)
- Dia a dia: use modelos intermediarios e mais baratos
- Codigo: modelos especializados (GLM, GPT 5.4)
- Crons: modelos rapidos e baratos (Mini, Flash)

## Regra Geral

Nao use o modelo mais caro para tudo. Segmente por tipo de tarefa.
O agente mais eficiente nao e o mais caro — e o mais bem organizado.