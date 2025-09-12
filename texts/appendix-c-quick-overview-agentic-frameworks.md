# Appendix C: Quick Overview of Agentic Frameworks

## Overview

Panorama resumido de frameworks para agentes e orquestração.

## LangChain

- Foco em compor cadeias/graphs com LCEL e LangGraph.
- Componentes: modelos, prompts, memórias, ferramentas, retrievers.
- Quando usar: prototipagem rápida, RAG, agentes com fluxo explícito.

## LangGraph

- Extensão "stateful" para fluxos cíclicos/condicionais com checkpoint e store.
- Ideal para agentes com memória de longo prazo e topologias complexas.

## Google ADK (Agent Development Kit)

- Agentes, ferramentas, sessões/estado/memória; integração com Vertex (RAG/Memory Bank).
- Suporte a MCP; execução em web UI e primitives para paralelismo/seqüência.

## Qual escolher?

- Fluxo linear/cadeias simples → LangChain.
- Estado rico, loops e stores → LangGraph.
- Integração Google/Vertex, execução/observabilidade nativas → ADK.

## Referências

- Consulte o apêndice original para snippets ilustrativos e comparativos.

<!-- nav-prev-next -->
| Anterior | Próximo |
| --- | --- |
| [Appendix B: AI Agentic — From GUI to Real World Environment](appendix-b-ai-agentic-from-gui-to-real-world.md) | [Appendix D: Building an Agent with AgentSpace (online)](appendix-d-building-agent-with-agentspace.md) |
