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
- Validar instrumentos
- Assegurar integridade dos dados

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

### 3.1 Objetivo geral

| Elemento      | Descrição                                                                 |
|---------------|--------------------------------------------------------------------------|
| Analisar      | Repositórios open-source populares que morreram                 |
| Propósito     | Compreender fatores associados à essa morte                   |
| Foco          | Sob os 3 pilares de engajamento, atividades de desenvolvimento e qualidade do código         |                                    |
| Contexto      | Top 1000 repositórios por estrelas no GitHub                             |

### 3.2 Objetivos específicos

| ID  | Objetivo                                                                                      |
|-----|-----------------------------------------------------------------------------------------------|
| 1  | Caracterizar padrões de engajamento (issues, PRs, interações) no período pré-morte          |
| 2  | Identificar mudanças em atividades de desenvolvimento (commits, releases, churn) pré-morte   |
| 3  | Avaliar indicadores de qualidade (complexidade, smells, dívida técnica) pré-morte    |
| 4  | Determinar combinações de métricas dos três pilares que melhor explicam a probabilidade de morte |
| 5  | Construir e validar (por meio de técnicas de machine learning) um modelo preditivo de risco de morte com antecedência, de acordo com a análise dos 3 pilares       |

### 3.3 Questões

| ID  | Questão                                                                                                     |
|-----|-------------------------------------------------------------------------------------------------------------|
| RQ1 | Quais padrões de engajamento (issues, PRs, interação) são encontrados no período pré-morte de repositórios populares?          |
| RQ2 | Quais mudanças nas atividades de desenvolvimento (frequência de commits, releases, churn) são encontrados pré-morte? |
| RQ3 | Quais indicadores de qualidade de código (complexidade, smells, dívida técnica) se degradam ou estabilizam antes da morte? |
| RQ4 | Quais combinações de métricas dos três pilares explicam melhor a probabilidade de morte?                    |
| RQ5 | É possível prever a morte com antecedência (dias ou meses) usando um modelo baseado em métricas históricas correlacionadas?  |

### 3.4 Métricas

| RQ  | Métrica                          | Definição                                      | Unidade          | Fonte              |
|-----|----------------------------------|------------------------------------------------|------------------|--------------------| 
| RQ1 | Issues abertas/mês               | Quantidade de issues abertas por mês           | count/mês        | GitHub GraphQL API |
| RQ1 | Issues fechadas/mês              | Quantidade de issues fechadas por mês          | count/mês        | GitHub GraphQL API |
| RQ1 | Taxa de Merge                       | PRs mergeados / PRs abertos                    | porcentagem            | GitHub GraphQL API |
| RQ1 | Tempo até merge                  | Dias entre abertura e merge do PR              | dias             | GitHub GraphQL API |
| RQ1 | Comentários/PR                   | Média de comentários por PR                    | count            | GitHub GraphQL API |
| RQ1 | Delta de estrelas/mês               | Variação mensal de estrelas                    | count/mês        | GitHub GraphQL API |
| RQ2 | Commits/mês                      | Quantidade de commits por mês                  | count/mês        | PyDriller          |
| RQ2 | Gaps entre commits               | Dias máximos entre commits consecutivos        | dias             | PyDriller          |
| RQ2 | Releases/mês                     | Quantidade de releases por mês                 | count/mês        | GitHub GraphQL API |
| RQ2 | Churn de contribuidores          | (Novos − Saídas) / Total no período            | porcentagem            | PyDriller          |
| RQ2 | Bus factor                       | % commits dos top 2 autores                    | %                | PyDriller          |
| RQ3 | Densidade de smells              | Code smells / KLOC                             | smells/KLOC      | SonarQube          |
| RQ3 | Complexidade ciclomática média   | Média por função                         | Complex. Ciclomática               | SonarQube          |
| RQ3 | Dívida técnica                   | Minutos estimados de correção / KLOC           | min/KLOC         | SonarQube          |
| RQ3 | % Duplicação                     | Linhas duplicadas / LOC total                  | %                | SonarQube          |
| RQ4 | Índice de Engajamento     | score das métricas da RQ1            | score            | Calculado          |
| RQ4 | Índice de Atividade       | score normalizado de métricas da RQ2            | score            | Calculado          |
| RQ4 | Índice de Qualidade       | score normalizado de métricas da RQ3  | score            | Calculado          |
| RQ5 | AUC-ROC*                          | Área sob curva ROC do modelo preditivo         | 0–1              | sklearn            |
| RQ5 | F1-Score*                         | Média harmônica de precisão e recall           | 0–1              | sklearn            |

