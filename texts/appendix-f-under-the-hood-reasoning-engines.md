# Appendix F: Under the Hood — Agents’ Reasoning Engines

## Overview

Visão de alto nível sobre como diferentes modelos/assistentes descrevem seu processo de raciocínio (ex.: Gemini, ChatGPT, Grok, Kimi, Claude, DeepSeek), focando em:

- Decomposição do prompt
- Recuperação/síntese de informação
- Estratégias de geração e ajuste
- Limitações e considerações

A meta não é expor cadeias internas proprietárias, mas organizar boas práticas de explicação/estruturação do raciocínio para uso prático em sistemas agentic.

## Padrões frequentes de explicação

- Leitura/entendimento do input
- Ativação de conhecimento relevante
- Seleção de método de raciocínio (CoT, plano, verificação)
- Simulação de passos (quando cabível)
- Formulação de resposta
- Ajuste de clareza/estilo/segurança

## Considerações

- Transparência vs. segurança: cuidado com exposição de cadeias internas.
- Alucinações: valide com evidências/checagens.
- Rastreabilidade: mantenha referências/citações quando for factual.

## Referências

- Consulte o apêndice original para exemplos por modelo e discussões completas.

<!-- nav-prev-next -->
| Anterior | Próximo |
| --- | --- |
| [Appendix E: AI Agents on the CLI (online)](appendix-e-ai-agents-on-the-cli.md) | [Appendix G: Coding Agents](appendix-g-coding-agents.md) |
