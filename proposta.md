# Plano de Experimento – Scoping e Planejamento

## 1. Identificação básica

### 1.1 Título do experimento
Mapeando a Morte de Repositórios Open-Source: uma Análise Empírica sobre Engajamento, Atividades e Qualidade do Código

### 1.2 ID / código
GRAMOS1.0

### 1.3 Versão do documento e histórico de revisão
Tabela de versões e revisões:

| Versão | Data        | Descrição                                                                 |
|--------|-------------|---------------------------------------------------------------------------|
| v1.0   | 20/11/2025  | Primeira elaboração das seções 1 e 2 baseada na definição do tema e GQM. |

### 1.4 Datas (criação, última atualização)
| Item                                     | Valor                                      |
|------------------------------------------|--------------------------------------------|
| Data de criação                          | 20/11/2025                                 |
| Última atualização                       | 20/11/2025                                 |

### 1.5 Autores (nome, área, contato)
| Papel                       | Nome                          | Contato                                                     |
|----------------------------|-------------------------------|-------------------------------------------------------------|
| Autor principal            | Gabriel Ramos Ferreira         | gabriel.ferreira.732131@sga.pucminas.br |
| Revisor metodológico       | Danilo de Quadros Maia Filho  | 1514571@sga.pucminas.br

### 1.6 Responsável principal (PI / dono do experimento)

#### Gabriel Ramos Ferreira

**Responsabilidades:**

- Aderência metodológica
- Aprovar mudanças de escopo
- Validar instrumentos assegurar
- Integridade dos dados

### 1.7 Projeto / produto / iniciativa relacionada 

**Área de conhecimento:** Sustentabilidade e evolução de projetos open-source.  

**Projeto:** Potencial geração de dataset público reutilizável e metodologia para análise de risco de morte de repositórios.

**Benefícios esperados:** Orientar mantenedores sobre sinais precoces de morte e fomentar estudos subsequentes sobre o gerenciamneto de projetos para OSS.

## 2. Contexto e problema

### 2.1 Descrição do problema / oportunidade
Repositórios open-source populares são uma porcentagem muito pequena de projetos que obtiveram sucesso em seu gerenciamento sem nenhum tipo de investimento financeiro, que acaba tornando difícil sua manutenção. No entanto, seu sucesso não garante que eles não voltem a passar por períodos de baixa constribuição que podem levar à sua morte. Tanto a comunidade científica, quanto a comunidade open-source já tem conhecimento desse fenômeno, mas ainda existem lacunas na compreensão de como padrões de engajamento comunitário, atividades de desenvolvimento e qualidade do código interagem antes da morte. A oportunidade é caracterizar esses padrões e construir bases de dados que possibilitem a comparação para os projetos existentes e a detecção precoce dos padrões que levam à morte dos repositórios, apoiando manutenção e tomada de decisão.

### 2.2 Contexto organizacional e técnico
O experimento será realizado em contexto acadêmico de TCC utilização de dados públicos do GitHub.

**Ferramentas técnicas:** GitHub GraphQL API (metadados de issues, PRs, stars, forks), PyDriller (histórico de commits), SonarQube (qualidade estática), ambiente de análise Python (pandas, numpy, scipy, scikit-learn). 

**Processo:** pipeline reprodutível de coleta → transformação → análise estatística → modelagem preditiva. 

Dados tratados em nível de repositório sem identificação sensível de indivíduos.

### 2.3 Trabalhos e evidências prévias (internos e externos)
#### Evidências externas

