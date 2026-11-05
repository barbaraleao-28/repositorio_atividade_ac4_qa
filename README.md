# Semana 13 — Integração Contínua em QA

Atividade do Módulo 3 — Automação de Testes. Identificação do trio pendente.

## Executar

Requisitos: Git e Node.js 24 com npm.

```sh
npm ci
npm test
```

A coleção Postman v2.1 consulta `GET /users/1` (200), consulta `GET /users/999999` (404) e envia `POST /posts` (201) à API pública https://jsonplaceholder.typicode.com.
O POST é simulado pela API: a resposta não significa que o post foi persistido.

## Pipeline

`.github/workflows/main.yml` executa em cada push ou pelo botão Run workflow. O job `testes-api` baixa o código, configura Node.js, instala as dependências com `npm ci` e executa Newman. Qualquer assertion que falhar produz código de saída diferente de zero e deixa o job vermelho. Os relatórios JSON e JUnit são enviados como artefatos mesmo quando os testes falham.

## Quebrar e consertar

1. Alterar somente o valor esperado de `Status 200`, de 200 para 201, em `colecao.json`.
2. Commit e push; abrir Actions e conferir a falha indicando 201 esperado e 200 recebido.
3. Restaurar 200, fazer commit e push e conferir o resultado verde.
4. Acrescentar uma assertion para o corpo do post, fazer commit e push e conferir o novo resultado verde.

As execuções locais são evidências locais; só a execução na aba Actions comprova o CI remoto. Este repositório implementa CI, sem implantação em produção e sem regra de proteção de branch.

## Referências

- https://learning.postman.com/docs/collections/using-newman-cli/installing-running-newman/
- https://learning.postman.com/docs/collections/using-newman-cli/newman-options/
- https://github.com/actions/setup-node
- https://github.com/actions/upload-artifact


## Execuções comprovadas no GitHub Actions

Repositório privado, conforme solicitado: https://github.com/barbaraleao-28/repositorio_atividade_ac4_qa

- Primeiro pipeline aprovado: https://github.com/barbaraleao-28/repositorio_atividade_ac4_qa/actions/runs/42129943947
- Falha proposital (esperado 201, recebido 200): https://github.com/barbaraleao-28/repositorio_atividade_ac4_qa/actions/runs/42130093311
- Correção aprovada: https://github.com/barbaraleao-28/repositorio_atividade_ac4_qa/actions/runs/42130384836
- O commit seguinte adiciona a verificação de preservação do corpo do post. Consulte a aba Actions para o resultado.

Os arquivos foram publicados pela interface web do GitHub porque o gerenciador de credenciais do Git não iniciou no ambiente de execução. Isso gera commits e dispara o mesmo evento push do workflow.

A coleção final tem 3 requisições e 11 assertions: status, identificador/nome/e-mail do usuário, resposta vazia para usuário inexistente e identificador/título/autor/corpo do post criado.
