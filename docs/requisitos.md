# Requisitos

Escopo: **MVP** = compromisso deste semestre · **Depois** = fora do compromisso, ver [visao-produto.md](visao-produto.md).

## Requisitos funcionais

### Catálogo

| ID | Requisito | Escopo |
|---|---|---|
| RF01 | Manter recursos (espaço ou material) com tipo, capacidade, localização, setores responsáveis e usuários que respondem por ele — um recurso pode ser compartilhado entre setores | MVP |
| RF02 | Manter a disponibilidade do recurso: janela de funcionamento e bloqueios | MVP |
| RF03 | Buscar e filtrar recursos por tipo, setor, capacidade e disponibilidade em um período | MVP |
| RF04 | Registrar, para recurso administrado fora do sistema, o caminho oficial de reserva, exibindo-o na busca | MVP |

### Regras de reserva

O comportamento da reserva é definido por **regra**, entidade própria associada ao recurso. Alterar política é operação de administração, não de desenvolvimento.

| ID | Requisito | Escopo |
|---|---|---|
| RF05 | Manter regras de reserva e associá-las a recursos. A regra define: modo de confirmação (automática ou mediante aprovação), permissão exigida para solicitar, antecedência mínima para solicitar, prazo limite para cancelar e precedência entre finalidades | MVP |
| RF06 | Recurso sem regra associada adota a regra padrão do sistema | MVP |
| RF07 | Quando a regra permitir, reserva de maior precedência substitui uma já confirmada: a substituída passa a **cancelada**, com motivo identificando a reserva que a substituiu, e o afetado é notificado | Depois |

### Perfis e permissões

Modelo de **concessão apenas**: não existe negação. O acesso efetivo é a união das permissões vindas dos perfis do usuário com as atribuídas diretamente a ele.

Toda atribuição é o par **(permissão, escopo)** — o escopo é um setor ou todos os setores. É assim que se expressa "aprova no DCC, apenas visualiza no DAC": duas atribuições da mesma permissão em escopos diferentes. Perfis e escopos são acumuláveis por usuário.

| ID | Requisito | Escopo |
|---|---|---|
| RF08 | Autenticar usuário | MVP |
| RF09 | Manter perfis, compondo cada um por um conjunto de permissões | MVP |
| RF10 | Atribuir perfis e permissões avulsas a um usuário, sempre com escopo | MVP |
| RF11 | Consultar o catálogo de permissões existentes no sistema | MVP |
| RF12 | Cada rota e operação é protegida por uma permissão, identificada por **chave estável** independente do caminho da rota | MVP |
| RF13 | Toda consulta filtra os registros pelo escopo do usuário, além de a rota ser protegida | MVP |
| RF14 | A interface exibe apenas os menus e ações correspondentes às permissões do usuário | MVP |

**RF12 guarda a porta; RF13 filtra o conteúdo.** Ter `reserva.aprovar` no escopo de um setor libera a tela da fila, mas a consulta ainda precisa devolver apenas os pedidos daquele setor.

#### Catálogo de permissões

| Chave | Libera |
|---|---|
| `recurso.visualizar` | consultar catálogo e disponibilidade |
| `recurso.gerenciar` | criar, editar e inativar recursos e sua disponibilidade |
| `regra.visualizar` | consultar regras de reserva |
| `regra.gerenciar` | criar e editar regras e associá-las a recursos |
| `reserva.solicitar` | abrir solicitação |
| `reserva.visualizar` | ver solicitações de terceiros |
| `reserva.aprovar` | aprovar e recusar solicitações |
| `reserva.cancelar` | cancelar reserva de terceiros |
| `historico.visualizar` | consultar histórico e auditoria |
| `acesso.gerenciar` | manter perfis e atribuições |

O solicitante sempre visualiza e cancela **as próprias** solicitações, sem permissão específica.

### Solicitação e reserva

A reserva é sempre do **recurso inteiro**, delimitada por um intervalo livre de data e hora, com granularidade de hora. Dois intervalos conflitam quando se sobrepõem; o fim de um pode coincidir com o início do seguinte sem conflito. Estados da solicitação: pendente, aprovada, recusada, cancelada.

| ID | Requisito | Escopo |
|---|---|---|
| RF15 | Abrir solicitação informando recurso, período, finalidade e vínculo, quando houver | MVP |
| RF16 | Avaliar a regra do recurso na abertura, resultando em: confirmação automática, encaminhamento para aprovação, ou recusa informando qual regra foi violada | MVP |
| RF17 | Impedir a confirmação de reserva que se sobreponha a outra no mesmo recurso, exibindo a conflitante | MVP |
| RF18 | Fila de solicitações pendentes para quem aprova, com filtro por setor, recurso, período e status | MVP |
| RF19 | Aprovar ou recusar solicitação, com motivo obrigatório na recusa | MVP |
| RF20 | Cancelar reserva, pelo solicitante ou por quem tem permissão, com motivo e respeitando o prazo da regra | MVP |
| RF21 | Consultar histórico auditável: quem pediu, quem decidiu, quando, sob qual regra, e o que mudou | MVP |

### Notificação

| ID | Requisito | Escopo |
|---|---|---|
| RF22 | Notificar toda mudança de estado ao solicitante e a quem aprova | MVP |
| RF23 | Registrar os envios para auditoria | MVP |
| RF24 | Central de notificações no sistema, com lidas e não lidas | Depois |
| RF25 | Lembrete antes do início da reserva | Depois |
| RF26 | Preferências por usuário: quais eventos notificam e por qual canal | Depois |

### Integração institucional

| ID | Requisito | Escopo |
|---|---|---|
| RF27 | Importar ocupação de sistema externo e refleti-la no catálogo como indisponibilidade | Depois |
| RF28 | Vincular reserva a um registro em sistema institucional, guardando a referência externa | Depois |

### Produto reutilizável

| ID | Requisito | Escopo |
|---|---|---|
| RF29 | Instituição como dimensão de configuração: setores, recursos, perfis, permissões e regras por instituição | Depois |

## Requisitos não funcionais

| ID | Requisito |
|---|---|
| RNF01 | Toda decisão sobre solicitação é registrada com autor, data, motivo e regra aplicada |
| RNF02 | Alteração de regra, perfil ou atribuição é registrada com autor e data |
| RNF03 | A autorização é verificada no servidor a cada requisição. Ocultar menu (RF14) é conveniência de interface, nunca controle de acesso |
| RNF04 | Nenhuma rota sem permissão declarada: rota nova sem vínculo a uma permissão falha na verificação automatizada |
| RNF05 | Alterar política de reserva não exige alteração de código nem novo deploy |
| RNF06 | Coletar o mínimo de dado pessoal necessário à reserva (LGPD) |
| RNF07 | Testes de aceitação escritos contra o comportamento, não contra a estrutura interna |
| RNF08 | Subir o sistema e popular o catálogo inicial deve ser operação simples e documentada |
