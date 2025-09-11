# Chapter 20: Prioritization

## Overview

Prioritization define como o agente decide o que fazer primeiro sob restrições de tempo, custo e valor. Envolve ordenar tarefas por impacto, urgência, dependências, risco e esforço, mantendo o plano atualizado conforme chegam novas informações.

Critérios comuns (exemplos):

- Valor/Impacto esperado (benefício para o usuário/negócio).
- Urgência/Prazo (SLA, janelas de oportunidade).
- Risco/Severidade (falhas críticas primeiro).
- Esforço/Custo (tamanho, tokens, custo de modelo, chamadas externas).
- Dependências (bloqueadores, ordem lógica).

## Use Cases

- Suporte: enfileirar tickets por severidade e prazo.
- Produto/Engenharia: ordenar backlog por valor vs. esforço.
- Agentes multi-tarefa: decidir o próximo passo quando há múltiplas metas concorrentes.

## Hands-On (conceitual)

- Modelo de dados: `Task(id, title, priority, due, effort, deps, risk, value)`.
- Função de scoring multi-critério (ponderada) + regras de desempate.
- Loop: reavaliar pontuações quando estado/tempo muda; registrar decisões.

## At a Glance

- O que: decidir a ordem de execução.
- Por quê: maximizar valor sob restrições.
- Como: pontuação multi-critério, dependências e reavaliação contínua.
