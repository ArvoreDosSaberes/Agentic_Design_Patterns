# Chapter 18: Guardrails / Safety Patterns

## Overview

Guardrails definem políticas e verificações que limitam entradas, saídas e ações do agente, reduzindo riscos (conteúdo inseguro, vazamento de dados, ações indevidas) e garantindo conformidade.

Componentes típicos:

- Políticas: regras de segurança/ética/negócio (ex.: PII, violência, autolesão, compliance).
- Classificadores/filtros: bloqueio/redirecionamento por categoria, confiança e contexto.
- Validação estrutural: schemas, Pydantic, formatos e constraints de domínios (ex.: ranges, enums, regex).
- Autorização/controle de ferramentas: whitelists, checagens por contexto/estado, revogação.
- Observabilidade: logging de decisões, porquês e trilha de auditoria.

## Use Cases

- Atendimento: filtrar prompts e ocultar dados sensíveis.
- Codificação: validar outputs (licença, periculosidade, injeção de prompts).
- Ações críticas: exigir dupla confirmação, HITL e limites de escopo.

## Hands-On (conceitual)

- Defina um validador de saída (Pydantic) + função de avaliação de política.
- Se violar: retorne erro estruturado, peça reformulação ou escale para humano.
- Integre num orquestrador (CrewAI/ADK) como etapa antes de efetivar ação/tool.

## At a Glance

- O que: políticas, validações e gates de segurança.
- Por quê: reduzir risco e garantir conformidade.
- Como: filtros/classificadores, schemas, autorização e auditoria.

<!-- nav-prev-next -->
| Anterior | Próximo |
| --- | --- |
| [Chapter 17: Reasoning Techniques](chapter-17-reasoning-techniques.md) | [Chapter 19: Evaluation and Monitoring](chapter-19-evaluation-and-monitoring.md) |
