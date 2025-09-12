# Appendix A: Advanced Prompting Techniques

## Overview

Técnicas de prompting avançadas para melhorar controle, qualidade e segurança:

- Princípios: instruções claras, limites, exemplos, formato de saída estruturado.
- Zero/One/Few-Shot: de zero até poucos exemplos representativos.
- Estruturação: system/role prompting, delimitadores, contexto explícito.
- Saída estruturada: schemas (ex.: Pydantic) e validação.
- Raciocínio: CoT, self-consistency, tree/graph of thoughts.
- Ação/Interação: ReAct, Tool/Function Calling, RAG.
- Técnicas avançadas: APE (auto prompt engineering), iterações e refinamentos, exemplos negativos, analogias, factored cognition/decomposition, personas, multimodal.

## Exemplo (saída estruturada simplificada)

```python
from pydantic import BaseModel, Field
class User(BaseModel):
    name: str
    email: str
    date_of_birth: str
```

Prompt para o LLM gerar JSON aderente ao schema e depois validar/parsing na aplicação.

## Boas práticas

- Controle formato de saída.
- Especifique persona/tarefa/passo a passo.
- Teste e versiona prompts; experimente sistematicamente.

## Referências

- Ver capítulo original para guia completo, exemplos e referências.

<!-- nav-prev-next -->
| Anterior | Próximo |
| --- | --- |
| [Chapter 21: Exploration and Discovery](chapter-21-exploration-and-discovery.md) | [Appendix B: AI Agentic — From GUI to Real World Environment](appendix-b-ai-agentic-from-gui-to-real-world.md) |
