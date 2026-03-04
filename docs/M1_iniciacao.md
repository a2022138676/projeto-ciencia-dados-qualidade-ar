# Milestone 1: Iniciação e Definição do Projeto

## 1. Descrição Detalhada do Problema
Este projeto centra-se na **monitorização da qualidade do ar**, um tema relevante no contexto da **saúde pública**, **gestão ambiental** e **planeamento urbano**. A poluição atmosférica influencia diretamente o bem-estar da população e é um fator crítico na definição de medidas de prevenção, mitigação e monitorização contínua.

O dataset selecionado, **AirQualityUCI**, contém medições **horárias** de poluentes atmosféricos (por exemplo, `CO(GT)`, `NOx(GT)` e `NO2(GT)`), leituras de sensores químicos (`PT08.*`) e variáveis meteorológicas (temperatura, humidade relativa e humidade absoluta).

Como o dataset não inclui um índice único de “qualidade do ar”, o projeto **foca-se num indicador mensurável de poluição** presente nos dados. Para a abordagem de **aprendizagem supervisionada (regressão)**, a variável-alvo definida é **`CO(GT)`**, por representar uma medição direta (ground truth) de um poluente e permitir objetivos claros de previsão.

**Perguntas de Investigação (mínimo 3):**
- Que padrões horários e/ou diários se observam na concentração de `CO(GT)` ao longo do período analisado?
- Que variáveis (sensores `PT08.*` e variáveis meteorológicas `T`, `RH`, `AH`) apresentam maior relação/correlação com `CO(GT)`?
- É possível prever `CO(GT)` com desempenho superior a um baseline simples (por exemplo, média histórica ou valor anterior), utilizando modelos de regressão?

## 2. Objetivos SMART

**Objetivo 0 (M1):** Até **24/02/2026 (Milestone 1)**, estruturar o repositório e documentar o plano do projeto, garantindo: repositório GitHub com estrutura completa, `README.md` inicial, `docs/M1_iniciacao.md` preenchido e notebook inicial no Kaggle com carregamento do dataset e inspeção básica.  
**Métrica de sucesso:** release/tag do M1 criado no GitHub e notebook a correr do início ao fim sem erros.

**Objetivo 1 (M2):** Até ao final da **Milestone 2 (24/03/2026)**, preparar e explorar o dataset **AirQualityUCI** de forma reprodutível, incluindo: carregamento correto do CSV (`sep=';'`, `decimal=','`), remoção de colunas/linhas totalmente vazias, conversão de `Date` + `Time` para `timestamp` e substituição do código de valores em falta `-200` por `NaN`.  
**Métrica de sucesso:** relatório/tabela com a **percentagem de valores em falta por variável**, EDA com visualizações e conclusões registadas, e dataset processado exportado (quando aplicável).

**Objetivo 2 (M3):** Até ao final da **Milestone 3 (21/04/2026)**, desenvolver e comparar **pelo menos 3 modelos de regressão** para prever **`CO(GT)`**, avaliando com **MAE** e **RMSE** (e **R²** como métrica complementar), e comparando com um **baseline** simples (ex.: média histórica ou valor anterior).  
**Métrica de sucesso:** obter uma melhoria mínima de **15% em MAE ou RMSE** face ao baseline, medida num conjunto de teste definido.

## 3. Metodologia de Gestão (PBL)
**Divisão de Tarefas:**
- **Rodrigo Pedro:** Engenharia de Dados (importação do dataset no Kaggle, leitura do CSV com parsing correto, limpeza estrutural, conversão `-200 → NaN`, criação de `timestamp` e organização do repositório).
- **Tiago Rodrigues:** EDA/Documentação (análise exploratória, gráficos e conclusões, correlações, preparação para modelação, atualização do `README.md` e documentação em `docs/`).

**Ferramentas de Colaboração:** GitHub (controlo de versões), Kaggle Notebooks (execução/partilha), Discord/WhatsApp (comunicação e reuniões curtas).  
**Ferramentas e bibliotecas Python:** `pandas`, `numpy`, `matplotlib`, `scikit-learn`.

## 4. Análise de Viabilidade dos Dados
**Disponibilidade:** O dataset foi obtido e utilizado em dois formatos (`AirQualityUCI.csv` e `AirQualityUCI.xlsx`) e importado para um notebook no Kaggle. O CSV foi lido com `sep=';'` e `decimal=','`, devido ao formato do ficheiro.

**Qualidade Inicial:** Foram executados `df.head()`, `df.info()` e `df.describe()` para inspeção inicial. Após remoção de colunas/linhas totalmente vazias, o dataset apresenta **9357 linhas** e **X colunas úteis** (confirmar e indicar se inclui/exclui `Date`/`Time` e/ou `timestamp`). Verificou-se que:
- existem valores em falta codificados como **`-200`** (não aparecem como `NaN` no ficheiro original), devendo ser convertidos para `NaN`;
- `Date` e `Time` necessitam de ser combinadas numa coluna temporal (`timestamp`) para análise temporal;
- a variável `NMHC(GT)` apresenta uma percentagem muito elevada de valores em falta (~90%), podendo exigir exclusão ou tratamento específico em fases seguintes.

**Ética:** O dataset contém medições ambientais e não inclui dados pessoais ou identificáveis. Assim, o risco de incumprimento do **RGPD** é reduzido. O uso será exclusivamente académico, com documentação transparente das transformações e limitações.

## 5. Cronograma Interno
| Fase | Data Limite | Entregável Esperado |
| :--- | :--- | :--- |
| M1: Iniciação | 24/02/2026 | Repositório estruturado e Plano de Projeto. |
| M2: Exploração | 24/03/2026 | Notebook de EDA e Dados Processados. |
| M3: Modelação | 21/04/2026 | Comparação de algoritmos e métricas. |
| M4: Finalização | 21/05/2026 | Pitch e Relatório Final. |
