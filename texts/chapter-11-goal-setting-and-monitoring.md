# Chapter 11: Goal Setting and Monitoring

## Overview

O padrão Goal Setting and Monitoring fornece direção e autocontrole ao agente.

- Defina objetivos claros (estado desejado) e mensuráveis (critérios/indicadores).
- Monitore continuamente progresso, ambiente e efeitos das ações.
- Faça correções de rota (replanejamento, escalonamento, ajuste de metas/táticas).

Esse ciclo transforma um agente reativo em um sistema proativo e confiável para tarefas multi-etapas sob condições dinâmicas.

## Practical Applications & Use Cases

- Suporte ao cliente: resolver consulta de cobrança e confirmar desfecho/feedback; escalar se necessário.
- Educação personalizada: adaptar materiais conforme métricas de desempenho do aluno.
- PM assistivo: acompanhar milestone, prazos, recursos; sinalizar riscos e sugerir ações.
- Trading: maximizar ganhos em limites de risco; agir e ajustar conforme indicadores.
- Robótica/AV: transportar com segurança de A→B observando sensores/estado/rota.
- Moderação de conteúdo: monitorar entradas, métricas, e escalonar ambíguos.

## Hands-On (Sketch com LangChain)

Exemplo conceitual de agente que estabelece metas de qualidade e itera geração→avaliação→refino até cumpri-las.

```python
from langchain_openai import ChatOpenAI

llm = ChatOpenAI(model="gpt-4o", temperature=0.3)

def goals_met(feedback_text: str) -> bool:
    resp = llm.invoke(
        """
        Given the feedback below, did the code meet the goals? Answer True or False only.
        Feedback:
        """ + feedback_text
    ).content.strip().lower()
    return resp == "true"
```

A implementação completa inclui utilitários para gerar prompt, revisar código, decidir parada e salvar saída final — seguindo o padrão goal→monitoring→correct.

## At a Glance

- O que: dotar agentes de propósito e mecanismo de autoavaliação.
- Por quê: executar com autonomia, confiabilidade e capacidade de adaptação.
- Regra prática: use quando o agente precisar cumprir objetivo alto nível sem supervisão constante.

## Key Takeaways

- Objetivos devem ser SMART (específicos, mensuráveis, alcançáveis, relevantes, com prazo).
- Defina métricas/sinais de sucesso e loops de feedback.
- No ADK, objetivos via instruções; monitoramento via estado/ferramentas; no geral, use stores e validações.

## References

- SMART Goals Framework: https://en.wikipedia.org/wiki/SMART_criteria