*A escolha das métricas da RQ5, foi feita de acordo com o que a biblioteca disponibiliza e a necessidade do trabalho em garantir um modelo de previsão mais preciso e equilibrado.

## 4. Escopo e contexto do experimento

### 4.1 Escopo funcional / de processo (incluído e excluído)

**Incluído:**
- Repositórios do Top 1000 por estrelas no GitHub (data de corte T0).
- Linguagens com suporte a SonarQube: JavaScript, TypeScript, Python, Java, Go, C#.
- Janela temporal: 12 meses anteriores à data de corte para séries históricas.
- Métricas de engajamento, atividade e qualidade conforme seção 3.4.
- Repositórios classificados como mortos (>180 dias sem commits) e controles ativos pareados.

**Excluído:**
- Repositórios explicitamente arquivados pelo proprietário.
- Forks sem desenvolvimento próprio significativo.
- Linguagens sem suporte adequado no SonarQube.
- Análise de discussões externas (Discord, Slack, fóruns) — fora do escopo de coleta.

### 4.2 Contexto do estudo (tipo de organização, projeto, experiência)

| Dimensão               | Descrição                                                                 |
|------------------------|--------------------------------------------------------------------------|
| Tipo de organização    | Acadêmico (TCC em Engenharia de Software – PUC Minas)                    |
| Tipo de projeto        | Pesquisa empírica observacional (mineração de repositórios)              |
| Criticidade            | Baixa                 |

### 4.3 Premissas

1. A API GraphQL do GitHub permanecerá disponível e com rate limits suficientes durante a coleta.
2. Os repositórios selecionados estarão acessíveis publicamente.
3. O SonarQube conseguirá analisar a maioria dos repositórios nas linguagens escolhidas.
4. Existem repositórios nos top 1000 do Github que estão a mais de 180 dias sem commits.
5. Métricas coletadas via PyDriller refletem fielmente o histórico de commits.

### 4.4 Restrições

| Tipo          | Descrição                                                                 |
|---------------|--------------------------------------------------------------------------|
| Tempo         | Prazo de TCC limita escopo a 6 meses de execução                        |
| Orçamento     | Uso de ferramentas gratuitas/open-source                     |
| Infraestrutura| Execução local    |
| Rate limits   | API GitHub: 5.000 req/hora pode exigir pausas na coleta   |
| Armazenamento | Clonagem de repositórios limitada pelo espaço de armazenamento

### 4.5 Limitações previstas

- **Generalização restrita:** Resultados aplicam-se a repositórios muito populares (Top 1000); projetos menores podem ter dinâmicas distintas.
- **Viés de linguagem:** Foco em linguagens com suporte SonarQube pode excluir ecossistemas relevantes (Rust, Kotlin).
- **Definição de morte:** Janela de 180 dias pode incluir projetos com ciclos de release longos.
- **Qualidade de métricas:** SonarQube pode não detectar todos os tipos de dívida técnica. Além disso a cobertura de testes depende de configuração do repositório.
- **Snapshot temporal:** Coleta em data única (T0) pode não refletir variações sazonais ou eventos pontuais.

## 5. Stakeholders e impacto esperado

### 5.1 Stakeholders principais

| Stakeholder                      | Papel / Interesse                                                      |
|----------------------------------|---------------------------------------------------------------
| Comunidade científica   | Consumo de resultados, replicação e extensão                           |
| Mantenedores de projetos OSS     | Uso de insights para monitorar saúde de repositórios                   |
| Plataformas (GitHub)             | Potencial uso de métricas para features de alerta de inatividade       |

### 5.2 Interesses e expectativas dos stakeholders

| Stakeholder                      | Expectativa                                                            |
|----------------------------------|------------------------------------------------------------------------|
| Comunidade científica            | Dataset aberto, modelo replicável e evidências estatísticas robustas    |
| Mantenedores OSS                 | Indicadores práticos de risco e  recomendações acionáveis                |
| Plataformas                      | Validação de métricas que possam alimentar dashboards de saúde de repos|

### 5.3 Impactos potenciais no processo / produto

- **Positivos:** Geração de dataset público, com metodologia reprodutível e modelo preditivo disponível para a comunidade.
- **Neutros:** Estudo observacional não interfere em repositórios analisados.
- **Riscos:** Possível sobrecarga de requisições à API (mitigado por rate-limiting) e tempo de processamento do SonarQube pode atrasar cronograma.

