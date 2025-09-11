# Chapter 17: Reasoning Techniques

## Overview

Técnicas de raciocínio ajudam agentes a estruturar pensamento, reduzir erros e aumentar a explicabilidade. Padrões comuns:

- Chain-of-Thought (CoT): decompor passo a passo.
- Self-Consistency: amostrar múltiplas cadeias e escolher consenso.
- Tree/Graph of Thoughts: explorar alternativas em árvore/grafo.
- Retrieval-augmented reasoning: intercalar buscas de evidência.
- Debate/Reflection: agentes discutem/criticam e refinam.
- Program-aided reasoning: usar ferramentas estruturadas (código, calculadoras, solvers).

## Use Cases

- Pesquisa web guiada por plano (buscar → avaliar → refinar → sintetizar).
- QA complexa com checagem de fontes e cotações.
- Análise comparativa: gerar critérios, pontuar, justificar.

## Hands-On (conceitual LangGraph)

Fluxo típico: `plan → search (paralelo) → reflect → evaluate → finalize` com condicionais para repetir busca se qualidade < limiar.

## At a Glance

- O que: estruturas e heurísticas para pensar melhor.
- Por quê: precisão, robustez e transparência.
- Como: CoT, self-consistency, árvores/grafos, reflexão e ferramentas.
