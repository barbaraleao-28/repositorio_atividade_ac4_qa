# AC4 — Integração Contínua em QA

Atividade do Módulo 3 — Automação de Testes, desenvolvida no curso ADS 5 NA, sob orientação do professor Raphael Botelho.

## Integrantes

- Mateus Henrique Gomes
- Barbara Maria Rodrigues Leao
- Nicole Lara Silva Almeida
- Rodrigo Neves Vieira

## Objetivo

Aplicar integração contínua aos testes de uma API, utilizando uma coleção Postman executada pelo Newman no GitHub Actions. A atividade demonstra a detecção de uma falha intencional, sua correção e a inclusão de uma nova verificação.

## Estrutura do projeto

- `colecao.json`: coleção de testes da API.
- `.github/workflows/main.yml`: configuração do pipeline.
- `package.json` e `package-lock.json`: dependências e comando de execução.
- `TEORIA.md`: fundamentação e acesso ao documento teórico do grupo.

## Execução local

Requisitos: Node.js 24 e npm.

```sh
npm ci
npm test
```

## Cenários de teste

A coleção utiliza a API pública [JSONPlaceholder](https://jsonplaceholder.typicode.com) e contém 3 requisições e 12 verificações.

| Requisição | Verificações |
| --- | --- |
| `GET /users/1` | Status 200, identificador 1, nome Leanne Graham, JSON Schema e formato do e-mail. |
| `GET /users/9999` | Status 404 e resposta vazia. |
| `POST /posts` | Status 201, título enviado, identificador numérico, autor e corpo da mensagem. |

A criação do post é simulada pela API; a resposta não representa persistência do recurso.

## Funcionamento do pipeline

O workflow **Testes de API** é iniciado a cada `push` e também permite execução manual por `workflow_dispatch`. O job `testes-api` utiliza `ubuntu-latest`, configura Node.js 24, instala as dependências com `npm ci` e executa a coleção com `npm test`.

Uma verificação reprovada faz o Newman retornar código de saída diferente de zero, sinalizando a falha do job. Os relatórios JSON e JUnit são preservados no artefato `relatorios-newman`, inclusive nas execuções com falha.

O escopo do projeto é a integração contínua. Não foi configurada implantação em produção nem regra de proteção de branch.

## Resultados da atividade

| Etapa | Resultado | Comprovação |
| --- | --- | --- |
| Pipeline inicial | Aprovado | [Execução 1](https://github.com/barbaraleao-28/repositorio_atividade_ac4_qa/actions/runs/42129943947) |
| Falha intencional | Reprovado: status esperado 201, recebido 200 | [Execução 2](https://github.com/barbaraleao-28/repositorio_atividade_ac4_qa/actions/runs/42130093311) |
| Correção da expectativa | Aprovado | [Execução 3](https://github.com/barbaraleao-28/repositorio_atividade_ac4_qa/actions/runs/42130384836) |
| Inclusão do teste de preservação do corpo do post | Aprovado | [Execução 4](https://github.com/barbaraleao-28/repositorio_atividade_ac4_qa/actions/runs/42130573632) |
| Integração da coleção base da aula | Aprovado: 3 requisições, 12 verificações e nenhuma falha | [Execução 5](https://github.com/barbaraleao-28/repositorio_atividade_ac4_qa/actions/runs/42132159714) |

Na falha intencional, a expectativa da consulta de usuário foi alterada de 200 para 201. Após a restauração do valor correto, o pipeline voltou a apresentar resultado aprovado. O histórico preserva as evidências desse processo.

As lacunas do modelo de workflow fornecido na aula correspondem a `push`, `ubuntu-latest` e `colecao.json`.

## Referências

- Material da Semana 13 — Professor Raphael Botelho.
- [Documentação do Newman](https://learning.postman.com/docs/collections/using-newman-cli/installing-running-newman/).
- [GitHub Actions](https://docs.github.com/actions).
