# Fundamentação teórica

A fundamentação da AC4 aborda os conceitos de DevOps, integração contínua, entrega contínua, implantação contínua e execução de testes sem interface gráfica.

A tabela de conceitos e as respostas completas da Missão 1 estão organizadas no [documento teórico do grupo](https://docs.google.com/document/d/1kE4OXty4JMgDqEIzlUMniFpNfdvoZpbqWd5rIWOECXM/edit). A descrição dos procedimentos e os links das execuções encontram-se no [README](README.md).

## Aplicação dos conceitos no projeto

A integração contínua foi implementada por meio de um workflow do GitHub Actions, que executa os testes a cada alteração enviada ao repositório. O Newman avalia as respostas HTTP e verifica se atendem aos critérios definidos na coleção.

O QA contribui para a definição dos cenários e dos critérios de aprovação, automatiza as verificações e analisa as falhas. Os critérios que bloqueiam uma entrega são acordados pela equipe; neste projeto, qualquer verificação reprovada provoca falha do job.

Os testes de API executados pelo Newman não utilizam navegador. O conceito de modo headless se aplica aos testes de interface que executam um navegador sem interface gráfica, como os realizados com Cypress.

O projeto implementa CI. Entrega contínua e implantação contínua são conceitos distintos: na primeira, o código aprovado permanece pronto para publicação com liberação manual; na segunda, a publicação em produção ocorre automaticamente.
