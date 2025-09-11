# Chapter 6: Planning

## Planning Pattern Overview

A Planning agent recebe um objetivo (o "o quê") e descobre o "como" — isto é, elabora um plano de ações para sair do estado inicial e atingir o estado final, adaptando-se a restrições e mudanças de contexto.

Características-chave:

- Descoberta do caminho: o plano não é pré-definido; é gerado conforme o objetivo e o contexto.
- Adaptabilidade: o agente revisa o plano frente a novos fatos (ex.: local indisponível) e propõe alternativas.
- Trade-off: quando o processo é bem conhecido e determinístico, um fluxo fixo é preferível a um planejador dinâmico.

Em essência, o padrão Planning move o agente de ações meramente reativas para um comportamento orientado a objetivos, decompondo uma meta em passos interdependentes executáveis.

## Practical Applications & Use Cases

- Automação de processos: onboarding de funcionário, com criação de contas, treinamentos e coordenação entre áreas.
- Robótica e navegação: planejar trajetória entre estados com otimização (tempo, energia) respeitando restrições (obstáculos, regras).
- Síntese estruturada de informação: gerar relatório com fases de coleta, sumarização, estruturação e refinamento.
- Suporte ao cliente: diagnosticar, aplicar solução, validar e escalar conforme necessário.

## Hands-on code (Crew AI) — Esboço

Abaixo um sketch simplificado inspirado no exemplo do documento, mostrando um agente que planeja e executa uma tarefa multi-etapas.

```python
from crewai import Agent, Task, Crew, Process
from langchain_openai import ChatOpenAI

# Modelo de linguagem
llm = ChatOpenAI(model="gpt-4-turbo")

# Agente planejador-executor
planner = Agent(
    role="Planner",
    goal=(
        "Dado um objetivo complexo, elabore um plano multi-etapas com dependências,"
        " valide restrições e execute cada passo na ordem correta."
    ),
    backstory="Especialista em orquestrar tarefas complexas com replanejamento quando necessário.",
    llm=llm,
)

# Tarefa com saída estruturada
task = Task(
    description=(
        "Organizar um offsite de equipe com orçamento, datas e locais."
        " Gere um plano, valide disponibilidade e proponha alternativas se necessário."
    ),
    expected_output=(
        "Plano com etapas, dependências, riscos, validações e próximo passo acionável."
    ),
    agent=planner,
)

crew = Crew(agents=[planner], tasks=[task], process=Process.sequential)
result = crew.kickoff()
print(result)
```

## At a Glance

- O que: transformar um objetivo em um plano executável e adaptável.
- Por quê: lidar com ambientes dinâmicos e múltiplas restrições.
- Quando: quando o "como" precisa ser descoberto; caso contrário, prefira fluxos fixos.

## Referências

- Seções e exemplos detalhados no documento original do capítulo Planning.