## 6. Riscos de alto nível, premissas e critérios de sucesso

### 6.1 Riscos de alto nível (negócio, técnicos, etc.)

| ID  | Risco                                      | Probabilidade | Impacto | Mitigação                                      |
|-----|--------------------------------------------|---------------|---------|------------------------------------------------|
| R1  | API GitHub indisponível ou rate-limited    | Média         | Alto    | Implementar retries, cache e coleta em lotes   |
| R2  | Poucos repositórios mortos no Top 1000     | Média         | Alto    | Expandir para Top 2000 se necessário           |
| R3  | SonarQube falha em repositórios grandes    | Média         | Médio   | Limitar análise a subconjunto de arquivos      |
| R4  | Espaço em disco insuficiente               | Baixa         | Médio   | Clonar shallow e limpar após extração          |
| R5  | Prazo de TCC insuficiente                  | Média         | Alto    | Priorizar RQs 1–3, deixando o modelo preditivo como extra |

### 6.2 Critérios de sucesso globais (go / no-go)

| Critério                                                        | Limiar mínimo                              |
|-----------------------------------------------------------------|--------------------------------------------|
| Quantidade de repositórios mortos identificados                 | ≥ 30 repositórios                          |
| Cobertura de métricas (% repositórios com dados completos)      | ≥ 80%                                      |

### 6.3 Critérios de parada antecipada (pré-execução)

- **Menos de 20 repositórios mortos** encontrados no Top 1000 após filtragem → reavaliar escopo ou expandir universo.
- **API GitHub com bloqueio prolongado** (>7 dias) → buscar alternativas (GH Archive, dataset público).
- **Mudança nos Termos de Serviço do GitHub** que impeça mineração

## 7. Modelo conceitual e hipóteses

### 7.1 Modelo conceitual do experimento
O modelo conceitual do experimento considera que a morte dos repositórios é influenciada por três pilares principais: 

- **Engajamento da comunidade**: A redução na abertura e fechamento de issues, na interação em pull requests e no crescimento de estrelas pode indicar perda de interesse da comunidade.
- **Atividades de desenvolvimento**: Diminuição na frequência de commits, aumento nos gaps entre commits e redução no número de releases podem significar que está havendo um esforço de manutenção.
- **Qualidade do código**: Aumento na densidade de code smells, complexidade e dívida técnica pode indicar a degradação técnica que desestimula contribuições enquanto aumenta as issues.

### 7.2 Hipóteses formais (H0, H1)
As hipóteses são formuladas para cada pilar:

- **Engajamento**:
  - H0E1: Não há diferença significativa na razão de issues abertas/fechadas nos últimos 90 dias pré-morte versus controles ativos.
  - H1E1: Há diferença significativa (menor fechamento ou menor abertura) nessa razão nos repositórios mortos.

- **Atividades de desenvolvimento**:
  - H0A1: A frequência média de commits/mês nos 3 últimos meses pré-morte não difere de controles ativos pareados.
  - H1A1: Repositórios mortos apresentam queda significativa na frequência de commits.

- **Qualidade do código**:
  - H0Q1: Métricas de complexidade média (ex.: complexidade ciclomática por função) não diferem entre mortos e ativos.
  - H1Q1: Repositórios mortos exibem aumento de complexidade ou pull-requests de refatorações que nunca são aprovados.

### 7.3 Nível de significância e considerações de poder
O nível de significância adotado será α = 0,05. O poder estatístico será avaliado para garantir que o tamanho amostral seja suficiente para detectar diferenças significativas.

## 8. Variáveis, fatores, tratamentos e objetos de estudo

### 8.1 Objetos de estudo
Os objetos de estudo são repositórios open-source populares (Top 1000 por estrelas no GitHub) classificados como "mortos" (sem commits por >180 dias) e seus controles ativos pareados.

### 8.2 Sujeitos / participantes (visão geral)
Os participantes indiretos são os mantenedores e contribuidores dos repositórios analisados visto que os dados são públicos e coletados de repositórios GitHub.

### 8.3 Variáveis independentes (fatores) e seus níveis
- **Status de morte**: Morto (1) ou ativo (0).
- **Linguagem principal**: JavaScript, Python, Java, Go, C#, TypeScript.
- **Idade do projeto**: Dias desde o primeiro commit.
- **Tamanho**: LOC total, número de arquivos.

