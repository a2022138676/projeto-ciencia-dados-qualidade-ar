# Milestone 3: Modelação e Avaliação

## 1. Estratégia de Modelação

Nesta fase inicial da modelação foi definida a abordagem metodológica para preparação dos dados e avaliação dos modelos preditivos, tendo em vista a previsão da variável `CO(GT)`.

* **Divisão do dataset:** O conjunto de dados foi dividido em dois subconjuntos, utilizando **80% para treino** e **20% para teste**. Dado que o dataset possui uma componente temporal, a divisão foi realizada de forma **cronológica**, garantindo que o modelo é treinado com observações passadas e avaliado em observações futuras. Esta abordagem permite simular um cenário real de previsão e evitar fugas de informação (*data leakage*).

* **Métrica de Sucesso:** Tratando-se de um problema de regressão, foi escolhida como métrica principal o **RMSE (Root Mean Squared Error)**, por penalizar mais fortemente erros de maior magnitude. Como métricas complementares foram ainda consideradas o **MAE (Mean Absolute Error)**, que permite interpretar o erro médio absoluto, e o **R² (Coeficiente de determinação)**, que indica a proporção da variabilidade explicada pelo modelo.

Adicionalmente, foi definido um pipeline de pré-processamento com o objetivo de garantir consistência na transformação dos dados e evitar fugas de informação. Este pipeline inclui imputação de valores em falta com a mediana nas variáveis numéricas, tratamento de outliers com base no método do IQR, codificação de variáveis categóricas com One-Hot Encoding e escalonamento das variáveis numéricas com StandardScaler. Todas estas transformações são ajustadas exclusivamente com base no conjunto de treino e posteriormente aplicadas ao conjunto de teste.

Para reforçar a robustez da avaliação, foi também definida uma estratégia de validação interna com `TimeSeriesSplit`, permitindo avaliar a estabilidade dos modelos ao longo do tempo.

## 2. Experiências Realizadas

### 2.1. Modelo Baseline

Como ponto de partida, foi utilizado um modelo simples de referência com o objetivo de estabelecer um patamar mínimo de desempenho.

* **Algoritmo:** `DummyRegressor` com estratégia baseada na média (`strategy="mean"`)

* **Resultado:** As métricas obtidas pelo modelo baseline foram registadas no notebook de modelação e servirão de base comparativa para os modelos mais avançados a testar nas fases seguintes. Nesta etapa, o objetivo principal foi estabelecer um referencial mínimo de desempenho, e não maximizar a capacidade preditiva.

Este modelo não utiliza as variáveis preditoras, limitando-se a prever sempre o valor médio da variável-alvo observada no conjunto de treino. Assim, qualquer modelo candidato considerado adequado deverá apresentar um desempenho superior ao do baseline, sobretudo em termos de RMSE e MAE.

### 2.2. Modelos Candidatos

Ainda não foram testados modelos candidatos nesta fase do projeto.

A seleção e comparação de algoritmos de machine learning será realizada numa etapa posterior.

## 3. Otimização (Tuning)

Nesta fase não foi realizada otimização de hiperparâmetros, uma vez que ainda não foram treinados modelos candidatos.

Esta etapa será desenvolvida após a implementação e comparação dos primeiros algoritmos de regressão.

## 4. Avaliação do Modelo Final

### 4.1. Matriz de Confusão / Erros

Não aplicável nesta fase, uma vez que ainda não foi selecionado um modelo final.

### 4.2. Importância dos Atributos (Feature Importance)

Não aplicável nesta fase.

A análise de importância dos atributos será realizada após o treino dos modelos candidatos.

## 5. Conclusão da Fase de Modelação

Até ao momento, foi definida a base metodológica da modelação, incluindo a partição dos dados, a estratégia de validação, as métricas de avaliação e a implementação do modelo baseline.

O sistema encontra-se preparado para a fase seguinte, que consistirá no treino, comparação e avaliação de modelos de regressão mais avançados.

---

*Data de última atualização: 24/04/2026*
