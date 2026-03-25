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
A qualidade do ar é um tema relevante para a saúde pública, para a gestão ambiental e para o apoio à decisão em contexto urbano. A existência de mecanismos que permitam antecipar níveis mais elevados de poluição pode ajudar entidades públicas e sistemas de monitorização a agir de forma mais informada.

Neste projeto pretende-se estudar a previsão da concentração de monóxido de carbono em ambiente urbano, procurando avaliar se é possível estimar esse valor com base em informação recolhida em contexto de monitorização da qualidade do ar. O problema é relevante porque a antecipação de episódios de maior poluição pode apoiar ações de prevenção, vigilância e mitigação.

### Objetivos do Projeto
* **Objetivo 1:** Até ao final da Milestone 2, preparar um conjunto de dados consistente e reprodutível para modelação, garantindo a remoção de colunas irrelevantes, o tratamento de valores em falta, a criação de atributos temporais derivados e a documentação completa das transformações efetuadas.
* **Objetivo 2:** Até ao final da Milestone 3, desenvolver e comparar pelo menos três modelos de regressão para prever a concentração de monóxido de carbono, avaliando o seu desempenho com base nas métricas RMSE, MAE e R².
* **Objetivo 3:** Até ao final da Milestone 3, selecionar um modelo com desempenho superior a um baseline simples, demonstrando capacidade preditiva útil para a estimação da concentração de monóxido de carbono.
* **Objetivo 4:** Até ao final da Milestone 4, interpretar os resultados obtidos e identificar os atributos com maior influência na previsão, de forma a produzir conclusões úteis para a monitorização da poluição atmosférica.

### Questões de Investigação
* É possível prever a concentração de monóxido de carbono com desempenho superior a um modelo de referência simples, utilizando modelos de regressão?
* Que variáveis apresentam maior contributo para a previsão da concentração de monóxido de carbono?
* A inclusão de variáveis temporais derivadas melhora o desempenho preditivo dos modelos?
* Modelos não lineares apresentam melhor desempenho do que modelos lineares na previsão da concentração de monóxido de carbono?

### Fonte de Dados
* Fonte oficial do dataset: UCI Machine Learning Repository — Air Quality
* Criador: Saverio Vito
* DOI: 10.24432/C5060Z
* Ligação oficial: https://archive.ics.uci.edu/dataset/387/air+quality

### Plataforma de Desenvolvimento
A exploração, limpeza e preparação inicial dos dados têm sido desenvolvidas em ambiente Kaggle Notebook, utilizando a versão do dataset disponibilizada na plataforma Kaggle. O notebook principal desta fase foi posteriormente exportado para a pasta `notebooks/` do repositório GitHub.

* Plataforma: Kaggle
* Dataset no Kaggle: AirQualityUCI
* Ligação do dataset: https://www.kaggle.com/datasets/jhonan/airqualityuci
* Ligação do notebook: (https://www.kaggle.com/code/rodrigopedro20/airquality-dataset)

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
<img width="955" height="659" alt="image" src="https://github.com/user-attachments/assets/821abe2f-8fd1-4034-9287-68232033b0f5" />

*Figura 1 — Heatmap da matriz de correlação entre as variáveis numéricas do dataset.*

* Ponto-chave: O valor `-200` representa valores em falta e foi convertido para `NaN` antes da análise.
* Ponto-chave: A variável `NMHC(GT)` apresentou uma percentagem muito elevada de valores em falta, o que justificou a sua remoção.
* Ponto-chave: As variáveis `C6H6(GT)` e `PT08.S2(NMHC)` apresentaram correlações positivas muito fortes com `CO(GT)`.
* Ponto-chave: As variáveis meteorológicas `T`, `RH` e `AH` revelaram correlações fracas com a variável-alvo.

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
