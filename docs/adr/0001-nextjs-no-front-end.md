# 0001 — Next.js no front-end

## Status

Aceito — 2026-08-27

## Contexto

O sistema precisa de interface web para o catálogo de recursos, a abertura de solicitações e a fila de aprovação. O Desafio 1 também exige uma pipeline de CI verde, com build e lint reais — não placeholders.

## Decisão

O front-end será **Next.js** com TypeScript, ESLint e Tailwind, em `web/`, usando App Router.

O que pesou:

- Traz roteamento, build e lint já configurados, o que permite ter CI executando verificação de verdade desde o primeiro PR.
- React com TypeScript permite tipar as entidades do domínio e reaproveitá-las entre telas.
- A renderização no servidor permite verificar permissão **antes** de entregar a tela, alinhado ao RNF03: ocultar menu é conveniência, autorização é no servidor.

O CI fixa **Node 24**, a mesma versão usada no ambiente de desenvolvimento.

Esta decisão cobre apenas o front-end. **Onde o back-end vai viver — nas rotas do próprio Next ou em um serviço separado — não está decidido aqui** e será objeto de outro ADR, porque afeta diretamente o percurso de migração entre arquiteturas.

## Consequências

- O projeto passa a depender do Node como ferramenta de build, e das convenções do App Router, que mudam entre versões maiores do Next.
- A pipeline deixa de ser simbólica: um erro de lint ou de tipo barra o PR.
- `web/` isola o front, deixando a raiz do repositório livre para outros módulos conforme a arquitetura evoluir.
- Os arquivos `web/AGENTS.md` e `web/CLAUDE.md` são gerados e reescritos pelo próprio Next a cada `next dev`; ficam versionados para não poluir o diff.
