# Chapter 9: Learning and Adaptation

## Overview

Agentes aprendem e se adaptam alterando conhecimento, estratégia e ações com base em dados e experiências. Entre técnicas comuns:

- Reinforcement Learning (RL): estratégia otimizada por recompensas/penalidades (ex.: PPO com clipping para estabilidade).
- Supervised Learning: mapeia entradas para saídas rotuladas para decisões e classificação.
- Unsupervised Learning: descobre padrões e estrutura em dados sem rótulo.
- Few/Zero-Shot com LLMs: adaptação rápida por instruções e poucos exemplos.
- Online Learning: atualização contínua com dados em fluxo.
- Memory-Based Learning: aproveita memórias semânticas/episódicas/procedurais para ajustar decisões.

## The Big Picture

- PPO: atualiza políticas com passo limitado (trust region/clipping), garantindo estabilidade.
- DPO: alinha LLMs diretamente a preferências humanas, sem modelo de recompensa separado; aumenta probabilidade das respostas preferidas.

## Practical Applications & Use Cases

- Assistentes personalizados: refinam protocolo de interação ao longo do tempo.
- Trading bots: ajustam parâmetros com dados de mercado em tempo real.
- Apps orientados a uso: adaptam UI/funcionalidades ao comportamento.
- Robótica/autônomos: integram sensores e histórico para navegação segura.
- Fraude: refinam modelos conforme surgem novos padrões.
- Recomendação: aprendem preferências para maior relevância.
- Knowledge Base Learning com RAG: mantêm base dinâmica de problemas/soluções (ver Cap. 14) e reutilizam estratégias bem-sucedidas.

## Case Study — SICA (Self-Improving Coding Agent)

SICA demonstra autoevolução: o agente escolhe uma versão anterior com melhor pontuação, propõe melhorias e modifica seu próprio código, avalia em benchmarks e registra no histórico, repetindo o ciclo. Evoluiu de sobrescrita simples para "Smart Editor" e depois "Diff-Enhanced Smart Editor" com minimização sensível a contexto (AST). Criou localizadores de símbolos baseados em AST (e híbridos) para navegação eficiente, com supervisão assíncrona para evitar loops/estagnação.

Organização de contexto: prompts de sistema (objetivos/regras), documentação de ferramentas/subagentes, instruções, enunciado do problema, arquivos abertos/mapa do diretório e mensagens/razões passo-a-passo — reduzindo custo/latência e melhorando eficácia.

## At a Glance

- O que: agentes atuam em ambientes dinâmicos e imprevisíveis; precisam aprender para otimizar estratégias e personalizar.
- Por quê: integrar mecanismos de aprendizado/autoajuste transforma agentes estáticos em sistemas evolutivos.
- Regra prática: use quando houver variabilidade, necessidade de personalização e enfrentamento de situações novas.

## Key Takeaways

- Adaptação é a mudança observável derivada do aprendizado.
- SICA ilustra autoedição guiada por desempenho histórico (ferramentas como Smart Editor e AST Symbol Locator).
- Subagentes e um "overseer" ajudam a escalar e manter segurança/controle.
- Estruturar a janela de contexto do LLM é crítico para eficiência.

## References

- Consulte o documento original para detalhes e figuras (SICA, AlphaEvolve) e bibliografia associada.
