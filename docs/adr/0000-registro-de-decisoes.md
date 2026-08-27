# 0000 — Registro de decisões arquiteturais (ADR)

## Status

Aceito — 2026-08-27

## Contexto

Ao longo do semestre a equipe vai tomar decisões arquiteturais (escolha de stack, divisão de contextos, estratégia de deploy, etc.) que afetam o projeto como um todo. Sem um registro, essas decisões — e principalmente o *motivo* por trás delas — se perdem, e a equipe (ou quem entra depois) acaba repetindo discussões já resolvidas.

## Decisão

A equipe vai registrar toda decisão arquitetural relevante como um ADR (Architecture Decision Record) em `docs/adr/`, numerado sequencialmente (`0001-titulo-curto.md`, `0002-...`), seguindo o formato:

- **Status** — proposto, aceito, rejeitado ou substituído (indicar por qual ADR), com a data.
- **Contexto** — o problema ou a força que motivou a decisão.
- **Decisão** — o que foi decidido.
- **Consequências** — o que fica mais fácil e o que fica mais difícil por causa disso.

Uma decisão é "arquitetural" quando muda a estrutura do sistema, uma dependência externa, um contrato entre contextos, ou é cara de reverter depois. Escolhas de implementação local não precisam de ADR.

O ADR entra por PR e é aceito na revisão dele, com a mesma aprovação exigida para qualquer mudança. Este documento segue o formato que institui.

## Consequências

- Toda decisão relevante fica rastreável e com o motivo documentado, reduzindo dependência de memória individual.
- Decisões supersedidas não são apagadas: um novo ADR referencia o antigo e marca seu status como substituído.
- Cada migração de arquitetura prevista para o semestre vira um ADR que substitui o anterior. A comparação entre os estilos fica registrada, e não apenas vivida.
- Adiciona um pequeno custo de disciplina: antes de mudar algo estrutural, escrever o ADR.
