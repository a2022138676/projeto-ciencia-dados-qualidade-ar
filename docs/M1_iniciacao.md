# Milestone 1: Iniciação e Definição do Projeto

## 1. Descrição Detalhada do Problema
Este projeto centra-se na **monitorização da qualidade do ar**, um tema relevante nos domínios da **saúde pública**, da **gestão ambiental** e do **planeamento urbano**. A poluição atmosférica afeta diretamente o bem-estar da população, sendo um fator crítico para a definição de medidas de prevenção, mitigação e monitorização contínua.

O conjunto de dados selecionado, **AirQualityUCI**, contém medições **horárias** de poluentes atmosféricos, como `CO(GT)`, `NOx(GT)` e `NO2(GT)`, bem como leituras de sensores químicos (`PT08.*`) e variáveis meteorológicas, nomeadamente temperatura (`T`), humidade relativa (`RH`) e humidade absoluta (`AH`).

Uma vez que o dataset não apresenta um índice global único de “qualidade do ar”, o projeto incide sobre um indicador quantitativo de poluição diretamente presente nos dados. Para a abordagem de **aprendizagem supervisionada do tipo regressão**, foi definida como variável-alvo a coluna **`CO(GT)`**, por corresponder a uma medição de referência de um poluente atmosférico e por permitir a formulação de objetivos concretos de previsão.

### Perguntas de Investigação
- Que padrões horários e/ou diários podem ser observados na concentração de `CO(GT)` ao longo do período analisado?
- Que variáveis, nomeadamente os sensores `PT08.*` e as variáveis meteorológicas `T`, `RH` e `AH`, apresentam maior relação com `CO(GT)`?
- É possível prever `CO(GT)` com desempenho superior a um modelo de referência simples, utilizando modelos de regressão?

## 2. Objetivos SMART

**Objetivo 1 (M1):** Até **24/02/2026**, estruturar o repositório GitHub e documentar o plano do projeto, garantindo a existência de uma estrutura organizada, de um `README.md` inicial, do ficheiro `docs/M1_iniciacao.md` preenchido e de um notebook no Kaggle com o carregamento do conjunto de dados e a respetiva inspeção inicial.  
**Métrica de sucesso:** criação da release/tag correspondente ao M1 no GitHub e notebook executado do início ao fim sem erros.

**Objetivo 2 (M2):** Até **24/03/2026**, preparar e explorar o conjunto de dados **AirQualityUCI** de forma reprodutível, incluindo a leitura correta do ficheiro CSV (`sep=';'` e `decimal=','`), a remoção de colunas totalmente vazias, a conversão de `Date` e `Time` para uma variável temporal e a substituição do código de valores em falta `-200` por `NaN`.  
**Métrica de sucesso:** produção de uma tabela com a percentagem de valores em falta por variável, realização de análise exploratória com visualizações e registo das principais conclusões, bem como geração do conjunto de dados processado, quando aplicável.

**Objetivo 3 (M3):** Até **21/04/2026**, desenvolver e comparar **pelo menos três modelos de regressão** para prever **`CO(GT)`**, recorrendo às métricas **MAE** e **RMSE**, bem como ao **R²** como métrica complementar, e comparando os resultados com um modelo de referência simples.  
**Métrica de sucesso:** obtenção de uma melhoria mínima de **15% em MAE ou RMSE** face ao modelo de referência, num conjunto de teste previamente definido.

## 3. Metodologia de Gestão (PBL)

### Divisão de Tarefas
- **Rodrigo Pedro:** responsável pela engenharia de dados, incluindo a importação do dataset no Kaggle, leitura correta do ficheiro CSV, limpeza estrutural, conversão de `-200` para `NaN`, criação da variável temporal (`timestamp`) e organização do repositório.
- **Tiago Rodrigues:** responsável pela análise exploratória dos dados, visualizações, interpretação de resultados, documentação em `docs/` e atualização do `README.md`.

### Ferramentas de Colaboração
- **GitHub** para controlo de versões e organização do portefólio
- **Kaggle** para desenvolvimento e execução dos notebooks
- **Discord** e/ou **WhatsApp** para comunicação e reuniões curtas

### Ferramentas e Bibliotecas Python
- `pandas`
- `numpy`
- `matplotlib`
- `seaborn`
- `scikit-learn`

## 4. Análise de Viabilidade dos Dados

**Disponibilidade:** O conjunto de dados foi obtido em dois formatos, `AirQualityUCI.csv` e `AirQualityUCI.xlsx`, tendo sido importado para um notebook no Kaggle. O ficheiro CSV exige leitura com `sep=';'` e `decimal=','`, devido ao seu formato original.

**Qualidade Inicial:** Foram executados os comandos `df.head()`, `df.info()` e `df.describe()` para inspeção inicial. Verificou-se que o conjunto de dados original contém **9471 linhas e 17 colunas**, incluindo **duas colunas finais vazias**, que deverão ser removidas. Assim, o dataset apresenta **15 colunas úteis** para análise inicial. Foram ainda identificados os seguintes aspetos:
- existem valores em falta codificados como **`-200`**, que não surgem inicialmente como `NaN` e terão de ser convertidos;
- as colunas `Date` e `Time` devem ser combinadas numa variável temporal (`timestamp`) para permitir análise cronológica;
- a variável `NMHC(GT)` apresenta uma percentagem muito elevada de valores em falta, o que poderá justificar a sua exclusão ou tratamento específico em fases posteriores;
- poderão existir outliers e inconsistências que terão de ser analisados durante a Milestone 2.

**Ética:** O conjunto de dados é constituído por medições ambientais e não inclui dados pessoais nem identificáveis. Assim, o risco de incumprimento do **RGPD** é reduzido. A utilização do dataset será exclusivamente académica, com documentação transparente das transformações, limitações e decisões tomadas.

## 5. Cronograma Interno

| Fase | Data Limite | Entregável Esperado |
| :--- | :--- | :--- |
| M1: Iniciação | 24/02/2026 | Repositório estruturado e plano de projeto |
| M2: Exploração | 24/03/2026 | Notebook de EDA e dados processados |
| M3: Modelação | 21/04/2026 | Comparação de algoritmos e métricas |
| M4: Finalização | 21/05/2026 | Pitch e relatório final |

---

*Data de última atualização: 06/03/2026*
