# Chapter 12: Exception Handling and Recovery

## Overview

O padrão Exception Handling and Recovery estrutura como o agente detecta falhas, aplica fallback, reintenta com estratégia e retorna a execução ao estado saudável.

Princípios:

- Classificar falhas (transitória, lógica, permissão, quota, tool indisponível).
- Isolar efeitos (estado transacional, idempotência, compensações).
- Estratégias de recuperação (retry exponencial com jitter, circuit breaker, mudança de ferramenta/rota, degradação graciosa).
- Telemetria e rastreabilidade (correlações, métricas, logs de decisão).

## Use Cases

- Integração com APIs instáveis (timeouts/intermitências).
- Pipelines longos com passos obrigatórios/alternativos.
- Execução de ferramentas com quotas/limites.

## Hands-On (esboço ADK)

Sequência com três agentes: primário → fallback → apresentador de resultado a partir do `state`.

```python
# Conceito: usar SequentialAgent para garantir ordem e ler/escrever em session.state
# Agente 1 tenta a ferramenta primária e grava state['result'] ou state['error']
# Agente 2 verifica erro e tenta fallback/tool alternativo
# Agente 3 apenas formata a resposta final a partir do state
```

## At a Glance

- O que: detecção, contenção e recuperação de falhas.
- Por quê: elevar confiabilidade e UX sob condições reais.
- Regra: preferir idempotência, retries com limites e plano B explícito.

## References

- Consulte o documento original do capítulo para exemplos detalhados e código ADK.

<!-- nav-prev-next -->
| Anterior | Próximo |
| --- | --- |
| [Chapter 11: Goal Setting and Monitoring](chapter-11-goal-setting-and-monitoring.md) | [Chapter 13: Human-in-the-Loop](chapter-13-human-in-the-loop.md) |