### 8.4 Tratamentos (condições experimentais)
- **Grupo controle**: Repositórios ativos pareados em relação à tamanho com os mortos.
- **Grupo experimental**: Repositórios classificados como mortos.

### 8.5 Variáveis dependentes (respostas)
- **Engajamento**: Issues abertas/fechadas, taxa de merge, comentários por PR.
- **Atividades**: Commits/mês, releases/mês, churn de contribuidores.
- **Qualidade**: Densidade de code smells, complexidade ciclomática, dívida técnica.

### 8.6 Variáveis de controle / bloqueio
- **Linguagem**: Controlada para evitar viés de ecossistema.
- **Tamanho do repositório**: Pareamento por LOC.
- **Idade do repositório**: Pareamento por tempo desde o primeiro commit.

### 8.7 Possíveis variáveis de confusão conhecidas
- **Mudança de mantenedores**: Pode afetar engajamento e atividades.
- **Eventos externos**: Ex.: mudanças na comunidade, no ecossistema, ou até mesmo venda do produto para uma iniciativa privada.

## 9. Desenho experimental

### 9.1 Tipo de desenho (completamente randomizado, blocos, fatorial, etc.)
O desenho será observacional com pareamento entre repositórios mortos e controles ativos. O pareamento será realizado por linguagem, tamanho, idade e popularidade (estrelas).

### 9.2 Randomização e alocação
Não se aplica randomização, pois o estudo é observacional. O pareamento será feito para minimizar viés de seleção.

### 9.3 Balanceamento e contrabalanço
O balanceamento será garantido pelo pareamento de controles ativos com características similares aos repositórios mortos. Não há necessidade de contrabalanço, pois não há ordem de tratamentos.

### 9.4 Número de grupos e sessões
Haverá dois grupos principais:
- **Grupo experimental**: Repositórios mortos (>180 dias sem commits).
- **Grupo controle**: Repositórios ativos pareados.

Cada grupo será analisado em uma única sessão de coleta e análise.

## 10. População, sujeitos e amostragem

### 10.1 População-alvo
A população-alvo são repositórios open-source hospedados no GitHub que atingiram popularidade significativa (medida por estrelas), mas que apesar de terem alcançado sucesso inicial, morreram.

