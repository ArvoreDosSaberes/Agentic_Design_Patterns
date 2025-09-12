# Chapter 10: Model Context Protocol (MCP)

## MCP Pattern Overview

O Model Context Protocol (MCP) é um padrão aberto que padroniza como LLMs/Agentes descobrem e interagem com recursos externos — dados (resources), prompts (templates) e ferramentas (tools) — via uma arquitetura cliente-servidor. Pense como um "adaptador universal" que permite plugar qualquer agente/LLM a serviços e APIs de forma interoperável.

Pontos de atenção:

- MCP é um contrato de interface agentic — a qualidade depende do design das APIs por trás. APIs legadas embrulhadas sem filtros/ordenação podem limitar agentes.
- Dados precisam estar em formatos legíveis pelo agente (ex.: texto/Markdown em vez de PDF bruto).

## MCP vs. Function/Tool Calling

- Function Calling: integração direta e proprietária entre app/LLM e um conjunto fixo de ferramentas (um-para-um, acoplado).
- MCP: protocolo aberto para descoberta, comunicação e uso de ferramentas/recursos de forma federada e reutilizável (cliente-servidor, descoberta dinâmica).

Use Function Calling para apps simples com poucas funções. Use MCP quando precisar de interoperabilidade, descoberta dinâmica e composição de múltiplos serviços.

## Practical Applications & Use Cases

- Integração com bancos de dados (ex.: BigQuery) via toolboxes MCP.
- Orquestração de mídias generativas (Imagen, Veo, Chirp 3 HD, Lyria).
- Chamadas a APIs externas padronizadas (clima, bolsa, CRM, e-mail).
- Extração baseada em raciocínio (respostas precisas a partir de trechos).
- Exposição de ferramentas internas como servidores MCP (ex.: FastMCP).
- Camada padronizada de comunicação LLM↔Aplicações.
- Orquestração de fluxos multi-etapas combinando várias ferramentas.
- Controle de dispositivos IoT por comandos em linguagem natural.
- Automação de finanças com interação a dados/plataformas/relatórios.

## Hands-On (ADK) — Cliente conectando a um servidor MCP

Exemplo conceitual: configurar um agente ADK com `MCPToolset` para acessar ferramentas expostas por um servidor MCP.

```python
from google.adk.agents import LlmAgent
from google.adk.tools.mcp_tool.mcp_toolset import MCPToolset, HttpServerParameters

FASTMCP_SERVER_URL = "http://localhost:8000"
root_agent = LlmAgent(
    model='gemini-2.0-flash',
    name='fastmcp_greeter_agent',
    instruction='You are a friendly assistant. Use the "greet" tool.',
    tools=[
        MCPToolset(
            connection_params=HttpServerParameters(url=FASTMCP_SERVER_URL),
            tool_filter=['greet']
        )
    ],
)
```

Para interação com sistema de arquivos, use `MCPToolset` com `StdioServerParameters` apontando para um diretório raiz absoluto que o servidor MCP poderá acessar.

## At a Glance

- O que: padrão aberto para LLMs descobrirem recursos/prompts/tools e interagirem via cliente-servidor.
- Por quê: reduzir integrações ad-hoc, aumentar interoperabilidade e reuso.
- Quando: sistemas complexos e escaláveis que exigem integração dinâmica de vários serviços.

## Key Takeaways

- MCP padroniza a comunicação LLM↔sistemas externos.
- ADK suporta consumir e expor ferramentas via MCP; FastMCP acelera construção de servidores.
- Útil para dados em tempo real, ações externas, automações e mídia generativa.

## References

- Documentação MCP (ADK): https://google.github.io/adk-docs/mcp/
- FastMCP: https://github.com/jlowin/fastmcp
- MCP Tools for Genmedia: https://google.github.io/adk-docs/mcp/#mcp-servers-for-google-cloud-genmedia
- MCP Databases Toolbox: https://google.github.io/adk-docs/mcp/databases/

<!-- nav-prev-next -->
| Anterior | Próximo |
| --- | --- |
| [Chapter 9: Learning and Adaptation](chapter-09-learning-and-adaptation.md) | [Chapter 11: Goal Setting and Monitoring](chapter-11-goal-setting-and-monitoring.md) |
