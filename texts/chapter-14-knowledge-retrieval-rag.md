# Chapter 14: Knowledge Retrieval (RAG)

## Overview

RAG (Retrieval-Augmented Generation) combina busca semântica em bases de conhecimento com geração por LLM, reduzindo alucinações e trazendo fatos atualizados. Componentes típicos:

- Ingestão: carregar, chunkar e indexar documentos (vetorização, metadados).
- Recuperação: top-k por similaridade/filtragem.
- Compressão/seleção: re-rankeamento/condensação opcional.
- Geração: prompt com contexto recuperado + políticas de citação.

## Use Cases

- QA empresarial, suporte e documentação técnica.
- Pesquisa e compliance (com trilha de evidências).
- Assistentes com conhecimento de produto/processos.

## Hands-On (esboço)

LangChain/LangGraph:

```python
# 1) carregar dados, 2) chunkar, 3) embedar e armazenar (ex.: Weaviate/FAISS),
# 4) criar retriever e 5) montar cadeia RAG com LLM.
```

ADK:

```python
# VertexAiRagMemoryService para busca persistente/semântica em corpora do Vertex.
```

## At a Glance

- O que: gerar com base em contexto recuperado.
- Por quê: factualidade e rastreabilidade.
- Quando: respostas ancoradas em conteúdo corporativo/externo.

## References

- Ver o capítulo original para exemplos completos de código com Vertex RAG e LangChain/LangGraph.

<!-- nav-prev-next -->
| Anterior | Próximo |
| --- | --- |
| [Chapter 13: Human-in-the-Loop](chapter-13-human-in-the-loop.md) | [Chapter 15: Inter-Agent Communication (A2A)](chapter-15-inter-agent-communication.md) |
