# Previsão da Concentração de Monóxido de Carbono com Dados de Qualidade do Ar

## Identificação da Equipa
* **Grupo n.º:** 11
* **Membros:**
  * Rodrigo Pedro — a2023129724
  * Tiago Rodrigues — a2022138676

## Organização do Repositório
A estrutura deste projeto segue boas práticas de Ciência de Dados e Engenharia de Software:

* **`data/`**: armazenamento de dados (`raw/` para dados brutos e `processed/` para dados preparados)
* **`docs/`**: documentação técnica detalhada por Milestones (`M1`, `M2`, `M3` e `M4`)
* **`notebooks/`**: Jupyter Notebooks para exploração, limpeza, preparação e modelação
* **`src/`**: código-fonte modular com funções reutilizáveis
* **`reports/`**: relatórios finais, apresentações e exportação de figuras (`figures/`)
* **`requirements.txt`**: bibliotecas e dependências necessárias ao projeto

---

## 1. Iniciação (Milestone 1)

### Contexto e Problema de Negócio
A qualidade do ar é um tema relevante para a saúde pública, para a gestão ambiental e para o apoio à decisão em contexto urbano. A existência de mecanismos que permitam antecipar níveis mais elevados de poluição pode ajudar entidades públicas e sistemas de monitorização a agir de forma mais informada.

Neste projeto pretende-se estudar a previsão da concentração de monóxido de carbono em ambiente urbano, procurando avaliar se é possível estimar esse valor com base em informação recolhida em contexto de monitorização da qualidade do ar. O problema é relevante porque a antecipação de episódios de maior poluição pode apoiar ações de prevenção, vigilância e mitigação.

### Objetivos do Projeto

* **S (Specific):** Prever a concentração de monóxido de carbono (`CO(GT)`) em ambiente urbano, com base em dados históricos de qualidade do ar, sensores químicos e variáveis meteorológicas.
* **M (Measurable):** Avaliar o desempenho dos modelos de regressão através de métricas como **RMSE**, **MAE** e **R²**, comparando diferentes algoritmos de *machine learning* com um modelo de referência simples.
* **A (Achievable):** Utilizar um dataset real de monitorização da qualidade do ar, com registos horários e variáveis adequadas à aplicação de técnicas de análise de dados, engenharia de atributos e modelação preditiva.
* **R (Relevant):** Contribuir para a compreensão dos fatores associados à concentração de monóxido de carbono e apoiar a monitorização da poluição atmosférica, com potencial utilidade em contextos de saúde pública e gestão ambiental.
* **T (Time-bound):** Desenvolver, preparar, treinar e avaliar os modelos preditivos até ao final da unidade curricular, de acordo com o cronograma definido nas diferentes Milestones do projeto.

### Questões de Investigação
* É possível prever a concentração de monóxido de carbono com desempenho útil a partir dos dados disponíveis?
* Que atributos têm maior influência na previsão da concentração de monóxido de carbono?
* A utilização de modelos não lineares melhora a capacidade preditiva face a modelos lineares?
* A criação de novos atributos e a seleção de variáveis melhoram o desempenho dos modelos?

### Fonte de Dados
* **Fonte oficial do dataset:** UCI Machine Learning Repository — Air Quality
* **Criador:** Saverio Vito
* **DOI:** 10.24432/C5060Z
* **Ligação oficial:** https://archive.ics.uci.edu/dataset/387/air+quality

### Plataforma de Desenvolvimento
A exploração, limpeza, preparação e modelação dos dados foram desenvolvidas em ambiente Kaggle Notebook, utilizando a versão do dataset disponibilizada na plataforma Kaggle. Os notebooks principais foram posteriormente exportados para a pasta `notebooks/` do repositório GitHub.

* **Plataforma:** Kaggle
* **Dataset no Kaggle:** AirQualityUCI
* **Ligação do dataset:** https://www.kaggle.com/datasets/jhonan/airqualityuci

### Dimensão dos Dados
* **Dimensão inicial de trabalho:** 9357 linhas e 15 colunas úteis, após limpeza estrutural inicial do ficheiro CSV

---

## 2. Exploração (Milestone 2)

### Limpeza e Preparação
Na fase de exploração e preparação dos dados foram desenvolvidas as seguintes etapas:

* Leitura do ficheiro CSV com `sep=';'` e `decimal=','`
* Remoção de colunas totalmente vazias e de linhas vazias no final do ficheiro
* Identificação do valor `-200` como código de valores em falta e conversão para `NaN`
* Criação da variável temporal `timestamp` a partir da junção de `Date` e `Time`
* Análise da percentagem de valores em falta por coluna
* Remoção da variável `NMHC(GT)` devido à elevada percentagem de *missing values*
* Remoção das linhas com `CO(GT)` em falta, por se tratar da variável-alvo
* Preenchimento dos restantes valores em falta com a mediana
* Verificação dos tipos de dados e tratamento inicial de outliers nas variáveis preditoras com base no método do IQR
* Aplicação de One-Hot Encoding às variáveis categóricas derivadas
* Aplicação de StandardScaler às variáveis numéricas contínuas preditoras
* Criação de novos atributos e seleção inicial de variáveis redundantes com base em multicolinearidade
* Exportação do dataset processado para ficheiro CSV
* Registo técnico e justificação das decisões em `docs/M2_exploracao.md`