[Dey & Mockus 2020](https://dl.acm.org/doi/10.1145/3382494.3410685), que justifica a morte considerada a partir de 180 dias de inatividade.

#### Evidências internas

No momento existem dados coletados pelo projeto de pesquisa de TI6 (se encontra privado no momento) relacionados à reativação de repositórios que morreram pelo período de 180 dias. No entanto, o foco dessa coleta foi apenas nos repositórios que se reativaram, o que já da um ponto de partida, com aqueles que apenas morreram sem se reativar.

### 2.4 Referencial teórico e empírico essencial

Referências ligadas aos três pilares (Engajamento, Atividades, Qualidade).

| Referência               | Pilar principal          | Achado relevante / Contribuição                        | Aplicação no Estudo                              |
|--------------------------|--------------------------|--------------------------------------------------------|--------------------------------------------------|
| [Serebrenik & Vasilescu 2019](https://arxiv.org/abs/1906.08058) | Engajamento/Atividade | Sinais precursores de abandono                         | Definição operacional de morte e sinais iniciais |
| [Kaur et. al. 2022](https://www.sciencedirect.com/science/article/pii/S1319157820305139?via%3Dihub)         | Engajamento             | Fatores de participação e retenção                     | Seleção de variáveis de engajamento              |
| [Steinmacher et al. 2021](https://arxiv.org/abs/2103.04656)  | Onboarding              | Diretrizes para entrada de novos contribuidores        | Interpretação do churn e retenção                |
| [Coelho et al. 2020](https://ieeexplore.ieee.org/document/6606589)       | Manutenção              | Tipos e métricas de manutenção                         | Classificação de commits/manutenção              |
| [Mockus et al. 2002](https://dl.acm.org/doi/10.1145/567793.567795)       | Dinâmica OSS            | Estrutura de papéis e contribuição                     | Modelagem de distribuição de esforço             |
| [Hilton et al. 2016](https://dl.acm.org/doi/10.1145/2970276.2970358)       | Engajamento/Qualidade   | Fatores que afetam aceitação de PR                     | Métricas de merge rate e tempo até merge         |
| [Ma et al. 2019](https://arxiv.org/abs/1908.09321)           | Qualidade/Engajamento   | Contribuição e qualidade influenciam aceitação de PR   | Conectar qualidade de código e throughput PR     |

## 3. Objetivos e questões (Goal / Question / Metric)

### 3.1 Objetivo geral (Goal template)
Preencha o objetivo geral usando um template claro (por exemplo, GQM), deixando explícito o que será analisado, com qual propósito, sob qual perspectiva e em qual contexto.

### 3.2 Objetivos específicos
Decomponha o objetivo geral em metas mais focadas (O1, O2, etc.), que descrevam resultados concretos de aprendizado ou decisão que o experimento deve gerar.

### 3.3 Questões de pesquisa / de negócio
Formule perguntas claras que o experimento deverá responder (Q1, Q2, etc.), em linguagem que faça sentido para os stakeholders técnicos e de negócio.

### 3.4 Métricas associadas (GQM)
Associe a cada questão as métricas que serão usadas para respondê-la, com nome, definição, unidade e fonte dos dados, garantindo alinhamento entre G, Q e M.

## 4. Escopo e contexto do experimento

### 4.1 Escopo funcional / de processo (incluído e excluído)
Explique claramente o que será coberto (atividades, artefatos, equipes, módulos) e o que ficará fora do experimento, para evitar interpretações divergentes.

### 4.2 Contexto do estudo (tipo de organização, projeto, experiência)
Caracterize o contexto em que o estudo ocorrerá: tipo e tamanho de organização, tipo de projeto, criticidade e perfil de experiência dos participantes.

### 4.3 Premissas
Liste as suposições consideradas verdadeiras para o plano funcionar (por exemplo, disponibilidade de ambiente, estabilidade do sistema), mesmo que não possam ser garantidas.

### 4.4 Restrições
Registre limitações práticas como tempo, orçamento, ferramentas, acessos ou regras organizacionais que impõem limites ao desenho.

### 4.5 Limitações previstas
Explique fatores que podem prejudicar a generalização dos resultados (validez externa), como contexto muito específico ou amostra pouco representativa.

## 5. Stakeholders e impacto esperado

### 5.1 Stakeholders principais
Liste os grupos ou papéis que têm interesse ou serão impactados pelo experimento (por exemplo, devs, QA, produto, gestores, clientes internos).

### 5.2 Interesses e expectativas dos stakeholders
Descreva o que cada grupo espera obter do experimento (insights, evidências, validação de decisão, mitigação de risco, etc.).

### 5.3 Impactos potenciais no processo / produto
Antecipe como a execução do experimento pode afetar prazos, qualidade, carga de trabalho ou o próprio produto durante e após o estudo.

## 6. Riscos de alto nível, premissas e critérios de sucesso

### 6.1 Riscos de alto nível (negócio, técnicos, etc.)
Identifique os principais riscos para negócio e tecnologia (atrasos, falhas de ambiente, indisponibilidade de dados, etc.) em nível macro.

### 6.2 Critérios de sucesso globais (go / no-go)
Defina as condições sob as quais o experimento será considerado útil e viável, inclusive critérios que sustentem uma decisão de seguir ou não com mudanças.

### 6.3 Critérios de parada antecipada (pré-execução)
Descreva situações em que o experimento deve ser adiado ou cancelado antes de começar (falta de recursos críticos, reprovação ética, mudanças de contexto).

## 7. Modelo conceitual e hipóteses

### 7.1 Modelo conceitual do experimento
Explique, em texto ou esquema, como você acredita que os fatores influenciam as respostas (por exemplo, "técnica A reduz defeitos em relação a B").

### 7.2 Hipóteses formais (H0, H1)
Formule explicitamente as hipóteses nulas e alternativas para cada questão principal, incluindo a direção esperada do efeito quando fizer sentido.

### 7.3 Nível de significância e considerações de poder
Defina o nível de significância (por exemplo, α = 0,05) e comente o que se espera em termos de poder estatístico, relacionando-o ao tamanho de amostra planejado.

## 8. Variáveis, fatores, tratamentos e objetos de estudo

### 8.1 Objetos de estudo
Descreva o que será efetivamente manipulado ou analisado (módulos de código, requisitos, tarefas, casos de teste, issues, etc.).

### 8.2 Sujeitos / participantes (visão geral)
Caracterize em alto nível quem serão os participantes (desenvolvedores, testadores, estudantes, etc.), sem ainda entrar em detalhes de seleção.

### 8.3 Variáveis independentes (fatores) e seus níveis
Liste os fatores que serão manipulados (por exemplo, técnica, ferramenta, processo) e indique os níveis de cada um (A/B, X/Y, alto/baixo).

### 8.4 Tratamentos (condições experimentais)
Descreva claramente cada condição de experimento (grupo controle, tratamento 1, tratamento 2, etc.) e o que distingue uma da outra.

### 8.5 Variáveis dependentes (respostas)
Informe as medidas de resultado que você observará (por exemplo, número de defeitos, esforço em horas, tempo de conclusão, satisfação).

### 8.6 Variáveis de controle / bloqueio
Liste fatores que você não está estudando diretamente, mas que serão mantidos constantes ou usados para formar blocos (por exemplo, experiência, tipo de tarefa).

### 8.7 Possíveis variáveis de confusão conhecidas
Identifique fatores que podem distorcer os resultados (como diferenças de contexto, motivação ou carga de trabalho) e que você pretende monitorar.

## 9. Desenho experimental

### 9.1 Tipo de desenho (completamente randomizado, blocos, fatorial, etc.)
Indique qual tipo de desenho será utilizado e justifique brevemente por que ele é adequado ao problema e às restrições.

### 9.2 Randomização e alocação
Explique o que será randomizado (sujeitos, tarefas, ordem de tratamentos) e como a randomização será feita na prática (ferramentas, procedimentos).

### 9.3 Balanceamento e contrabalanço
Descreva como você garantirá que os grupos fiquem comparáveis (balanceamento) e como lidará com efeitos de ordem ou aprendizagem (contrabalanço).

### 9.4 Número de grupos e sessões
Informe quantos grupos existirão e quantas sessões ou rodadas cada sujeito ou grupo irá executar, com uma breve justificativa.

## 10. População, sujeitos e amostragem

### 10.1 População-alvo
Descreva qual é a população real que você deseja representar com o experimento (por exemplo, "desenvolvedores Java de times de produto web").

### 10.2 Critérios de inclusão de sujeitos
Especifique os requisitos mínimos para um participante ser elegível (experiência, conhecimento, papel, disponibilidade, etc.).

### 10.3 Critérios de exclusão de sujeitos
Liste condições que impedem participação (conflitos de interesse, falta de skills essenciais, restrições legais ou éticas).

### 10.4 Tamanho da amostra planejado (por grupo)
Defina quantos participantes você pretende ter no total e em cada grupo, relacionando a decisão com poder, recursos e contexto.

### 10.5 Método de seleção / recrutamento
Explique como os participantes serão escolhidos (amostra de conveniência, sorteio, convite aberto, turma de disciplina, time específico).

### 10.6 Treinamento e preparação dos sujeitos
Descreva qual treinamento ou material preparatório será fornecido para nivelar entendimento e reduzir vieses por falta de conhecimento.

## 11. Instrumentação e protocolo operacional

### 11.1 Instrumentos de coleta (questionários, logs, planilhas, etc.)
Liste todos os instrumentos que serão usados para coletar dados (arquivos, formulários, scripts, ferramentas), com uma breve descrição do papel de cada um.

### 11.2 Materiais de suporte (instruções, guias)
Descreva as instruções escritas, guias rápidos, slides ou outros materiais que serão fornecidos a participantes e administradores do experimento.

### 11.3 Procedimento experimental (protocolo – visão passo a passo)
Escreva, em ordem, o que acontecerá na operação (do convite ao encerramento), de modo que alguém consiga executar o experimento seguindo esse roteiro.

### 11.4 Plano de piloto (se haverá piloto, escopo e critérios de ajuste)
Indique se um piloto será realizado, com que participantes e objetivos, e defina que tipo de ajuste do protocolo poderá ser feito com base nesse piloto.

## 12. Plano de análise de dados (pré-execução)

### 12.1 Estratégia geral de análise (como responderá às questões)
Explique, em alto nível, como os dados coletados serão usados para responder cada questão de pesquisa ou de negócio.

### 12.2 Métodos estatísticos planejados
Liste os principais testes ou técnicas estatísticas que pretende usar (por exemplo, t-teste, ANOVA, testes não paramétricos, regressão).

### 12.3 Tratamento de dados faltantes e outliers
Defina previamente as regras para lidar com dados ausentes e valores extremos, evitando decisões oportunistas após ver os resultados.

### 12.4 Plano de análise para dados qualitativos (se houver)
Descreva como você tratará dados qualitativos (entrevistas, comentários, observações), especificando a técnica de análise (codificação, categorias, etc.).

## 13. Avaliação de validade (ameaças e mitigação)

### 13.1 Validade de conclusão
Liste ameaças que podem comprometer a robustez das conclusões estatísticas (baixo poder, violação de suposições, erros de medida) e como pretende mitigá-las.

### 13.2 Validade interna
Identifique ameaças relacionadas a causas alternativas para os efeitos observados (history, maturation, selection, etc.) e explique suas estratégias de controle.

### 13.3 Validade de constructo
Reflita se as medidas escolhidas realmente representam os conceitos de interesse e descreva como você reduzirá ambiguidades de interpretação.

### 13.4 Validade externa
Discuta em que contextos os resultados podem ser generalizados e quais diferenças de cenário podem limitar essa generalização.

### 13.5 Resumo das principais ameaças e estratégias de mitigação
Faça uma síntese das ameaças mais críticas e das ações planejadas, de preferência em forma de lista ou tabela simples.

## 14. Ética, privacidade e conformidade

### 14.1 Questões éticas (uso de sujeitos, incentivos, etc.)
Descreva potenciais questões éticas (pressão para participar, uso de estudantes, incentivos, riscos de exposição) e como serão tratadas.

### 14.2 Consentimento informado
Explique como os participantes serão informados sobre objetivos, riscos, benefícios e como registrarão seu consentimento.

### 14.3 Privacidade e proteção de dados
Indique que dados pessoais serão coletados, como serão protegidos (anonimização, pseudoanonimização, controle de acesso) e por quanto tempo serão mantidos.

### 14.4 Aprovações necessárias (comitê de ética, jurídico, DPO, etc.)
Liste órgãos ou pessoas que precisam aprovar o experimento (comitê de ética, jurídico, DPO, gestores) e o status atual dessas aprovações.

## 15. Recursos, infraestrutura e orçamento

### 15.1 Recursos humanos e papéis
Identifique os membros da equipe do experimento e descreva brevemente o papel e responsabilidade de cada um.

### 15.2 Infraestrutura técnica necessária
Liste ambientes, servidores, ferramentas, repositórios e integrações que devem estar disponíveis para executar o experimento.

### 15.3 Materiais e insumos
Relacione materiais físicos ou digitais necessários (máquinas, licenças, formulários, dispositivos) que precisam estar prontos antes da operação.

### 15.4 Orçamento e custos estimados
Faça uma estimativa dos principais custos envolvidos (horas de pessoas, serviços, licenças, infraestrutura) e a fonte de financiamento.

## 16. Cronograma, marcos e riscos operacionais

### 16.1 Macrocronograma (até o início da execução)
Defina as principais datas e marcos (conclusão do plano, piloto, revisão, início da operação) com uma visão de tempo realista.

### 16.2 Dependências entre atividades
Indique quais atividades dependem de outras para começar (por exemplo, treinamento após aprovação ética), deixando essas dependências claras.

### 16.3 Riscos operacionais e plano de contingência
Liste riscos ligados a cronograma, disponibilidade de pessoas ou recursos, e descreva ações de contingência caso esses riscos se materializem.

## 17. Governança do experimento

### 17.1 Papéis e responsabilidades formais
Defina quem decide, quem executa, quem revisa e quem apenas deve ser informado, deixando claro o fluxo de responsabilidade.

### 17.2 Ritos de acompanhamento pré-execução
Descreva as reuniões, checkpoints e revisões previstos antes da execução, incluindo frequência e participantes.

### 17.3 Processo de controle de mudanças no plano
Explique como mudanças no desenho ou no escopo do experimento serão propostas, analisadas, aprovadas e registradas.

## 18. Plano de documentação e reprodutibilidade

### 18.1 Repositórios e convenções de nomeação
Indique onde o plano, instrumentos, scripts e dados (futuros) serão armazenados e quais convenções de nomes serão usadas.

### 18.2 Templates e artefatos padrão
Liste os modelos (questionários, formulários, checklists, scripts) que serão usados e onde podem ser encontrados.

### 18.3 Plano de empacotamento para replicação futura
Descreva o que será organizado desde já (documentos, scripts, instruções) para facilitar a replicação do experimento por outras equipes ou no futuro.

## 19. Plano de comunicação

### 19.1 Públicos e mensagens-chave pré-execução
Liste os grupos que precisam ser comunicados e quais mensagens principais devem receber (objetivos, escopo, datas, impactos esperados).

### 19.2 Canais e frequência de comunicação
Defina por quais canais (e-mail, reuniões, Slack/Teams, etc.) e com que frequência as comunicações serão feitas.

### 19.3 Pontos de comunicação obrigatórios
Especifique os eventos que exigem comunicação formal (aprovação do plano, mudanças relevantes, adiamentos, cancelamentos).

## 20. Critérios de prontidão para execução (Definition of Ready)

### 20.1 Checklist de prontidão (itens que devem estar completos)
Liste os itens que precisam estar finalizados e aprovados (plano, instrumentos, aprovação ética, recursos, comunicação) para autorizar o início da operação.

### 20.2 Aprovações finais para iniciar a operação
Indique quem precisa dar o "ok final" (nomes ou cargos) e como esse aceite será registrado antes da execução começar.
