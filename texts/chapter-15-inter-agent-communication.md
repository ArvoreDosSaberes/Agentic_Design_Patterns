# Chapter 15: Inter-Agent Communication (A2A)

## Overview

Agent-to-Agent (A2A) define como agentes trocam mensagens, coordenam decisões e compõem capacidades. Estruturas comuns:

- Request/Response síncrono: chamada com resposta imediata (bloca quem chama).
- Streaming: respostas parciais/contínuas para feedback rápido.
- Pub/Sub e eventos: acoplamento fraco, escalável.
- Protocolos e contratos: mensagens tipadas, esquemas, validações.

A2A não substitui MCP (padrão de integração com ferramentas/sistemas). MCP foca agente↔sistemas; A2A foca agente↔agente.

## Use Cases

- Orquestração hierárquica: coordenador delega sub-tarefas e agrega respostas.
- Times especialistas: pesquisa, análise, verificação e síntese em pipeline/parallel.
- Supervisão: agente "overseer" monitora, avalia e intervém.

## Hands-On (conceitual)

- Defina mensagens (schema) e estados observáveis.
- Implemente nós de comunicação (sync/stream) e políticas de retry/timeouts.
- Registre correlações (trace-id) para depuração ponta-a-ponta.

## At a Glance

- O que: padrões de comunicação agente↔agente.
- Por quê: modularidade, paralelismo e robustez.
- Como: contratos claros, telemetria e estratégias de acoplamento.

<!-- nav-prev-next -->
| Anterior | Próximo |
| --- | --- |
| [Chapter 14: Knowledge Retrieval (RAG)](chapter-14-knowledge-retrieval-rag.md) | [Chapter 16: Resource-Aware Optimization](chapter-16-resource-aware-optimization.md) |
