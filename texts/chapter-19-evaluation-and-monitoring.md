# Chapter 19: Evaluation and Monitoring

## Overview

Avaliação e monitoramento fornecem visibilidade contínua da qualidade, custo e confiabilidade do agente. Sem medições, não há melhoria sistemática nem segurança operacional.

Dimensões típicas:

- Qualidade: exatidão factual, cobertura, completude, aderência a instruções/políticas.
- Eficiência: latência ponta-a-ponta, custo por requisição/tarefa, tokens, taxas de acerto por rota/modelo.
- Confiabilidade: taxas de erro, quedas de ferramentas, timeouts, retries, incidentes.
- Experiência: métricas de satisfação, intervenção humana, retrabalho.

## Techniques

- LLM-as-a-Judge com rubricas claras (viés/limitações devem ser mitigados com amostragens humanas).
- Testes de regressão de prompts/workflows.
- Telemetria estruturada: trace-id, logs de decisão, métricas de cada nó/agente.
- Benchmarks orientados a casos de uso (conjuntos de perguntas/etiquetas de ouro).

## Hands-On (conceitual)

- Defina rubricas para avaliação automatizada (pydantic/schemas de saída + critérios).
- Colete métricas de custo/latência por rota/modelo e gere painéis (ex.: Prometheus/Grafana).
- Registre trajetórias (inputs, outputs, ferramentas) para auditoria e reprodução.

## At a Glance

- O que: medir para garantir qualidade, custo e confiabilidade.
- Por quê: base de melhoria contínua e operação segura.
- Como: rubricas, testes, telemetria e painéis.
