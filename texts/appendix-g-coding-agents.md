# Appendix G: Coding Agents

## Overview

Padrões e práticas para agentes de codificação que atuam como membros de equipe: análise de requisitos, planejamento, edição de código, testes, documentação e PRs.

## Core Components

- Entendimento de tarefa: objetivo, constraints e critérios de aceitação.
- Operações de código: leitura, busca, edição segura (diff), formatação e lint.
- Execução/validação: testes, builds, checagens estáticas e dinâmicas.
- Versionamento/PR: commits atômicos, mensagens claras, descrição e checklist.
- Segurança: escopo de diretórios, bloqueio de ações perigosas, revisão humana.

## Princípios da equipe aumentada

- Transparência: logs de decisão e mudanças rastreáveis.
- Reprodutibilidade: passos determinísticos para chegar ao resultado.
- Colaboração: handoffs entre agentes (pesquisa → implementação → revisão).
- Padrões de qualidade: linters, testes, cobertura mínima e guidelines do repo.

## Setup Checklist (conceitual)

- Ambiente e credenciais mínimas.
- Ferramentas de análise/edição (grep, rg, formatters, linters, test runners).
- Políticas de guardrail (arquivos proibidos, comandos vetados, validações).

## Conclusão

Agentes de código eficazes combinam entendimento de requisitos, execução segura e ciclos de verificação, integrando-se a fluxos de engenharia modernos.