### Principais Conclusões da Análise Exploratória

* O valor `-200` representa valores em falta e teve de ser convertido para `NaN` antes de qualquer análise estatística ou modelação.
* A variável `NMHC(GT)` apresentou uma percentagem muito elevada de valores em falta, o que justificou a sua remoção.
* As variáveis `C6H6(GT)` e `PT08.S2(NMHC)` revelaram correlações positivas muito fortes com `CO(GT)`, enquanto `PT08.S3(NOx)` evidenciou uma relação inversa forte.
* As variáveis meteorológicas `T`, `RH` e `AH` revelaram correlações fracas com a variável-alvo.
* O tratamento dos *missing values*, dos outliers e a criação de novos atributos deixaram o dataset preparado para a fase seguinte de modelação.

---

## 3. Modelação (Milestone 3)

### Abordagem Técnica
Na fase de modelação foi definida uma estratégia de avaliação rigorosa, com:

* divisão cronológica dos dados em **80% treino** e **20% teste**
* validação cruzada com **TimeSeriesSplit**
* utilização de um pipeline de pré-processamento para evitar *data leakage*
* comparação entre um modelo baseline e vários modelos candidatos
* otimização do melhor modelo com `GridSearchCV`

### Modelos Testados
Foram testados os seguintes modelos:

* **Baseline:** `DummyRegressor`
* **Regressão Linear**
* **Random Forest Regressor**
* **Gradient Boosting Regressor**
* **Gradient Boosting Regressor otimizado** com `GridSearchCV`

### Métricas de Avaliação
* **Métrica principal:** RMSE
* **Métricas complementares:** MAE e R²

### Modelo Final Escolhido
O modelo final selecionado foi o **Gradient Boosting otimizado**, por apresentar o melhor equilíbrio entre:

* **Desempenho**, com os melhores resultados no conjunto de teste
* **Estabilidade**, evidenciando melhor capacidade de generalização do que os restantes candidatos
* **Interpretabilidade**, permitindo análise através de curvas de aprendizagem, gráfico de resíduos, gráfico de valores reais versus previstos e importância dos atributos

### Desempenho Final do Modelo
No conjunto de teste, o modelo final obteve:

* **RMSE:** 0.4806
* **MAE:** 0.3210
* **R²:** 0.8722

### Principais Conclusões da Modelação
* O modelo **Gradient Boosting otimizado** superou claramente o baseline e os restantes candidatos.
* O **Random Forest** apresentou sinais de sobreajuste (*overfitting*).
* A **Regressão Linear** revelou desempenho inferior, sugerindo incapacidade para captar toda a complexidade das relações presentes nos dados.
* Os maiores erros continuam a ocorrer em valores extremos da variável `CO(GT)`, o que indica margem para melhoria futura.

As decisões metodológicas, os resultados detalhados e a análise crítica encontram-se documentados em `docs/M3_modelacao.md`.

---

## 4. Finalização (Milestone 4)

### Resposta ao Problema
O projeto demonstra que é possível prever a concentração de monóxido de carbono com um bom nível de precisão a partir de leituras de sensores e variáveis ambientais.

A solução desenvolvida permite não só comparar diferentes abordagens de modelação, como também identificar um modelo final com desempenho robusto e potencial de aplicação em contextos de monitorização e apoio à decisão.

### Recomendações de Inovação
1. Integrar o modelo num sistema de monitorização com alertas automáticos quando a previsão ultrapassar um limiar definido.
2. Explorar validação temporal mais avançada e atualização periódica do modelo, de forma a lidar com sazonalidade e possível deriva do conceito.
3. Criar variáveis adicionais, como indicadores temporais mais detalhados ou médias móveis, para melhorar a capacidade preditiva.
4. Reforçar a análise de erros extremos e explorar técnicas adicionais de otimização e interpretação do modelo.

---

## Como Reproduzir este Projeto
1. Clone o repositório: `git clone https://github.com/a2022138676/projeto-ciencia-dados-qualidade-ar.git`
2. Instale as dependências: `pip install -r requirements.txt`
3. Execute os notebooks na pasta `notebooks/`, seguindo a ordem numérica
4. Consulte os ficheiros na pasta `docs/` para acompanhar a evolução do projeto por Milestone
5. Verifique os gráficos exportados na pasta `reports/figures/`

---

## Referências
1. Vito, S. (2008). *Air Quality* [Dataset]. UCI Machine Learning Repository. https://doi.org/10.24432/C5060Z
2. Kaggle. *AirQualityUCI*. Disponível em: https://www.kaggle.com/datasets/jhonan/airqualityuci
3. Méndez, M., Merayo, M. G., & Núñez, M. (2023). *Machine learning algorithms to forecast air quality: a survey*.
4. Aula, K., Mäkelä, V., et al. (2022). *Evaluation of low-cost air quality sensor calibration models*.

**Instituição:** Coimbra Business School | ISCAC  
**Curso:** Licenciatura em Ciência de Dados para a Gestão  
**Unidade Curricular:** Projeto em Ciência de Dados  
**Professor Responsável:** Dora Melo (`dmelo@iscac.pt`)
