# Chapter 8: Memory Management

## Overview

Memory management é fundamental para agentes manterem contexto, aprenderem com interações e personalizarem respostas. Em geral há dois níveis:

- Curto prazo (Session/State): contexto da conversa atual, eventos e dados temporários usados pelo fluxo.
- Longo prazo (Memory/Knowledge): repositório pesquisável e persistente de fatos, preferências e experiências passadas (ex.: RAG/Vector DB).

No Google ADK:

- `Session`: trilha de conversa com `events` e `state` (dados temporários).
- `SessionService`: gerencia ciclo de vida da sessão.
- `MemoryService`: armazena e busca conhecimento de longo prazo (ex.: `VertexAiRagMemoryService`).

Em LangChain/LangGraph:

- Memória de conversa (ex.: `ConversationBufferMemory`, `ChatMessageHistory`).
- Lembretes de longo prazo em stores/"namespaces" (ex.: `InMemoryStore` com embeddings para busca semântica).

## Practical Applications & Use Cases

- Chatbots: manter contexto e preferências para respostas coerentes e personalizadas.
- Agentes de tarefas: rastrear progresso/estado em fluxos multi-etapas.
- Personalização: recuperar preferências e histórico do usuário.
- Aprendizado contínuo: registrar sucessos/falhas e ajustar comportamento.
- RAG: buscar conhecimento factual relevante durante a resposta.
- Sistemas autônomos: combinar memória de curto prazo (situação) e longo prazo (mapas/regras).

## Hands-On (ADK) — Estado e Ferramenta de Atualização

```python
from google.adk.agents import LlmAgent
from google.adk.sessions import InMemorySessionService
from google.adk.runners import Runner
from google.genai.types import Content, Part

# Agente com output_key grava no state
agent = LlmAgent(
    name="Greeter",
    model="gemini-2.0-flash",
    instruction="Generate a short, friendly greeting.",
    output_key="last_greeting",
)

session_service = InMemorySessionService()
runner = Runner(agent=agent, app_name="state_app", session_service=session_service)
session = session_service.create_session("state_app", "user1", "session1")

for event in runner.run(user_id="user1", session_id="session1", new_message=Content(parts=[Part(text="Hello")])):
    pass
print("State:", session_service.get_session("state_app", "user1", "session1").state)
```

Atualização de `state` via Tool (recomendado):

```python
import time
from google.adk.tools.tool_context import ToolContext, InvocationContext
from google.adk.sessions import InMemorySessionService

def log_user_login(tool_context: ToolContext) -> dict:
    state = tool_context.state
    state["user:login_count"] = state.get("user:login_count", 0) + 1
    state["user:last_login_ts"] = time.time()
    state["task_status"] = "active"
    state["temp:validation_needed"] = True
    return {"status": "ok"}

svc = InMemorySessionService()
session = svc.create_session("app", "u", "s", state={"user:login_count": 0})
ctx = ToolContext(invocation_context=InvocationContext(app_name="app", user_id="u", session_id="s", session=session, session_service=svc))
log_user_login(ctx)
print(svc.get_session("app", "u", "s").state)
```

## Hands-On (LangChain/LangGraph) — Conversa e Store

```python
from langchain.memory import ConversationBufferMemory
from langchain.chains import LLMChain
from langchain.prompts import PromptTemplate
from langchain_openai import OpenAI

llm = OpenAI(temperature=0)
prompt = PromptTemplate.from_template(
    """You are a helpful assistant.\nHistory:\n{history}\nQ: {question}\nA:"""
)
memory = ConversationBufferMemory(memory_key="history")
chain = LLMChain(llm=llm, prompt=prompt, memory=memory)
print(chain.predict(question="Hi"))
print(chain.predict(question="What did I say?"))
```

Armazenamento de longo prazo (conceitual): `InMemoryStore` com embeddings por `namespace` para put/get/search.

## Vertex Memory Bank (ADK)

Serviço gerenciado do Vertex AI Agent Engine para memórias persistentes do usuário, com extração automática e recuperação por similaridade.

## Key Takeaways

- Separe curto prazo (Session/State) de longo prazo (Memory/RAG).
- Atualize `state` de forma estruturada (ex.: `output_key`, `EventActions.state_delta` ou ferramentas ADK).
- Para conversas, `ConversationBufferMemory` simplifica; para longo prazo, use stores + embeddings.
- Memory Bank (Vertex) oferece persistência e recall automáticos.

<!-- nav-prev-next -->
| Anterior | Próximo |
| --- | --- |
| [Chapter 7: Multi-Agent](chapter-07-multi-agent.md) | [Chapter 9: Learning and Adaptation](chapter-09-learning-and-adaptation.md) |
