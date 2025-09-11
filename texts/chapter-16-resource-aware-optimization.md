# Chapter 16: Resource-Aware Optimization

## Overview

Resource-Aware Optimization trata de escolher modelos, ferramentas e caminhos de execução considerando custo, latência e qualidade. O agente pode:

- Alternar entre modelos (ex.: Flash vs. Pro) por tamanho/complexidade da tarefa.
- Roteamento dinâmico por custo/limite de token/tempo disponível.
- Cache, batch e deduplicação de chamadas.
- Timeouts, cancelamentos e backpressure para estabilidade.

## Use Cases

- Atendimento escalável: perguntas simples → modelo barato/rápido; casos complexos → modelo potente.
- Pesquisa: coarse filtering barato + re-rankeamento caro só no top-k.
- Orquestração: paralelizar I/O; serializar passos críticos; aplicar cotas.

## Hands-On (conceitual)

- Classificador rápido decide "simple" vs "complex" e escolhe o modelo.
- Ferramenta de busca limitada por orçamento (n resultados, janelas temporais).
- Métricas por rota/modelo para políticas adaptativas.

## At a Glance

- O que: otimização de custo/latência/qualidade.
- Por quê: viabilizar operação eficiente e previsível.
- Como: roteamento por políticas, cache, cotas e instrumentação.
