# Milestone 3: Modelação e Avaliação

## 1. Estratégia de Modelação

Nesta fase foram preparados os dados e definida a metodologia de avaliação para os modelos preditivos, com o objetivo de prever a concentração de monóxido de carbono (`CO(GT)`).

* **Divisão do dataset:**  
Foi utilizada uma divisão de **80% para treino** e **20% para teste**.  
Dado que o dataset possui uma componente temporal, a divisão foi realizada de forma **cronológica**, garantindo que o modelo é treinado com observações passadas e avaliado em observações futuras.  

Esta abordagem permite simular um cenário real de previsão e assegura o isolamento dos dados de teste, evitando fugas de informação (*data leakage*).

Adicionalmente, foi utilizada validação cruzada com `TimeSeriesSplit` no conjunto de treino, garantindo maior robustez dos resultados e reduzindo a dependência de uma única divisão dos dados.

* **Métrica de Sucesso:**  
Tratando-se de um problema de regressão, foi escolhida como métrica principal o **RMSE (Root Mean Squared Error)**.

O RMSE foi privilegiado por penalizar mais fortemente erros de maior magnitude, o que é relevante neste contexto, uma vez que erros elevados podem representar falhas na previsão de níveis críticos de poluição.

Como métricas complementares foram utilizadas:

- **MAE (Mean Absolute Error)** — permite interpretar diretamente o erro médio  
- **R² (Coeficiente de determinação)** — avalia a capacidade explicativa do modelo  

Esta combinação permite avaliar simultaneamente precisão, robustez e qualidade global das previsões.

---

## 2. Experiências Realizadas

### 2.1. Modelo Baseline

Como ponto de partida, foi utilizado um modelo simples de referência.

* **Algoritmo:** DummyRegressor (strategy = "mean")  

Este modelo prevê sempre o valor médio da variável-alvo, não utilizando qualquer informação das variáveis preditoras.

* **Resultado:**
- RMSE: 1.3576  
- MAE: 1.0831  
- R²: -0.0196  

Este modelo define o nível mínimo de desempenho esperado, sendo utilizado como base de comparação para os restantes modelos.

---

### 2.2. Modelos Candidatos

Foram testados diferentes algoritmos de regressão com o objetivo de superar o desempenho do baseline.

A seleção dos modelos teve em conta a diversidade de abordagens:

- modelos lineares (Regressão Linear)  
- modelos de ensemble (Random Forest e Gradient Boosting)  

| Algoritmo | Parâmetros Base | Métrica (Treino - RMSE) | Métrica (Teste - RMSE) | Notas |
| :--- | :--- | :--- | :--- | :--- |
| Regressão Linear | default | 0.4968 | 0.7649 | Underfitting parcial |
| Random Forest | n_estimators=100 | 0.1345 | 0.5387 | Sinais de overfitting |
| Gradient Boosting | default | 0.3366 | 0.5071 | Melhor generalização |

### Análise

Os resultados demonstram que todos os modelos superam significativamente o baseline, evidenciando a capacidade dos algoritmos em capturar padrões nos dados.

O modelo **Gradient Boosting** destacou-se como o melhor, apresentando o menor erro no conjunto de teste e a melhor capacidade de generalização.

O modelo **Random Forest** apresentou um desempenho elevado no treino, mas com degradação no teste, indicando sinais de **overfitting**.

O modelo de **Regressão Linear** apresentou resultados inferiores, sugerindo que as relações entre as variáveis não são puramente lineares.

A maior complexidade dos modelos de ensemble traduziu-se em ganhos reais de desempenho, justificando o seu uso face ao modelo baseline.

---

## 3. Otimização (Tuning)

Nesta fase não foi ainda realizada otimização de hiperparâmetros.

A escolha do modelo foi baseada na sua capacidade de generalização, tendo sido identificado o **Gradient Boosting** como o melhor candidato para otimização futura.

Como trabalho futuro, prevê-se a utilização de técnicas como **GridSearchCV** para ajuste de parâmetros como:

- número de estimadores  
- taxa de aprendizagem  
- profundidade das árvores  

---

## 4. Avaliação do Modelo Final

### 4.1. Matriz de Confusão / Erros

Tratando-se de um problema de regressão, foi realizada análise de erros com base nos resíduos (diferença entre valores reais e previstos).

> **Análise:**  
Os maiores erros concentram-se em valores extremos da variável `CO(GT)`, indicando maior dificuldade do modelo em prever situações de elevada variabilidade na qualidade do ar.

A comparação entre treino e teste revelou que:

- o Random Forest apresenta sobreajuste  
- o Gradient Boosting apresenta melhor equilíbrio  
- o modelo Linear apresenta menor capacidade preditiva  

---

### 4.2. Importância dos Atributos (Feature Importance)

Ainda não foi realizada uma análise formal de importância dos atributos nesta fase.

No entanto, com base na análise exploratória, espera-se que variáveis relacionadas com sensores químicos tenham maior relevância na previsão.

---

## 5. Conclusão da Fase de Modelação

Os resultados obtidos demonstram que é possível prever a concentração de monóxido de carbono com elevada precisão utilizando modelos de machine learning.

O modelo **Gradient Boosting** revelou-se o mais adequado, apresentando o melhor compromisso entre erro e capacidade de generalização.

A comparação com o modelo baseline evidenciou melhorias significativas, justificando a utilização de modelos mais complexos.

Apesar dos bons resultados, foram identificadas limitações na previsão de valores extremos, indicando potencial para melhorias futuras.

O modelo encontra-se adequado para continuação do processo, nomeadamente na fase de otimização e validação final.

---

*Data de última atualização: 21/04/2026*
