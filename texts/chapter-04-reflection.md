# Chapter 4: Reflection

## Reflection Pattern Overview

The Reflection pattern introduces a feedback loop in which an agent evaluates its own work (or another agent’s output) and iteratively refines the result. Unlike plain chaining (sequential steps) or routing (branching decisions), reflection adds meta-cognition: execution → critique → refinement → (optional) repetition until a stopping condition is met.

A common design is the Producer–Critic model:

- Producer (or Generator): gera a primeira versão (código, plano, rascunho etc.).
- Critic (ou Reviewer): avalia aderência a requisitos, correção, estilo, qualidade, segurança, conformidade.
- Producer (refinado): incorpora o feedback e reescreve/ajusta.

Com memória (ver Cap. 8), a reflexão torna-se cumulativa, evitando repetição de erros e melhorando consistência em longas conversas. Em conjunto com metas e monitoramento (ver Cap. 11), a reflexão é o motor corretivo que aproxima a execução do objetivo.

## Practical Applications & Use Cases

- Creative Writing: rascunho → crítica de fluidez/clareza/estilo → revisão.
- Code Generation & Debugging: gera código → testa/analisa → corrige e otimiza.
- Complex Problem Solving: avalia passos intermediários, detecta contradições, ajusta rota.
- Summarization: confere completude/precisão contra o original e refina.
- Planning & Strategy: valida viabilidade e restrições antes da execução.
- Conversational Agents: mantém contexto, corrige mal-entendidos e melhora a resposta.

## Hands-On Code Sketch (LangChain)

Exemplo conceitual de laço de reflexão com dois prompts distintos (produtor e crítico). Adapte às suas bibliotecas/modelos:

```python
from langchain_openai import ChatOpenAI
from langchain_core.prompts import ChatPromptTemplate
from langchain_core.output_parsers import StrOutputParser

llm = ChatOpenAI(temperature=0)

producer_prompt = ChatPromptTemplate.from_template(
    """You are a senior technical writer. Draft a concise section about '{topic}'.\n"""
)
critic_prompt = ChatPromptTemplate.from_template(
    """You are a meticulous reviewer. Critique the draft below for clarity, completeness, and correctness.\nDraft:\n{draft}\n"""
)
refine_prompt = ChatPromptTemplate.from_template(
    """Apply the following critique to improve the draft.\nDraft:\n{draft}\nCritique:\n{critique}\nProduce the revised draft only."""
)

produce = producer_prompt | llm | StrOutputParser()
critique = critic_prompt | llm | StrOutputParser()
refine = refine_prompt | llm | StrOutputParser()

def reflect(topic: str, iterations: int = 2) -> str:
    draft = produce.invoke({"topic": topic})
    for _ in range(iterations):
        notes = critique.invoke({"draft": draft})
        draft = refine.invoke({"draft": draft, "critique": notes})
    return draft

print(reflect("Prompt Chaining"))
```

## At a Glance

- O que: ciclo execução → crítica → refinamento (com possível iteração).
- Por quê: elevar qualidade, reduzir erros e alinhar ao objetivo/regras.
- Quando usar: tarefas com requisitos exigentes (exatidão, estilo, conformidade) e problemas de múltiplos passos.

## References

- Conceitos e exemplos adicionais estão distribuídos ao longo do documento original do capítulo.
