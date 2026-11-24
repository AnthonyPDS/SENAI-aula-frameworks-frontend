# Aula 6 — Projetos Front-End (Gestão Ágil)

**Disciplina:** Frameworks Front-end  
**Professor:** Prof. Me. Deivison S. Takatu

---

## 📌 Sumário da Aula
1. Por que gerenciar um projeto Front-End?
2. Gestão de Projetos Front-End
3. Gestão de Requisitos (Requisito, User Story e Tarefa)
4. Gestão do Backlog
5. Priorização e Estimativa
6. Definition of Done (DoD)
7. Framework Ágil Scrum

---

## 1. Por que gerenciar um projeto Front-End?

Projetos Front-End crescem rapidamente em número de componentes, estados e integrações.

| Sem Planejamento e Gestão | Com Processo de Gestão |
| :--- | :--- |
| Tarefas esquecidas e requisitos confusos | Responsabilidades claras na equipe |
| Retrabalho constante e atrasos | Prioridades bem definidas |
| Conflitos frequentes no Git | Entregas incrementais e contínuas |
| Problemas de integração com APIs | Acompanhamento visível do progresso |
| Dificuldade para medir o progresso | Redução significativa de retrabalho |

---

## 2. Gestão de Requisitos: Do Problema às Tarefas

Um projeto nasce de uma ideia que precisa ser transformada em **requisitos claros**, estruturada em um **Backlog** e quebrada em unidades acionáveis:

- **Requisito:** Declaração macro da capacidade do sistema.  
  *Exemplo:* "O sistema deve permitir o gerenciamento de tarefas."
- **User Story (História de Usuário):** Descrição centrada no valor para o usuário final.  
  *Exemplo:* "Como usuário, quero criar uma tarefa para organizar meu dia."
- **Tarefas Técnicas (Tasks):** Passos práticos de implementação no Front-End:
  - Criar formulário e componente visual
  - Validar campos de entrada
  - Integrar com a API (Back-end)
  - Criar e executar testes

---

## 3. Backlog, Priorização e Estimativa

- **Gestão do Backlog:** Reúne todas as funcionalidades, melhorias, correções de bugs e atividades técnicas necessárias para desenvolver e evoluir o produto.
- **Priorização:** Determina o que deve ser construído primeiro considerando valor de negócio, necessidades do usuário, dependências técnicas e restrições de prazo.
- **Estimativa:** Ajuda a equipe a compreender a **complexidade relativa** e o esforço de cada atividade antes de assumir o compromisso de entrega em um ciclo.

---

## 4. Definition of Done (DoD — Definição de Pronto)

Estabelece uma lista de critérios objetivos para que uma tarefa ou história seja considerada **realmente concluída**. No desenvolvimento Front-End, um bom *Definition of Done* inclui:
- [x] Código implementado seguindo os padrões do projeto
- [x] Responsividade verificada (mobile/desktop)
- [x] Integração com a API realizada e tratada
- [x] Testes executados sem erros
- [x] Code review (revisão de código) concluído e branch integrada

---

## 5. Scrum no Desenvolvimento Front-End

O **Scrum** é um framework ágil para desenvolvimento de produtos complexos de forma **incremental e iterativa**, baseado em transparência, inspeção frequente e adaptação:
- Organiza o trabalho em ciclos curtos chamados **Sprints**.
- Utiliza quadros visuais (**Kanban / Scrum Board**) para acompanhar o fluxo (*To Do*, *In Progress*, *Code Review*, *Done*).
- Alinha o uso de **branches no Git** com as tarefas do backlog para evitar conflitos e manter entregas contínuas.

### 🔗 Repositórios de Referência da Aula
- [Aula Gestão](https://github.com/deivisontakatu/aula-gestao)
- [Aula Gestão de Produto](https://github.com/deivisontakatu/aula-gestao-produto)
- [Aula Scrum](https://github.com/deivisontakatu/aula-scrum)
