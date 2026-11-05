# Missão 1 — Conceitos

| Conceito | Definição | Aplicação nesta atividade |
| --- | --- | --- |
| DevOps | Cultura de colaboração entre desenvolvimento e operação para entregas frequentes e confiáveis. | Automatizar a verificação a cada alteração. |
| QA | Atuação para prevenir problemas e avaliar a qualidade do produto e do processo. | Definir cenários, assertions e critérios de aprovação. |
| Shift-left | Antecipar atividades de qualidade no ciclo de desenvolvimento. | Testar cada mudança, antes da entrega. |
| CI | Integrar e testar alterações automaticamente com frequência. | GitHub Actions executa Newman em cada push. |
| Entrega contínua | Manter mudanças aprovadas prontas para publicação, com decisão humana de liberar. | Não implementada neste exercício. |
| Implantação contínua | Publicar automaticamente mudanças aprovadas em produção. | Não implementada neste exercício. |
| Headless | Executar navegador sem interface gráfica. | Cypress run usa esse modo; Newman testa HTTP sem navegador. |
| Workflow | Automação descrita em YAML. | .github/workflows/main.yml. |
| Gatilho | Evento que inicia a automação. | push e workflow_dispatch. |
| Job | Conjunto de passos executado em um runner. | testes-api. |
| Runner | Máquina que executa o job. | ubuntu-latest hospedado pelo GitHub. |
| Step | Comando ou action dentro do job. | Instalar dependências e rodar a coleção. |
| Action | Componente reutilizável do workflow. | checkout, setup-node e upload-artifact. |
| Assertion | Verificação de uma expectativa. | Status 200, 404 e 201 e dados das respostas. |
| Artefato | Arquivo preservado ao final da execução. | Relatórios JSON e JUnit do Newman. |

## Discussão complementar

Estas respostas são complementares. As três perguntas específicas e a tabela original do roteiro do aluno não foram fornecidas; não se afirma que estes sejam os enunciados do professor.

**Por que usar CI?** Para detectar rapidamente problemas introduzidos por mudanças e verificar o projeto em um ambiente reproduzível, com resultados associados a cada commit.

**Qual é o papel do QA?** Selecionar cenários relevantes, automatizar verificações, estabelecer critérios de aprovação e analisar as falhas. Uma assertion inválida também deve ser corrigida; pipeline verde não garante ausência de todos os defeitos.

**O que o ciclo vermelho → verde demonstra?** Que uma expectativa incorreta faz a execução falhar e que sua correção permite a aprovação. O workflow acusa a falha; bloquear merges exige configurar uma regra de proteção separadamente.
