# Chapter 7: Multi-Agent

## Multi-Agent Collaboration Pattern Overview

The Multi-Agent Collaboration pattern organiza múltiplos agentes independentes ou semi-independentes para cooperar em direção a um objetivo comum. Cada agente possui um papel definido, metas alinhadas e, possivelmente, ferramentas e bases de conhecimento distintas. O ganho vem da interação e da sinergia entre eles.

Formas comuns de colaboração:

- Sequential Handoffs: agentes passam saídas adiante em um pipeline explícito.
- Parallel Processing: agentes trabalham em partes diferentes simultaneamente e combinam resultados.
- Debate and Consensus: agentes com perspectivas diferentes discutem e chegam a consenso.
- Hierarchical Structures: um agente gerente delega a agentes trabalhadores e integra resultados.
- Expert Teams: especialistas (pesquisa, escrita, revisão, etc.) constroem uma entrega complexa.
- Critic-Reviewer: um grupo cria a saída e outro faz crítica/revisão (políticas, segurança, qualidade), reduzindo alucinações e erros.

## Practical Applications & Use Cases

- Pesquisa e análise complexas: busca, sumarização, identificação de tendências, síntese em relatório.
- Desenvolvimento de software: requisitos, geração de código, testes, documentação, passagem de bastão entre agentes.
- Conteúdo criativo: pesquisa de mercado, copywriting, geração de imagem, agendamento social.
- Finanças: dados de preço, sentimento de notícias, análise técnica, recomendações.
- Suporte ao cliente: triagem por agente de front-line e escalonamento para especialistas.
- Cadeia de suprimentos: agentes por nó otimizam inventário, logística e cronogramas.
- Operações de rede/infra: triagem, diagnóstico e remediação colaborativa entre agentes e ferramentas legadas.

## Inter-relações e estruturas de comunicação

Modelos comuns (resumo):

1. Single Agent: operação autônoma sem coordenação externa; simples, porém limitada.
2. Network: agentes em rede P2P, resilientes, porém com sobrecarga de comunicação.
3. Supervisor: um agente coordena subordinados (hub central e ponto único de falha).
4. Supervisor as a Tool: supervisor provê recursos e análises sem controle rígido.
5. Hierarchical: múltiplos níveis de supervisores para decompor problemas complexos.
6. Custom: arquiteturas híbridas e sob medida conforme restrições/objetivos.

## Hands-On (esboço com CrewAI)

Exemplo conceitual: dupla pesquisador + redator, orquestrados sequencialmente.

```python
from crewai import Agent, Task, Crew, Process
from langchain_google_genai import ChatGoogleGenerativeAI

llm = ChatGoogleGenerativeAI(model="gemini-2.0-flash")

researcher = Agent(
    role='Senior Research Analyst',
    goal='Find and summarize the latest trends in AI.',
    backstory='Experienced analyst focused on key trends and synthesis.',
    verbose=True,
)

writer = Agent(
    role='Technical Content Writer',
    goal='Write a clear blog post based on research findings.',
    backstory='Skilled writer translating complex topics into accessible content.',
    verbose=True,
)

research_task = Task(
    description='Research top 3 emerging AI trends and summarize with sources.',
    expected_output='Summary of top 3 trends with key points and sources.',
    agent=researcher,
)

writing_task = Task(
    description='Write a 500-word post based on the research summary.',
    expected_output='A complete 500-word post.',
    agent=writer,
    context=[research_task],
)

crew = Crew(
    agents=[researcher, writer],
    tasks=[research_task, writing_task],
    process=Process.sequential,
    llm=llm,
)

print(crew.kickoff())
```

## At a Glance

- O que: cooperação entre agentes com papéis e ferramentas diferentes.
- Por quê: modularidade, escalabilidade e robustez para problemas complexos.
- Como: handoffs sequenciais, paralelismo, debate/consenso, hierarquias ou arquiteturas customizadas.

## Referências

- Conceitos detalhados e exemplos adicionais constam no documento original do capítulo Multi-Agent.

<!-- nav-prev-next -->
| Anterior | Próximo |
| --- | --- |
| [Chapter 6: Planning](chapter-06-planning.md) | [Chapter 8: Memory Management](chapter-08-memory-management.md) |
