# Chapter 5: Tool Use

## Tool Use Pattern Overview

O padrão Tool Use (ou Function/Tool Calling) permite que um agente acesse APIs, bancos de dados, serviços externos ou execute código. Em alto nível:

1. Definição do Tool: descreva nome, objetivo e parâmetros aceitos.
2. Decisão do LLM: o modelo escolhe se e quando invocar um tool.
3. Geração da chamada: o LLM retorna o nome do tool e os argumentos (ex.: JSON estruturado).
4. Execução do Tool: a orquestração chama a função/API real com os argumentos.
5. Observação/Resultado: a resposta do tool volta para o agente.
6. Continuação: o LLM usa a saída do tool para responder ao usuário ou decidir próximos passos.

Esse padrão expande a capacidade do LLM além do treinamento, habilitando dados atualizados, cálculos confiáveis, acesso a dados do usuário e ações no mundo digital/físico.

Frameworks como LangChain, LangGraph e Google ADK oferecem suporte robusto à definição e ao uso de tools, frequentemente mapeando para a funcionalidade nativa de "function calling" de LLMs modernos.

## Practical Applications & Use Cases

- Informações em tempo real: consultar clima, cotações, notícias via API.
- Bancos de dados e APIs: checar estoque, status de pedido, disparar pagamentos.
- Cálculos e análise: usar calculadora, bibliotecas de análise ou planilhas.
- Comunicação: enviar e-mails/mensagens por APIs externas.
- Execução de código: rodar trechos em ambiente seguro para inspeção.
- Controle de sistemas: acionar IoT, automações e integrações.

Tool Use transforma um LLM de gerador de texto em um agente capaz de perceber, raciocinar e agir.

## Hands-On (esboço com LangChain)

```python
from langchain_core.tools import tool
from langchain_openai import ChatOpenAI
from langchain.agents import create_tool_calling_agent, AgentExecutor

# Defina um tool simples
@tool
def weather(city: str) -> str:
    """Retorna condições climáticas simuladas para a cidade."""
    return f"Weather in {city}: sunny 26°C (simulado)."

llm = ChatOpenAI(model="gpt-4o-mini", temperature=0)
agent = create_tool_calling_agent(llm, [weather])
executor = AgentExecutor(agent=agent, tools=[weather])

print(executor.invoke({"input": "What's the weather in London?"}))
```

## At a Glance

- O que: acoplamento do LLM com funções/APIs externas.
- Por quê: ultrapassar limites do treinamento e executar ações reais.
- Como: definir tools, permitir decisão do modelo e orquestrar a execução segura.

## References

- Consulte a documentação dos frameworks (LangChain, LangGraph, Google ADK) para padrões de binding e execução.
