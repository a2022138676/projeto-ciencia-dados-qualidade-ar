# Previsão da Concentração de Monóxido de Carbono com Dados de Qualidade do Ar

## Identificação da Equipa
* **Grupo nº:** 11
* **Membros:**
  * Rodrigo Pedro — a2023129724
  * Tiago Rodrigues — a2022138676

## Organização do Repositório
A estrutura deste projeto segue boas práticas de Ciência de Dados e Engenharia de Software:

* **`data/`**: armazenamento de dados (`raw/` para dados brutos e `processed/` para dados preparados).
* **`docs/`**: documentação técnica detalhada por Milestones (`M1`, `M2`, `M3` e `M4`).
* **`notebooks/`**: Jupyter Notebooks para exploração, limpeza, preparação e modelação.
* **`src/`**: código-fonte modular com funções reutilizáveis.
* **`reports/`**: relatórios finais, apresentações e exportação de figuras (`figures/`).
* **`requirements.txt`**: bibliotecas e dependências necessárias ao projeto.

## 1. Iniciação (Milestone 1)

### Contexto e Problema de Negócio
Este projeto centra-se na **monitorização da qualidade do ar**, um tema com impacto direto na **saúde pública**, na **gestão ambiental** e no **planeamento urbano**. A poluição atmosférica afeta o bem-estar da população e constitui uma dimensão importante para apoiar políticas públicas, sistemas de monitorização e medidas de prevenção.

O conjunto de dados selecionado, **AirQualityUCI**, contém medições **horárias** de poluentes atmosféricos, como `CO(GT)`, `NOx(GT)` e `NO2(GT)`, bem como leituras de sensores químicos (`PT08.*`) e variáveis meteorológicas, nomeadamente temperatura (`T`), humidade relativa (`RH`) e humidade absoluta (`AH`).

Como o dataset não apresenta um índice global único de “qualidade do ar”, o projeto incide sobre um **indicador mensurável de poluição**. Para a abordagem de **aprendizagem supervisionada por regressão**, foi definida como variável-alvo a coluna **`CO(GT)`**, por corresponder a uma medição de referência de um poluente atmosférico e permitir objetivos concretos de previsão.

O desafio do projeto consiste em **preparar, explorar e analisar** estes dados de forma reprodutível, identificando padrões relevantes e avaliando a capacidade de **prever `CO(GT)`** com modelos de regressão.

### Objetivos do Projeto
* **Objetivo 1:** Construir um processo de preparação de dados reprodutível, incluindo leitura correta do CSV (`sep=';'` e `decimal=','`), remoção de colunas e linhas vazias, criação da variável temporal `timestamp` e conversão do valor `-200` para `NaN`.
* **Objetivo 2:** Realizar análise exploratória de dados (EDA) para identificar padrões temporais, relações entre sensores e poluentes e possíveis ligações com variáveis meteorológicas.
* **Objetivo 3:** Desenvolver e comparar modelos de regressão para prever a variável-alvo **`CO(GT)`**, avaliando o desempenho face a um modelo de referência simples.

### Fonte de Dados
* **Dataset:** AirQualityUCI (Kaggle / ficheiros `AirQualityUCI.csv` e `AirQualityUCI.xlsx`)
* **Dimensão:** 9357 linhas e 15 colunas úteis, após a limpeza estrutural inicial do ficheiro CSV

## 2. Exploração (Milestone 2)

### Limpeza e Preparação
Até ao momento, na Milestone 2, foram desenvolvidas as seguintes etapas:

* Leitura do ficheiro CSV com `sep=';'` e `decimal=','`.
* Remoção de colunas totalmente vazias e de linhas vazias no final do ficheiro.
* Identificação do valor `-200` como código de valores em falta e conversão para `NaN`.
* Criação da variável temporal `timestamp` a partir da junção de `Date` e `Time`.
* Análise da percentagem de valores em falta por coluna.
* Remoção da variável `NMHC(GT)` devido à elevada percentagem de missing values.
* Remoção das linhas com `CO(GT)` em falta, por se tratar da variável-alvo.
* Preenchimento dos restantes valores em falta com a mediana.
* Verificação dos tipos de dados e tratamento inicial de outliers nas variáveis preditoras com base no método do IQR.
* Registo técnico e justificação das decisões em `docs/M2_exploracao.md`.

### Principais Conclusões (EDA)
> *Sugestão: inserir aqui o heatmap de correlação ou um dos scatter plots mais relevantes do projeto.*

* **Ponto-chave:** O valor **`-200`** representa valores em falta e teve de ser convertido para `NaN` antes de qualquer análise estatística ou modelação.
* **Ponto-chave:** A variável **`NMHC(GT)`** revelou uma percentagem muito elevada de valores em falta, o que justificou a sua remoção.
* **Ponto-chave:** As variáveis **`C6H6(GT)`** e **`PT08.S2(NMHC)`** apresentaram correlações positivas muito fortes com `CO(GT)`, enquanto **`PT08.S3(NOx)`** evidenciou uma relação inversa forte.
* **Ponto-chave:** As variáveis meteorológicas **`T`**, **`RH`** e **`AH`** revelaram correlações fracas com a variável-alvo.
* **Ponto-chave:** Até ao momento, o tratamento dos missing values e dos outliers deixou o dataset mais preparado para as etapas seguintes de engenharia de atributos e modelação.

## 3. Modelação (Milestone 3)

### Abordagem Técnica
* **Modelos:** Regressão Linear, Ridge, Lasso, Random Forest Regressor e Gradient Boosting Regressor (a validar e comparar na Milestone 3).
* **Métrica Principal:** **RMSE**, com **MAE** como métrica complementar e **R²** para apoio à interpretação do desempenho.

## 4. Finalização (Milestone 4)

### Resposta ao Problema
No final do projeto, será apresentada uma solução reprodutível para **prever `CO(GT)`** a partir de leituras de sensores (`PT08.*`) e variáveis meteorológicas (`T`, `RH`, `AH`), incluindo a identificação dos fatores com maior influência e a avaliação do desempenho face a um modelo de referência.

### Recomendações de Inovação
1. Integrar o modelo num sistema de monitorização com alertas automáticos quando a previsão ultrapassar um limiar definido.
2. Explorar validação temporal e atualização periódica do modelo, de forma a lidar com sazonalidade e possível deriva do conceito.
3. Criar variáveis adicionais, como hora do dia, dia da semana ou médias móveis, para melhorar a capacidade preditiva.
4. Comparar abordagens lineares e não lineares, avaliando o impacto da multicolinearidade observada entre algumas variáveis.

## Como Reproduzir este Projeto
1. Clone o repositório: `git clone https://github.com/a2022138676/projeto-ciencia-dados-qualidade-ar.git`
2. Instale as dependências: `pip install -r requirements.txt`
3. Execute os notebooks na pasta `notebooks/`, seguindo a ordem numérica.
4. Consulte os ficheiros na pasta `docs/` para acompanhar a evolução do projeto por Milestone.

**Instituição:** Coimbra Business School | ISCAC  
**Curso:** Licenciatura em Ciência de Dados para a Gestão  
**Unidade Curricular:** Projeto em Ciência de Dados  
**Professor Responsável:** Dora Melo (`dmelo@iscac.pt`)
