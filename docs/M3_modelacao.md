# Milestone 3: Modelação e Avaliação

## 1. Estratégia de Modelação

Nesta fase foi definida a abordagem metodológica para preparação dos dados e avaliação dos modelos preditivos, com o objetivo de prever a concentração de monóxido de carbono (`CO(GT)`).

* **Divisão do dataset:**  
O conjunto de dados foi dividido em dois subconjuntos, utilizando **80% para treino** e **20% para teste**.  
Dado que o dataset possui uma componente temporal, a divisão foi realizada de forma **cronológica**, garantindo que o modelo é treinado com observações passadas e avaliado em observações futuras. Esta abordagem permite simular um cenário real de previsão e evitar fugas de informação (*data leakage*).

* **Métrica de Sucesso:**  
Tratando-se de um problema de regressão, foi escolhida como métrica principal o **RMSE (Root Mean Squared Error)**, por penalizar mais fortemente erros de maior magnitude.  
Como métricas complementares foram consideradas:
- **MAE (Mean Absolute Error)** — mede o erro médio absoluto  
- **R² (Coeficiente de determinação)** — indica a proporção da variabilidade explicada pelo modelo  

Adicionalmente, foi definido um pipeline de pré-processamento com o objetivo de garantir consistência na transformação dos dados e evitar fugas de informação. Este pipeline inclui:

- imputação de valores em falta com a mediana (variáveis numéricas)  
- tratamento de outliers com base no método do IQR  
- codificação de variáveis categóricas com One-Hot Encoding  
- escalonamento das variáveis numéricas com StandardScaler  

Todas estas transformações são ajustadas exclusivamente com base no conjunto de treino e posteriormente aplicadas ao conjunto de teste.

Para reforçar a robustez da avaliação, foi também definida uma estratégia de validação interna com `TimeSeriesSplit`, permitindo avaliar a estabilidade dos modelos ao longo do tempo.

---

## 2. Experiências Realizadas

### 2.1. Modelo Baseline

Como ponto de partida, foi utilizado um modelo simples de referência com o objetivo de estabelecer um patamar mínimo de desempenho.

* **Algoritmo:** `DummyRegressor` (strategy = "mean")  

Este modelo não utiliza as variáveis preditoras, limitando-se a prever sempre o valor médio da variável-alvo observada no conjunto de treino.

* **Resultado (Teste):**
  - RMSE: [1.3576]  
  - MAE: [1.0831]  
  - R²: [-0.0196]  

As métricas obtidas por este modelo constituem o referencial mínimo de desempenho. Assim, todos os modelos mais avançados deverão apresentar melhorias face a este baseline, especialmente em termos de redução do erro (RMSE e MAE) e aumento da capacidade explicativa (R²).

---

### 2.2. Modelos Candidatos

Ainda não foram testados modelos candidatos nesta fase do projeto.

A seleção e comparação de algoritmos de machine learning será realizada numa etapa posterior.

---

## 3. Otimização (Tuning)

Nesta fase não foi realizada otimização de hiperparâmetros, uma vez que ainda não foram treinados modelos candidatos.

Esta etapa será desenvolvida após a implementação dos primeiros modelos de regressão.

---

## 4. Avaliação do Modelo Final

### 4.1. Matriz de Confusão / Análise de Erros

Não aplicável nesta fase, uma vez que ainda não foi selecionado um modelo final.

---

### 4.2. Importância dos Atributos (Feature Importance)

Não aplicável nesta fase.

A análise de importância dos atributos será realizada após o treino dos modelos candidatos.

---

## 5. Conclusão da Fase de Modelação

Até ao momento, foi definida a base metodológica da modelação, incluindo:

- partição dos dados em treino e teste com abordagem temporal  
- definição de métricas de avaliação adequadas ao problema de regressão  
- construção de um pipeline de pré-processamento sem fuga de informação  
- definição de estratégia de validação interna  
- implementação do modelo baseline  

O sistema encontra-se preparado para a fase seguinte, que consistirá no treino, comparação e avaliação de modelos de regressão mais avançados.

---

*Data de última atualização: 24/04/2026*
