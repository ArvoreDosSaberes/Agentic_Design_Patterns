# Chapter 13: Human-in-the-Loop

## Overview

Human-in-the-Loop (HITL) introduz checkpoints humanos em fluxos agentic para decisões, validações, aprovações ou intervenções quando:

- Risco/impacto é alto (financeiro, legal, segurança).
- Confiança do modelo é baixa ou ambiguidade é alta.
- Políticas exigem supervisão/dupla checagem.

## Practical Applications & Use Cases

- Suporte: escalar tickets ambíguos a especialistas.
- Medial/legal: revisão humana obrigatória antes de ação.
- Dados: validação/rotulagem humana para re-treino.

## Hands-On (esboço)

- Estado armazena `needs_human_review=True` e contexto do caso.
- Tarefa "handoff" cria item em fila humana com metadados.
- Após decisão humana, agente retoma do estado e conclui.

## At a Glance

- O que: inserir humanos como verificadores/aprovadores.
- Por quê: aumentar segurança, qualidade e conformidade.
- Como: ramos condicionais, filas, estados e SLAs de retorno.

## References

- Ver documento original para exemplos detalhados de código/ADK.

<!-- nav-prev-next -->
| Anterior | Próximo |
| --- | --- |
| [Chapter 12: Exception Handling and Recovery](chapter-12-exception-handling-and-recovery.md) | [Chapter 14: Knowledge Retrieval (RAG)](chapter-14-knowledge-retrieval-rag.md) |
