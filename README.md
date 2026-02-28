# Projeto de Ciência de Dados — Qualidade do Ar (AirQualityUCI)

## Identificação da Equipa
* **Grupo nº:** 11
* **Membros:**
 * **Rodrigo Pedro** - [a2023129724]
 * **Tiago Rodrigues** - [a2022138676]

## Organização do Repositório
A estrutura deste projeto segue as boas práticas de Ciência de Dados e Engenharia de Software:

* **`data/`**: Armazenamento de dados (dados brutos em `raw/` e processados em `processed/`).
* **`docs/`**: Documentação técnica detalhada dividida por Milestones (M1, M2, M3 e M4).
* **`notebooks/`**: Jupyter Notebooks para experimentação, limpeza e modelação.
* **`src/`**: Código-fonte modular (scripts `.py`) para funções reutilizáveis.
* **`reports/`**: Relatórios finais, apresentações e exportação de figuras (`figures/`). *(pasta prevista para fases posteriores)*  
* **`requirements.txt`**: Ficheiro de configuração com as bibliotecas necessárias. *(a criar/atualizar ao longo do projeto)*

## 1. Iniciação (Milestone 1)

### Contexto e Problema de Negócio
Este projeto centra-se na **monitorização da qualidade do ar**, um tema com forte impacto na **saúde pública**, na **gestão ambiental** e no **planeamento urbano**. A poluição atmosférica influencia diretamente o bem-estar da população e é uma dimensão relevante para a definição de políticas públicas, sistemas de monitorização e medidas de prevenção.

O dataset selecionado, **AirQualityUCI**, contém medições horárias de poluentes atmosféricos (por exemplo, `CO(GT)`, `NOx(GT)` e `NO2(GT)`), leituras de sensores químicos (`PT08.*`) e variáveis meteorológicas (temperatura, humidade relativa e humidade absoluta). Este conjunto de dados permite analisar padrões temporais, relações entre variáveis e, em fases posteriores, desenvolver modelos preditivos para estimar variáveis de qualidade do ar.

O desafio do projeto consiste em preparar e analisar estes dados de forma reprodutível, identificando padrões relevantes e avaliando a capacidade de previsão de variáveis-alvo associadas à qualidade do ar.

### Objetivos do Projeto
* **Objetivo 1:** Construir um pipeline de preparação de dados reprodutível (conversão de `Date` + `Time` para `timestamp`, remoção de colunas/linhas vazias e substituição de `-200` por `NaN`).
* **Objetivo 2:** Realizar análise exploratória (EDA) e identificar padrões horários/diários, correlações entre sensores e poluentes, e relações com variáveis meteorológicas.
* **Objetivo 3:** Desenvolver e comparar modelos de regressão para prever uma variável-alvo de qualidade do ar (ex.: `CO(GT)` ou `NO2(GT)`).

### Fonte de Dados
* **Dataset:** AirQualityUCI (Kaggle / ficheiros `AirQualityUCI.csv` e `AirQualityUCI.xlsx`)
* **Dimensão:** **9357 linhas, 15 colunas úteis** (após limpeza estrutural do ficheiro CSV)
* **Observação técnica:** O ficheiro CSV requer parsing específico (`sep=';'`, `decimal=','`).

## 2. Exploração (Milestone 2)

### Limpeza e Preparação
* Leitura do ficheiro CSV com parsing específico (`sep=';'`, `decimal=','`).
* Remoção de colunas totalmente vazias e linhas vazias no final do ficheiro.
* Identificação do valor **`-200`** como código de valores em falta e conversão para `NaN`.
* Criação da coluna temporal `timestamp` a partir de `Date` + `Time`.
* Verificação inicial de integridade temporal (ordenação, duplicados e intervalos horários).
* Detalhes técnicos e evidências serão documentados em `docs/M2_exploracao.md`.

### Principais Conclusões (EDA)
> *Dica: Insere aqui o gráfico mais importante do projeto.*

* **Ponto-chave:** Foi identificado que o valor **`-200`** representa valores em falta, sendo obrigatório o seu tratamento antes da modelação.
* **Ponto-chave:** A variável `NMHC(GT)` apresenta uma percentagem muito elevada de valores em falta (~90%), podendo exigir exclusão ou tratamento específico.
* **Ponto-chave:** O dataset apresenta estrutura temporal horária adequada para análise temporal e modelação por regressão.

## 3. Modelação (Milestone 3)

### Abordagem Técnica


## 4. Finalização (Milestone 4)

### Resposta ao Problema


### Recomendações de Inovação

## Como Reproduzir este Projeto
1. Clone o repositório: `git clone [url-do-repo]`
2. Instale as dependências: `pip install -r requirements.txt`
3. Execute os notebooks na pasta `notebooks/` seguindo a ordem numérica.

**Instituição:** Coimbra Business School | ISCAC  
**Curso:** Licenciatura em Ciência de Dados para a Gestão  
**Unidade Curricular:** Projeto em Ciência de Dados  
**Professor Responsável:** Dora Melo (dmelo@iscac.pt)
