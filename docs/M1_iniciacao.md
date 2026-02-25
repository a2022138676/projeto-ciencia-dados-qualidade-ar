# Milestone 1: Iniciação e Definição do Projeto

## 1. Descrição Detalhada do Problema
Este projeto centra-se na **monitorização da qualidade do ar**, um tema relevante nas áreas da **saúde pública**, **gestão ambiental** e **cidades inteligentes**. A poluição atmosférica tem impacto direto no bem-estar da população e na definição de políticas públicas, tornando a análise destes dados particularmente importante no contexto atual.

O dataset selecionado, **AirQualityUCI**, contém medições horárias de poluentes atmosféricos (como CO, NOx e NO2), leituras de sensores químicos e variáveis meteorológicas (temperatura, humidade relativa e humidade absoluta). Este conjunto de dados permite analisar padrões temporais e relações entre variáveis, bem como desenvolver modelos preditivos em fases posteriores do projeto.

O problema é relevante para a unidade curricular de Projeto de Ciência de Dados porque permite aplicar a metodologia **CRISP-DM** de forma completa, começando pela compreensão do problema e dos dados, passando pela preparação e análise exploratória, e evoluindo para modelação e avaliação.

## 2. Objetivos SMART
*Defina os objetivos do projeto seguindo a lógica SMART (Específico, Mensurável, Atingível, Relevante e Temporal):*

1. **Objetivo 1:** Construir, até à **Milestone 2**, um pipeline de preparação de dados reprodutível para o dataset **AirQualityUCI**, incluindo conversão de `Date` + `Time` para `timestamp`, remoção de colunas/linhas vazias e substituição dos valores inválidos `-200` por `NaN`, com documentação de todas as transformações.
2. **Objetivo 2:** Realizar, até à **Milestone 2**, uma análise exploratória com **pelo menos 5 visualizações** e **5 conclusões documentadas** sobre padrões horários/diários, correlações entre sensores e poluentes, e relação com variáveis meteorológicas.
3. **Objetivo 3:** Desenvolver e comparar, até à **Milestone 3**, **pelo menos 3 modelos de regressão** para prever uma variável-alvo (ex.: `CO(GT)` ou `NO2(GT)`), avaliados com **MAE, RMSE e R²**, obtendo uma melhoria mínima de **15% em MAE ou RMSE** face a um modelo de referência simples (baseline).

## 3. Metodologia de Gestão (PBL)
* **Divisão de Tarefas:**
  * **Rodrigo Pedro:** Responsável pela **Engenharia de Dados e Preparação** (carregamento dos ficheiros CSV/XLSX, limpeza inicial, tratamento dos valores `-200`, transformação de `Date` + `Time` para `timestamp` e preparação do dataset para EDA/modelação).
  * **Tiago Rodrigues:** Responsável pela **Análise Exploratória, Modelação e Documentação** (estatística descritiva, visualizações, análise de correlações, construção e avaliação de modelos de regressão, atualização do `README.md` e do `docs/M1_iniciacao.md`).
  * **Trabalho de ambos:** Definição dos objetivos SMART, perguntas de investigação, interpretação de resultados, revisão final da documentação e apresentação do projeto.
* **Ferramentas de Colaboração:** **GitHub** (repositório e controlo de versões), **GitHub Projects/Issues** (gestão de tarefas/Kanban), **Kaggle Notebooks** (exploração inicial), **Python + Jupyter** (análise/modelação), **Discord/WhatsApp** (comunicação e reuniões).

## 4. Análise de Viabilidade dos Dados
* **Disponibilidade:** Os dados já foram descarregados e estão disponíveis em dois formatos: `AirQualityUCI.csv` e `AirQualityUCI.xlsx`. O ficheiro XLSX encontra-se mais limpo para arranque da exploração, enquanto o CSV será útil para validar o pipeline de ingestão (com parsing específico de separador `;` e decimal `,`).
* **Qualidade Inicial:** Na inspeção preliminar, verificou-se que o dataset útil tem **9357 observações** e **15 variáveis** (após limpeza do CSV). O ficheiro CSV contém colunas vazias extra e linhas vazias no final. Foram identificados valores inválidos codificados como **`-200`**, que representam valores em falta e terão de ser convertidos para `NaN` na M2. A coluna `NMHC(GT)` apresenta uma percentagem muito elevada de valores em falta (~90%), podendo vir a ser excluída ou tratada de forma específica.
* **Ética:** O dataset contém **dados ambientais** e **não inclui dados pessoais**, pelo que o risco de incumprimento do RGPD é muito reduzido. Ainda assim, serão seguidas boas práticas de utilização académica, referência à origem dos dados e documentação transparente das transformações efetuadas. Reconhece-se também que os resultados podem não generalizar para outros contextos geográficos/temporais.

### Primeiras Impressões Técnicas (Aula 5 – Inspeção Inicial no Kaggle)
Na Aula 5 foi realizada uma inspeção inicial do dataset **AirQualityUCI** num Kaggle Notebook, com execução dos comandos `df.head()`, `df.info()` e `df.describe()`.

#### Resultados da inspeção inicial
- O dataset, após limpeza estrutural do ficheiro CSV (remoção de colunas e linhas totalmente vazias), apresenta **9357 observações** e **15 variáveis**.
- Foi confirmado que o ficheiro CSV utiliza **separador `;`** e **decimal `,`**, exigindo parsing específico no carregamento (`sep=';'`, `decimal=','`).
- As colunas incluem variáveis de data/hora, poluentes atmosféricos, sensores químicos e variáveis meteorológicas.

#### Verificação de integridade e tipos de dados
- A estrutura geral dos dados é adequada para análise exploratória e futura modelação.
- As colunas `Date` e `Time` encontram-se separadas, sendo necessária a sua combinação numa coluna temporal (`timestamp`) para análise de séries temporais.
- As restantes colunas de medições são maioritariamente numéricas e compatíveis com análise estatística e modelação.

#### Valores em falta / valores inválidos
- Foi identificado que o valor **`-200`** é utilizado como **código para valores em falta** em várias variáveis.
- Após substituição de `-200` por `NaN`, verificou-se a existência de valores em falta com impacto relevante em algumas colunas, nomeadamente:
  - `NMHC(GT)` com percentagem muito elevada de valores em falta (~90%);
  - `CO(GT)`, `NOx(GT)` e `NO2(GT)` com percentagens aproximadas entre 17% e 18%;
  - outras variáveis com percentagens inferiores.
- Esta situação será tratada de forma sistemática na fase de exploração/modelação (milestones seguintes), através de estratégias de limpeza, imputação e/ou exclusão de variáveis.

#### Conclusão da inspeção inicial
A inspeção inicial confirma que o dataset **AirQualityUCI** é **viável e adequado** ao projeto, mas exige tratamento prévio de qualidade de dados, especialmente no que respeita à codificação de valores em falta (`-200`).

## 5. Cronograma Interno
| Fase | Data Limite | Entregável Esperado |
| :--- | :--- | :--- |
| M1: Iniciação | 24/02/2026 | Repositório estruturado e Plano de Projeto. |
| M2: Exploração | 24/03/2026 | Notebook de EDA e dados processados. |
| M3: Modelação | 21/04/2026 | Comparação de algoritmos e métricas. |
| M4: Finalização | 21/05/2026 | Pitch e relatório final. |

---
*Data de última atualização: 25/02/2026*
