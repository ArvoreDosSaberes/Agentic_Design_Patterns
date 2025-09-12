# Chapter 21: Exploration and Discovery

## Overview

Exploration and Discovery foca em como agentes buscam novo conhecimento, geram hipóteses e expandem fronteiras de solução, especialmente quando não há instruções explícitas ou dados previamente vistos.

Padrões típicos:

- Exploração sistemática: varrer espaços de busca (parâmetros, fontes, ferramentas) com limites e heurísticas.
- Geração de hipóteses: propor candidatos, estimar valor/risco e planejar validações.
- Experimentos iterativos: projetar testes, medir resultados, atualizar crenças (Bayes/ablation/DoE).
- Curiosidade guiada por incerteza: priorizar áreas com maior valor informacional esperado.

## Use Cases

- Pesquisa (científica/mercado): levantar perguntas, coletar evidências, validar e sintetizar achados.
- Produto/Inovação: explorar combinações de features/UX/precificação com testes controlados.
- Engenharia: descobrir prompts/pipelines/modelos mais eficientes com search/evolutionary.

## Hands-On (conceitual)

- Defina métrica de valor (ex.: info gain, score de qualidade) e budget (tempo/custo).
- Rode ciclos: `ideate → prioritize → experiment → learn → decide`.
- Registre hipóteses, resultados e mudanças de crença; gere relatório final.

## At a Glance

- O que: expandir conhecimento e encontrar soluções não óbvias.
- Por quê: lidar com incerteza/novidade além do visto em treino.
- Como: hipóteses + experimentos + atualização de crenças sob orçamento.

<!-- nav-prev-next -->
| Anterior | Próximo |
| --- | --- |
| [Chapter 20: Prioritization](chapter-20-prioritization.md) | [Appendix A: Advanced Prompting Techniques](appendix-a-advanced-prompting-techniques.md) |
