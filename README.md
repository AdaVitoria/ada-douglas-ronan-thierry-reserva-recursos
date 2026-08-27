# Reserva de Laboratórios e Equipamentos

Projeto Integrador I (GCC267) — turma 2026/2, 14A.

A reserva de espaços e equipamentos na instituição é descentralizada: cada setor responsável controla os seus recursos do seu jeito, o que impede a consulta unificada da disponibilidade e obriga a checagens pontuais com cada departamento ou secretaria.

Este projeto unifica o ponto de entrada — um catálogo único do que existe, de quem responde por cada recurso e de como pedir. Organizado em três contextos: **Catálogo** (o que existe e está disponível), **Reserva** (quem reservou o quê, quando) e **Notificação** (avisos de confirmação, lembrete e conflito).

## Documentação

- [Visão do produto](docs/visao-produto.md)
- [Requisitos](docs/requisitos.md)
- [Equipe](docs/equipe.md)
- [ADRs](docs/adr/)

## Status

Repositório em fase inicial (Desafio 1) — estrutura, documentação base e pipeline de CI.

O front-end é **Next.js**, em [web/](web/). O CI em [.github/workflows/ci.yml](.github/workflows/ci.yml) roda `npm ci`, `npm run lint` e `npm run build` a cada PR.

## Licença

Distribuído sob a licença MIT — ver [LICENSE](LICENSE).
