\# Desafio técnico — Git e GitHub Actions com fluxo por ambiente



\## Objetivo



Demonstrar o uso de Git, controle de branches, Pull Requests e GitHub Actions,

simulando um fluxo de desenvolvimento.



\## Fluxo de branches



O projeto utiliza três branches principais:



\- `develop` — ambiente de desenvolvimento.

\- `staging` — ambiente de homologação.

\- `main` — ambiente de produção.



\### Branches de feature



Branches de funcionalidade podem ser criadas a partir do fluxo de desenvolvimento.



Exemplo:



`feature/exemplo` → `develop`



Branches de feature podem abrir Pull Requests para `develop`.



\### Branches de release



Para `staging` e `main`, a branch de origem deve seguir obrigatoriamente o formato:



`release/x.x.x.x`



Exemplos válidos:



\- `release/1.0.0.0`

\- `release/2.1.3.4`



Exemplo de fluxo:



`release/1.0.0.0` → `staging`



`release/1.0.0.0` → `main`



Branches como `release/teste` não são aceitas.



\## Regras de proteção



As branches `develop`, `staging` e `main` possuem proteção configurada no GitHub.



As regras incluem:



\- Pull Request obrigatório antes do merge.

\- Push direto nas branches principais bloqueado.

\- Force push bloqueado.

\- O check do GitHub Actions `validate` deve passar antes do merge.



\### Regras de origem



| Branch de destino | Branch de origem permitida |

|---|---|

| `develop` | Qualquer branch |

| `staging` | `release/x.x.x.x` |

| `main` | `release/x.x.x.x` |



\## Validação de Pull Requests



O workflow `validate-pr.yml` é executado quando um Pull Request é:



\- aberto;

\- reaberto;

\- atualizado com novos commits.



O workflow identifica:



\- branch de origem;

\- branch de destino.



Para `staging` e `main`, a origem é validada para garantir o formato

`release/x.x.x.x`.



Caso a origem seja inválida, a validação falha e o merge é bloqueado.



\## Deploy



O workflow `deploy.yml` é executado quando ocorre um `push` nas branches:



\- `develop`

\- `staging`

\- `main`



O deploy é apenas simulado e exibe uma mensagem indicando o ambiente correspondente.



Exemplos:



```text

Deploy realizado no ambiente develop

Deploy realizado no ambiente staging

Deploy realizado no ambiente main

