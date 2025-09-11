# Frequently Asked Questions (FAQ) — Agentic Design Patterns

- O que é um sistema agentic?
  Sistemas que percebem, raciocinam e agem para atingir objetivos definidos, integrando padrões como chaining, routing, parallelization, planning e tool use.

- Quando usar RAG vs. memória curta?
  RAG para conhecimento factual persistente; memória curta (state/session) para contexto imediato da conversa.

- MCP substitui function calling?
  Não. Function calling resolve integrações específicas e diretas. MCP padroniza descoberta/uso de ferramentas e dados entre múltiplos clientes/servidores.

- Como evitar alucinações?
  Use RAG, validações (schemas), guardrails, raciocínio estruturado e checagens com evidências/citações.

- Como começar com multi-agentes?
  Defina papéis claros, contratos de mensagens, telemetria e um coordenador simples. Evolua para paralelismo/debate conforme necessidade.

- Como medir qualidade?
  Rubricas (LLM-as-a-judge + amostragens humanas), testes de regressão de prompts e métricas por rota/modelo.
