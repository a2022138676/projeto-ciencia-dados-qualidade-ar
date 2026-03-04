# Projeto de Ciência de Dados — Qualidade do Ar (AirQualityUCI)

## Identificação da Equipa
* **Grupo nº:** 11
* **Membros:**
 * Rodrigo Pedro - a2023129724
 * Tiago Rodrigues - a2022138676

## Organização do Repositório
A estrutura deste projeto segue as boas práticas de Ciência de Dados e Engenharia de Software:
* **`data/`**: Armazenamento de dados (dados brutos em `raw/` e processados em `processed/`).
* **`docs/`**: Documentação técnica detalhada dividida por Milestones (M1, M2, M3 e M4).
* **`notebooks/`**: Jupyter Notebooks para experimentação, limpeza e modelação.
* **`src/`**: Código-fonte modular (scripts `.py`) para funções reutilizáveis.
* **`reports/`**: Relatórios finais, apresentações e exportação de figuras (`figures/`).
* **`requirements.txt`**: Ficheiro de configuração com as bibliotecas necessárias.

## 1. Iniciação (Milestone 1)

### Contexto e Problema de Negócio
Este projeto centra-se na **monitorização da qualidade do ar**, um tema com impacto direto na **saúde pública**, na **gestão ambiental** e no **planeamento urbano**. A poluição atmosférica influencia o bem-estar da população e é uma dimensão relevante para suportar políticas públicas, sistemas de monitorização e medidas de prevenção.

O conjunto de dados selecionado, **AirQualityUCI**, contém medições **horárias** de poluentes atmosféricos (por exemplo, `CO(GT)`, `NOx(GT)` e `NO2(GT)`), leituras de sensores químicos (`PT08.*`) e variáveis meteorológicas (temperatura, humidade relativa e humidade absoluta).  
Como o conjunto de dados não inclui um índice único de “qualidade do ar”, a abordagem do projeto foca-se num **indicador mensurável de poluição**. Para aprendizagem supervisionada (regressão), a variável-alvo definida é **`CO(GT)`**.

O desafio do projeto consiste em **preparar, explorar e analisar** estes dados de forma reprodutível, identificando padrões relevantes e avaliando a capacidade de **prever `CO(GT)`** com modelos de regressão.

### Objetivos do Projeto
* **Objetivo 1:** Construir um processo de preparação de dados reprodutível (leitura do CSV com `sep=';'` e `decimal=','`, remoção de colunas/linhas vazias, criação de `timestamp` e substituição de `-200` por `NaN`).
* **Objetivo 2:** Realizar análise exploratória (EDA) e identificar padrões horários/diários, relações entre sensores e poluentes, e ligações com variáveis meteorológicas.
* **Objetivo 3:** Desenvolver e comparar modelos de regressão para prever a variável-alvo **`CO(GT)`**, comparando com um modelo de referência simples.

### Fonte de Dados
* **Dataset:** AirQualityUCI (Kaggle / ficheiros `AirQualityUCI.csv` e `AirQualityUCI.xlsx`)
* **Dimensão:** 9357 linhas, 15 colunas úteis (após limpeza estrutural do ficheiro CSV)

## 2. Exploração (Milestone 2)

### Limpeza e Preparação
* Leitura do ficheiro CSV com `sep=';'` e `decimal=','`.
* Remoção de colunas totalmente vazias e de linhas vazias no final do ficheiro.
* Identificação do valor `-200` como código de valores em falta e conversão para `NaN`.
* Criação da coluna temporal `timestamp` a partir de `Date` + `Time`.
* Verificação inicial de integridade temporal (ordenação, duplicados e intervalos horários).
* Detalhes técnicos e evidências em `docs/M2_exploracao.md`.

### Principais Conclusões (EDA)
> *Dica: Insere aqui o gráfico mais importante do projeto.*

* **Ponto-chave:** O valor **`-200`** representa valores em falta e deve ser tratado antes da modelação.
* **Ponto-chave:** A variável `NMHC(GT)` apresenta uma percentagem muito elevada de valores em falta (~90%), podendo justificar exclusão ou tratamento específico.
* **Ponto-chave:** O conjunto de dados apresenta estrutura temporal horária adequada para análise temporal e modelação por regressão.

## 3. Modelação (Milestone 3)

### Abordagem Técnica
* **Modelos:** Regressão Linear / Ridge / Lasso; Random Forest Regressor; Gradient Boosting Regressor (a validar na Milestone 3).
* **Métrica Principal:** RMSE (com MAE como métrica complementar e R² para interpretação adicional).

## 4. Finalização (Milestone 4)

### Resposta ao Problema
No final do projeto, será apresentada uma solução reprodutível para **prever `CO(GT)`** a partir de sensores (`PT08.*`) e variáveis meteorológicas (`T`, `RH`, `AH`), incluindo a identificação dos fatores com maior influência e a avaliação do desempenho face a um modelo de referência.

### Recomendações de Inovação
1. Integrar o modelo num sistema de monitorização com alertas (por exemplo, quando a previsão excede um limiar definido).
2. Explorar validação temporal e atualização periódica do modelo para lidar com sazonalidade e deriva do conceito.
3. Considerar a criação de variáveis adicionais (ex.: hora do dia, dia da semana, média móvel) para melhorar a capacidade preditiva.

## Como Reproduzir este Projeto
1. Clone o repositório: `git clone <url-do-repo>`
2. Instale as dependências: `pip install -r requirements.txt`
3. Execute os notebooks na pasta `notebooks/` seguindo a ordem numérica.

**Instituição:** Coimbra Business School | ISCAC  
**Curso:** Licenciatura em Ciência de Dados para a Gestão  
**Unidade Curricular:** Projeto em Ciência de Dados  
**Professor Responsável:** Dora Melo (dmelo@iscac.pt)