### 10.2 Critérios de inclusão de repositórios
- Pertencer ao Top 1000 repositórios por número de estrelas no GitHub na data de corte T0.
- Linguagem principal com suporte adequado no SonarQube (JavaScript, TypeScript, Python, Java, Go, C#).
- Repositório público e acessível para clonagem.
- Histórico de commits disponível para os 12 meses anteriores a T0.
- Para grupo morto: sem commits no branch principal por >180 dias consecutivos.
- Para grupo controle: pelo menos 1 commit nos últimos 30 dias.

### 10.3 Critérios de exclusão de repositórios
- Repositórios arquivados.
- Forks.
- Repositórios de documentação.
- Repositórios com commits corrompidos.

### 10.4 Tamanho da amostra planejado (por grupo)
| Grupo                | Tamanho esperado | Justificativa                                      |
|----------------------|------------------|----------------------------------------------------|
| Repositórios mortos  | ≥ 30             | Mínimo para análises estatísticas robustas         |
| Repositórios ativos (controle) | 30–60  | Relação 1:1 ou 1:2 com mortos                   |
| **Total estimado**   | 60–90            | Balanceado estatístico         |

Caso o Top 1000 não forneça ≥30 repositórios mortos, o universo será expandido para Top 5000.

### 10.5 Método de seleção / recrutamento
1. **Extração inicial:** Query GraphQL para obter Top 1000 repositórios ordenados por estrelas.
2. **Classificação:** Script automatizado para identificar repositórios mortos (>180 dias sem commits).
3. **Pareamento:** Para cada repositório morto, serão selecionados 1–2 controles ativos pareados por:
   - Linguagem principal (exata)
   - Faixa de estrelas (±10%)
   - Idade do repositório (±1 ano)
   - Tamanho aproximado (LOC ±20%)

### 10.6 Treinamento e preparação dos sujeitos
Não aplicável. O estudo é observacional e os "sujeitos" são repositórios de software. A preparação consiste na configuração do pipeline de coleta e análise.

## 11. Instrumentação e protocolo operacional

### 11.1 Instrumentos de coleta (questionários, logs, planilhas, etc.)

| Instrumento                  | Tipo           | Descrição / Papel                                              |
|------------------------------|----------------|----------------------------------------------------------------|
| GitHub GraphQL API           | API            | Coleta de metadados: issues, PRs, stars, forks, releases       |
| PyDriller                    | Biblioteca Python | Extração de histórico de commits, autores, diffs, churn     |
| SonarQube (Community Edition)| Ferramenta     | Análise estática: smells, complexidade, dívida técnica         |
| Scripts Python        | Scripts        | Transformação e normalização de métricas         |
| Planilha de rastreamento     | Excel      | Controle de repositórios processados, status e erros           |
| Arquivo de configuração de ambiente      | JSON      | Parâmetros do experimento (data T0, thresholds, linguagens)    |
| Logs de execução             | Arquivos .log  | Registro de erros, warnings e progresso do pipeline            |

### 11.2 Materiais de suporte (instruções, guias)
- **README do repositório:** Instruções para configurar ambiente e executar pipeline.
- **Documentação de métricas:** Definição de cada métrica coletada.
- **Checklist de validação:** Verificação de integridade dos dados coletados.

### 11.3 Procedimento experimental (protocolo – visão passo a passo)

![Metodologia_Imagem_1](Metodologia-1.png)

![Metodologia_Imagem_2](Metodologia-2.png)

### 11.4 Plano de piloto (se haverá piloto, escopo e critérios de ajuste)

**Haverá piloto:** Sim

| Aspecto              | Descrição                                                      |
|----------------------|----------------------------------------------------------------|
| Escopo               | Top 100 repositórios (subconjunto do universo)                 |
| Objetivo             | Validar pipeline, identificar gargalos e ajustar thresholds    |
| Duração estimada     | 1–2 semanas                                                    |
| Critérios de ajuste  | Ajustar rate limits, revisar critérios de exclusão, calibrar SonarQube |
| Decisão go/no-go     | Piloto bem-sucedido se ≥5 repositórios mortos identificados e processados |

## 12. Plano de análise de dados (pré-execução)

### 12.1 Estratégia geral de análise (como responderá às questões)

| RQ  | Estratégia de análise                                                                 |
|-----|--------------------------------------------------------------------------------------|
| RQ1 | Estatística descritiva (média, mediana, desvio padrão) e comparação entre grupos (mortos vs ativos) para métricas de engajamento. Visualização com boxplots e gráficos de linha. |
| RQ2 | Análise descritiva de commits, releases e churn. Comparação de medianas entre grupos. Gráficos de tendência temporal. |
| RQ3 | Comparação de métricas de qualidade (smells, complexidade, dívida) entre grupos. Análise de correlação entre métricas. |
| RQ4 | Correlação entre métricas dos três pilares e status de morte. Identificação das métricas mais associadas à morte. |
| RQ5 | Treinamento de modelo de classificação (Random Forest). Avaliação por AUC-ROC e F1-Score. |

### 12.2 Métodos estatísticos planejados

| Tipo de análise              | Método                                      | Aplicação                                  |
|------------------------------|---------------------------------------------|--------------------------------------------|
| Estatística descritiva       | Média, mediana, desvio padrão, quartis      | Caracterizar cada métrica por grupo        |
| Comparação de 2 grupos       | Mann-Whitney U                              | Comparar mortos vs ativos (não-paramétrico)|
| Correlação                   | Spearman                                    | Associação entre métricas contínuas        |
| Classificação (ML)           | Regressão Logística                               | Modelo preditivo de morte                  |

### 12.3 Tratamento de dados faltantes e outliers

**Dados faltantes:**
- Repositórios com muitas métricas ausentes (>30%): exclusão do repositório.
- Para variáveis com poucos valores ausentes: imputação pela mediana do grupo.

**Outliers:**
- Identificação visual por boxplots.
- Documentar outliers identificados e decidir caso a caso se devem ser mantidos ou removidos.

### 12.4 Plano de análise para dados qualitativos (se houver)
O estudo é predominantemente quantitativo. Não há coleta sistemática de dados qualitativos.

## 13. Avaliação de validade (ameaças e mitigação)

### 13.1 Validade de conclusão
| Ameaça | Descrição | Mitigação |
|--------|-----------|----------|
| Baixo poder estatístico | Amostra pequena de repositórios mortos pode não detectar diferenças reais | Garantir mínimo de 30 repositórios mortos e expandir universo se necessário |
| Teste estatístico não atende às condições | Dados podem não seguir distribuição esperada | Usar testes não-paramétricos |
| Erros de medida | Métricas podem conter ruído ou imprecisões | Validar métricas no piloto e documentar limitações das ferramentas |

### 13.2 Validade interna
| Ameaça | Descrição | Mitigação |
|--------|-----------|----------|
| Seleção | Repositórios mortos podem ter características distintas não controladas | Pareamento por linguagem, tamanho, idade e estrelas |
| Contexto histórico do repositório | Eventos externos como mudança de licença podem afetar resultados | Documentar eventos conhecidos |
| Falsas premissas | Variáveis não medidas podem explicar a morte | Incluir variáveis de controle e reconhecer limitação |

### 13.3 Validade de constructo
| Ameaça | Descrição | Mitigação |
|--------|-----------|----------|
| Definição de morte | 180 dias pode não capturar todos os casos de abandono | Justificar com literatura (Dey & Mockus 2020) e fazer análise de sensibilidade com outros thresholds |
| Métricas de qualidade | SonarQube pode não refletir qualidade percebida | Usar múltiplas métricas e documentar as limitações |
| Engajamento incompleto | Não captura discussões externas | Reconhecer como limitação explícita |

### 13.4 Validade externa
| Ameaça | Descrição | Mitigação |
|--------|-----------|----------|
| Generalização restrita | Resultados aplicam-se apenas a repositórios muito populares | Explicitar contexto (Top 1000) e sugerir replicação em outros contextos |
| Viés de linguagem | Foco em linguagens com suporte SonarQube | Documentar linguagens incluídas e discutir o impacto desse ponto |
| Contexto temporal | Coleta em momento único pode não refletir padrões gerais | Registrar data de coleta e sugerir estudos longitudinais |

### 13.5 Resumo das principais ameaças e estratégias de mitigação

| Prioridade | Ameaça | Estratégia |
|------------|--------|------------|
| Alta | Poucos repositórios mortos | Expandir para Top 5000 se necessário |
| Alta | Definição arbitrária de morte | Justificar com literatura e fazer análise de sensibilidade |
| Média | Confundidores não medidos | Pareamento cuidadoso e reconhecer limitação |
| Média | Generalização limitada | Explicitar contexto e sugerir replicações |
| Baixa | Erros de medida | Validar no piloto e usar múltiplas fontes |

## 14. Ética, privacidade e conformidade

### 14.1 Questões éticas (uso de sujeitos, incentivos, etc.)
O estudo utiliza exclusivamente dados públicos de repositórios GitHub, sem interação direta com participantes humanos. Não há:
- Coleta de dados sensíveis ou pessoais
- Incentivos financeiros ou pressão para participação
- Manipulação de repositórios ou interferência em projetos

**Considerações éticas:**
- Respeito aos Termos de Serviço do GitHub
- Uso responsável da API (rate limiting)
- Não há exposição negativa de projetos ou contribuidores específicos

### 14.2 Consentimento informado
Não se aplica.

### 14.3 Privacidade e proteção de dados
**Dados coletados:**
- Métricas agregadas em nível de repositório
- Nomes de usuários apenas para cálculo de métricas (ex.: contagem de contribuidores)

**Proteção:**
- Análises reportadas em nível agregado, sem identificação individual
- Nomes de repositórios podem ser mencionados por serem públicos
- Dados armazenados localmente durante o estudo
- Dataset final disponibilizado sem informações que permitam identificação de indivíduos

### 14.4 Aprovações necessárias (comitê de ética, jurídico, DPO, etc.)
Não é necessário.

## 15. Recursos, infraestrutura e orçamento

### 15.1 Recursos humanos e papéis
| Membro | Papel | Responsabilidades |
|--------|-------|-------------------|
| Gabriel Ramos Ferreira | Pesquisador principal | Execução do experimento, coleta, análise e documentação |
| Danilo Maia | Orientador | Revisão metodológica, validação de resultados, orientação |

### 15.2 Infraestrutura técnica necessária
| Recurso | Descrição | Status |
|---------|-----------|--------|
| Computador pessoal | Mínimo 16GB RAM, 500GB SSD | Disponível |
| Python 3.10+ | Ambiente de análise | Disponível |
| GitHub Personal Access Token | Autenticação para API GraphQL | Disponível |
| SonarQube Community Edition | Análise estática de código | Instalado em docker |
| Git | Clonagem de repositórios | Disponível |
| VS Code / Jupyter | Desenvolvimento e análise | Disponível |

### 15.3 Materiais e insumos
| Material | Tipo | Status |
|----------|------|--------|
| Bibliotecas Python (pandas, scipy, sklearn, PyDriller) | Software | A instalar |
| Espaço em disco | Hardware | Disponível |
| Conexão internet estável | Infraestrutura | Disponível |
| Repositório GitHub para código | Versionamento | A criar |

### 15.4 Orçamento e custos estimados
| Item | Custo estimado | Observação |
|------|----------------|------------|
| Ferramentas | R$ 0 | Todas open-source/gratuitas |
| Infraestrutura | R$ 0 | Uso de recursos próprios |
| GitHub API | R$ 0 | Plano gratuito suficiente |
| Horas do pesquisador | ~200h | Custo de oportunidade |
| **Total** | **R$ 0** | Projeto sem custos diretos |

## 16. Cronograma, marcos e riscos operacionais

### 16.1 Macrocronograma (até o início da execução)
| Fase | Atividade | Início | Fim | Duração |
|------|-----------|--------|-----|----------|
| 1 | Finalização do plano experimental | Jun/2026 | Jun/2026 | 2 semanas |
| 2 | Configuração do ambiente | Jul/2026 | Jul/2026 | 1 semana |
| 3 | Piloto (Top 100) | Jul/2026 | Jul/2026 | 2 semanas |
| 4 | Ajustes pós-piloto | Ago/2026 | Ago/2026 | 1 semana |
| 5 | Coleta completa | Ago/2026 | Set/2026 | 4 semanas |
| 6 | Análise de dados | Set/2026 | Out/2026 | 4 semanas |
| 7 | Redação do TCC | Out/2026 | Nov/2026 | 4 semanas |
| 8 | Revisão e entrega | Nov/2026 | Dez/2026 | 2 semanas |

### 16.2 Dependências entre atividades
```
[Plano] → [Ambiente] → [Piloto] → [Ajustes] → [Coleta] → [Análise] → [Redação] → [Entrega]
```

| Atividade | Depende de |
|-----------|------------|
| Configuração do ambiente | Plano aprovado |
| Piloto | Ambiente configurado |
| Coleta completa | Piloto bem-sucedido |
| Análise | Coleta finalizada |
| Redação | Análise concluída |

### 16.3 Riscos operacionais e plano de contingência
| Risco | Probabilidade | Impacto | Contingência |
|-------|---------------|---------|---------------|
| Atraso na coleta por rate limits | Média | Médio | Implementar cache; coleta em horários de baixa demanda |
| SonarQube falha em repos grandes | Média | Médio | Analisar apenas arquivos principais e limitar o escopo |
| Poucos repositórios mortos | Média | Alto | Expandir para Top 5000 |
| Problemas de saúde/pessoais | Baixa | Alto | Folga de 2 semanas no cronograma |
| Perda de dados | Baixa | Alto | Backup diário em nuvem e HD externo |

## 17. Governança do experimento

### 17.1 Papéis e responsabilidades formais
| Papel | Pessoa | Responsabilidade |
|-------|--------|------------------|
| Executor | Gabriel Ramos | Implementar pipeline, coletar dados, executar análises |
| Decisor | Gabriel Ramos | Aprovar mudanças de escopo menores |
| Revisor | Danilo Maia | Validar metodologia, revisar resultados |
| Aprovador | Danilo Maia | Aprovar mudanças significativas no plano |

### 17.2 Ritos de acompanhamento pré-execução
| Rito | Frequência | Participantes | Objetivo |
|------|------------|---------------|----------|
| Reunião de orientação | Quinzenal | Gabriel, Danilo | Acompanhar progresso, resolver bloqueios |
| Checkpoint de fase | A cada marco | Gabriel, Danilo | Validar entregáveis |
| Revisão do piloto | Após piloto | Gabriel, Danilo | Avaliar resultados, ajustar plano |

### 17.3 Processo de controle de mudanças no plano
**Mudanças menores** (ajustes de threshold, inclusão de métrica):
1. Documentar mudança no histórico de revisões
2. Informar orientador na próxima reunião

**Mudanças significativas** (alteração de RQs, expansão de escopo):
1. Propor mudança por escrito
2. Discutir com orientador
3. Obter aprovação formal
4. Atualizar documento e versão

## 18. Plano de documentação e reprodutibilidade

### 18.1 Repositórios e convenções de nomeação
**Repositório principal:** `github.com/gramos22/tcc-morte-repositorios`

**Estrutura de pastas:**
```
/
├── docs/              # Documentação e plano experimental
├── scripts/           # Scripts de coleta e análise
├── data/              # Dados coletados (raw e processados)
├── notebooks/         # Jupyter notebooks de análise
├── results/           # Resultados e visualizações
└── README.md          # Instruções gerais
```

**Convenções de nomeação:**
- Scripts: `snake_case.py` (ex.: `collect_github_metrics.py`)
- Dados: `YYYY-MM-DD_descricao.csv` (ex.: `2026-02-15_repos_mortos.csv`)
- Notebooks: `NN_descricao.ipynb` (ex.: `01_exploratory_analysis.ipynb`)

### 18.2 Templates e artefatos padrão
| Artefato | Localização | Descrição |
|----------|-------------|----------|
| Plano experimental | `/docs/proposta.md` | Este documento |
| Script de coleta GitHub | `/scripts/collect_github.py` | Coleta via GraphQL API |
| Script PyDriller | `/scripts/collect_commits.py` | Extração de histórico |
| Notebook de análise | `/notebooks/` | Análises estatísticas |
| Checklist de validação | `/docs/checklist.md` | Verificação de dados |

### 18.3 Plano de empacotamento para replicação futura
**Artefatos para replicação:**
1. **requirements.txt** - Dependências Python com versões fixas
2. **README.md** - Instruções passo a passo para execução
3. **config.json** - Parâmetros do experimento (T0, thresholds)
4. **Dataset final** - Dados anonimizados em formato CSV
5. **Scripts documentados** - Comentários explicativos no código

**Disponibilização:**
- Repositório público no GitHub após defesa
- Registrar dataset para DOI permanente

## 19. Plano de comunicação

### 19.1 Públicos e mensagens-chave pré-execução
| Público | Mensagem-chave | Momento |
|---------|----------------|----------|
| Orientador | Status do projeto, bloqueios, decisões necessárias | Contínuo |
| Banca avaliadora | Objetivos, metodologia, resultados esperados | Defesa |
| Comunidade científica | Contribuições, dataset, modelo preditivo | Pós-defesa |

### 19.2 Canais e frequência de comunicação
| Canal | Uso | Frequência |
|-------|-----|------------|
| E-mail | Comunicações formais, envio de documentos | Conforme necessidade |
| Reuniões presenciais/online | Orientação, revisões | Quinzenal |
| GitHub | Acompanhamento de progresso, código | Contínuo |
| WhatsApp/Teams | Dúvidas rápidas, agendamentos | Conforme necessidade |

### 19.3 Pontos de comunicação obrigatórios
| Evento | Ação | Destinatário |
|--------|------|---------------|
| Aprovação do plano | E-mail formal | Orientador |
| Conclusão do piloto | Relatório + reunião | Orientador |
| Mudança significativa de escopo | Proposta escrita + reunião | Orientador |
| Bloqueio crítico | Comunicação imediata | Orientador |
| Conclusão da coleta | Relatório de status | Orientador |
| Entrega final | Documento completo | Orientador + Banca |

## 20. Critérios de prontidão para execução (Definition of Ready)

### 20.1 Checklist de prontidão (itens que devem estar completos)

**Documentação:**
- [ ] Plano experimental revisado e aprovado pelo orientador
- [ ] Definições operacionais de todas as métricas documentadas
- [ ] Critérios de inclusão/exclusão finalizados

**Infraestrutura:**
- [ ] Ambiente Python configurado com todas as dependências
- [ ] GitHub Personal Access Token configurado e testado
- [ ] SonarQube instalado e funcionando
- [ ] Espaço em disco suficiente (~100GB)
- [ ] Repositório Git criado e estruturado

**Validação:**
- [ ] Piloto executado com sucesso (≥5 repositórios mortos processados)
- [ ] Scripts de coleta testados e funcionando
- [ ] Métricas extraídas corretamente no piloto

**Planejamento:**
- [ ] Cronograma detalhado definido
- [ ] Riscos identificados e mitigações planejadas
- [ ] Backup e versionamento configurados

### 20.2 Aprovações finais para iniciar a operação
| Aprovador | Critério | Registro |
|-----------|----------|----------|
| Gabriel Ramos | Checklist 100% completo | Commit no repositório |
| Danilo Maia | Plano experimental aprovado | E-mail de confirmação |
| Danilo Maia | Resultados do piloto satisfatórios | Ata de reunião |

**Condição de início:** Todos os itens do checklist marcados e aprovações registradas.
