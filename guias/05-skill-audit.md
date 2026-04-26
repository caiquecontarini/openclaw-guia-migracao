# 05 — Revisar Skills com Skill Audit

## Por Que Fazer Isso?

Skills criadas com o Claude podem nao funcionar bem com o GPT ou Gemini. O Skill Audit analisa cada SKILL.md e sugere melhorias para funcionar com qualquer LLM.

## Como Usar

1. Instale a skill do Skill Audit no seu agente
2. Peca ao agente: "Audite todas as minhas skills"
3. O agente vai retornar um plano de melhoria

## Repositorios

- Original: https://github.com/okjpg/skill-audit
- Fork melhorado: https://github.com/caiquecontarini/skill-audit

## Os 10 Criterios de Auditoria

1. Gatilho claro e definido
2. Frontmatter YAML valido
3. Instrucoes sem ambiguidade
4. Compatibilidade com multiplas LLMs
5. Sem exposicao de dados sensiveis
6. Tamanho otimizado para o contexto
7. Formato de saida definido
8. Dependencias documentadas
9. Exemplos praticos presentes
10. Comportamento de fallback definido

---

*Proximo: 06-arquitetura-vps.md*