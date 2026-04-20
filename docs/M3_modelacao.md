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
  - RMSE: 1.3576  
  - MAE: 1.0831  
  - R²: -0.0196  

As métricas obtidas por este modelo constituem o referencial mínimo de desempenho. Assim, todos os modelos mais avançados deverão apresentar melhorias face a este baseline, especialmente em termos de redução do erro (RMSE e MAE) e aumento da capacidade explicativa (R²).

---

### 2.2. Modelos Candidatos

Foram testados diferentes algoritmos de regressão com o objetivo de superar o desempenho do modelo baseline.

Os modelos selecionados incluem abordagens lineares e baseadas em ensemble:

- Regressão Linear — modelo simples e interpretável  
- Random Forest — algoritmo baseado em múltiplas árvores de decisão  
- Gradient Boosting — modelo de ensemble com elevada capacidade preditiva  

#### Resultados obtidos

| Algoritmo | RMSE (Treino) | RMSE (Teste) | MAE (Teste) | R² (Teste) |
| :--- | :--- | :--- | :--- | :--- |
| Regressão Linear | 0.4968 | 0.7649 | 0.6174 | 0.6764 |
| Random Forest | 0.1345 | 0.5387 | 0.3571 | 0.8395 |
| Gradient Boosting | 0.3366 | 0.5071 | 0.3438 | 0.8578 |

#### Análise

Os resultados demonstram que todos os modelos testados superam significativamente o modelo baseline, evidenciando a capacidade dos algoritmos de machine learning em capturar padrões relevantes nos dados.

Os modelos baseados em ensemble, nomeadamente o **Random Forest** e o **Gradient Boosting**, destacaram-se pelo seu desempenho superior, apresentando menores valores de erro (RMSE e MAE) e maior capacidade explicativa (R²).

O modelo **Gradient Boosting** revelou-se o mais eficaz, apresentando o menor RMSE e o maior R² no conjunto de teste, indicando uma melhor capacidade de generalização.

O modelo **Random Forest** apresentou também um desempenho elevado, embora ligeiramente inferior ao Gradient Boosting. No entanto, a diferença significativa entre o erro de treino e de teste sugere possíveis sinais de **overfitting**.

Por outro lado, o modelo de **Regressão Linear** apresentou um desempenho inferior, sugerindo que as relações entre as variáveis não são exclusivamente lineares e que modelos mais complexos são mais adequados para este problema.

---

## 3. Otimização (Tuning)

Nesta fase não foi ainda realizada otimização de hiperparâmetros.

Esta etapa será desenvolvida após a identificação do modelo com melhor desempenho, com o objetivo de melhorar ainda mais os resultados obtidos.

---

## 4. Avaliação do Modelo Final

### 4.1. Matriz de Confusão / Análise de Erros

Não aplicável nesta fase, uma vez que ainda não foi selecionado um modelo final.

---

### 4.2. Importância dos Atributos (Feature Importance)

Não aplicável nesta fase.

A análise de importância dos atributos será realizada após o treino do modelo final.

---

## 5. Conclusão da Fase de Modelação

Até ao momento, foi definida a base metodológica da modelação e foram testados diferentes modelos de regressão.

Os resultados demonstram que modelos baseados em ensemble apresentam melhor desempenho face ao modelo baseline e ao modelo linear, destacando-se o Gradient Boosting como a melhor abordagem nesta fase.

O sistema encontra-se preparado para a fase seguinte, que consistirá na otimização do modelo selecionado e na sua avaliação final.

---

*Data de última atualização: 24/04/2026*
