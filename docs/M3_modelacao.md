# Milestone 3: Modelação e Avaliação

## 1. Estratégia de Modelação

Nesta fase foram preparados os dados e definida a metodologia de avaliação para os modelos preditivos, com o objetivo de prever a concentração de monóxido de carbono (`CO(GT)`).

* **Divisão do dataset:**  
Foi utilizada uma divisão de **80% para treino** e **20% para teste**.  
Dado que o dataset possui uma componente temporal, a divisão foi realizada de forma **cronológica**, garantindo que o modelo é treinado com observações passadas e avaliado em observações futuras.

Esta abordagem permite simular um cenário real de previsão e assegura o isolamento dos dados de teste, evitando fugas de informação (*data leakage*).

Adicionalmente, foi utilizada validação cruzada com `TimeSeriesSplit` no conjunto de treino, garantindo maior robustez dos resultados e reduzindo a dependência de uma única divisão dos dados. Desta forma, as conclusões obtidas não dependem apenas de uma partição “afortunada”, mas de um processo mais estável e repetível.

Antes do treino, foi ainda definido um pipeline de pré-processamento com o objetivo de garantir consistência na transformação dos dados. Este pipeline inclui:

- imputação de valores em falta com a mediana nas variáveis numéricas  
- tratamento de outliers com base no método do IQR  
- codificação de variáveis categóricas com One-Hot Encoding  
- escalonamento das variáveis numéricas com StandardScaler  

Todas estas transformações são ajustadas exclusivamente com base no conjunto de treino e posteriormente aplicadas ao conjunto de teste.

* **Métrica de Sucesso:**  
Tratando-se de um problema de regressão, foi escolhida como métrica principal o **RMSE (Root Mean Squared Error)**.

O RMSE foi privilegiado em detrimento do MAE por penalizar mais fortemente erros de maior magnitude, o que é particularmente relevante neste contexto, uma vez que falhas maiores podem corresponder a previsões incorretas em situações de concentração mais elevada de poluição atmosférica. Assim, esta métrica mede de forma mais adequada o sucesso do objetivo definido no Milestone 1: prever com rigor a concentração de `CO(GT)`.

Como métricas complementares foram utilizadas:

- **MAE (Mean Absolute Error)** — permite interpretar diretamente o erro médio em unidades da variável-alvo  
- **R² (Coeficiente de determinação)** — avalia a capacidade explicativa do modelo  

Esta combinação permite avaliar simultaneamente precisão, robustez e qualidade global das previsões.

## 2. Experiências Realizadas

### 2.1. Modelo Baseline

Como ponto de partida, foi utilizado um modelo simples de referência.

* **Algoritmo:** `DummyRegressor` (`strategy="mean"`)

Este modelo prevê sempre o valor médio da variável-alvo, não utilizando qualquer informação das variáveis preditoras.

* **Resultado:**  
- RMSE: **1.3576**  
- MAE: **1.0831**  
- R²: **-0.0196**

Este modelo define o nível mínimo de desempenho esperado, sendo utilizado como base de comparação para os restantes modelos. A utilização de um baseline permite avaliar se a complexidade adicional dos modelos candidatos produz, de facto, ganhos estatísticos e práticos.

### 2.2. Modelos Candidatos

Foram testados diferentes algoritmos de regressão com o objetivo de superar o desempenho do baseline.

A seleção dos modelos teve em conta a diversidade de abordagens e a sua adequação ao problema:

- **modelo linear** (*Regressão Linear*), como referência simples e interpretável  
- **modelos de ensemble** (*Random Forest* e *Gradient Boosting*), por serem capazes de capturar relações não lineares e interações complexas entre variáveis  

| Algoritmo | Parâmetros Base | Métrica (Treino) | Métrica (Teste) | Notas |
| :--- | :--- | :--- | :--- | :--- |
| Regressão Linear | `default` | RMSE = 0.4968 | RMSE = 0.7649 | Indícios de underfitting |
| Random Forest | `n_estimators=100` | RMSE = 0.1345 | RMSE = 0.5387 | Evidência de overfitting |
| Gradient Boosting | `default` | RMSE = 0.3366 | RMSE = 0.5071 | Melhor capacidade de generalização |

Os resultados demonstram que todos os modelos superam significativamente o baseline, evidenciando que a utilização de algoritmos de machine learning acrescenta valor real ao problema.

Os modelos baseados em ensemble apresentaram melhor desempenho face ao modelo linear, o que sugere que as relações entre as variáveis não são puramente lineares.

O modelo **Gradient Boosting** destacou-se como o melhor, apresentando o menor erro no conjunto de teste e o melhor equilíbrio entre desempenho de treino e de teste, revelando maior capacidade de generalização.

O modelo **Random Forest** apresentou desempenho muito forte no treino, mas com degradação no teste, o que constitui evidência de **overfitting**.

Já a **Regressão Linear** apresentou desempenho inferior aos modelos de ensemble, sugerindo **underfitting parcial**, ou seja, capacidade limitada para capturar a complexidade do fenómeno em estudo.

Comparativamente ao baseline, a maior complexidade dos modelos candidatos trouxe benefícios estatísticos claros, justificando o custo computacional adicional.

## 3. Otimização (Tuning)

Nesta fase não foi ainda realizada otimização de hiperparâmetros.

A escolha do modelo foi baseada na sua capacidade de generalização, tendo sido identificado o **Gradient Boosting** como o melhor candidato para otimização futura.

Como trabalho seguinte, prevê-se a utilização de técnicas como **GridSearchCV** ou **RandomizedSearchCV** para ajuste de parâmetros como:

- número de estimadores  
- taxa de aprendizagem  
- profundidade das árvores  

Espera-se que esta etapa permita melhorar ainda mais o desempenho do modelo selecionado, mantendo o equilíbrio entre erro de treino e erro de teste.

## 4. Avaliação do Modelo Final

### 4.1. Matriz de Confusão / Erros

Tratando-se de um problema de regressão, a avaliação foi feita com base na análise dos erros e resíduos (diferença entre valores reais e previstos), bem como na comparação entre desempenho de treino e de teste.

> **Análise:**  
Verificou-se que os maiores erros se concentram nos valores extremos da variável `CO(GT)`, indicando maior dificuldade dos modelos em prever situações de elevada variabilidade na qualidade do ar.

A comparação entre treino e teste revelou que:

- o **Random Forest** apresenta sinais claros de sobreajuste, com erro muito reduzido no treino e superior no teste;  
- o **Gradient Boosting** apresenta melhor equilíbrio entre treino e teste, sendo o modelo com melhor capacidade de generalização;  
- a **Regressão Linear** apresenta desempenho mais fraco em ambos os conjuntos, sugerindo capacidade preditiva insuficiente para modelar a complexidade dos dados.  

Foram ainda geradas **curvas de aprendizagem** para o modelo Gradient Boosting, permitindo analisar a evolução do erro à medida que o número de observações aumenta. Estas curvas sugerem comportamento estável e reforçam a ideia de que este modelo generaliza melhor do que os restantes candidatos, embora ainda possa beneficiar de otimização adicional e, eventualmente, de mais dados.

### 4.2. Importância dos Atributos (Feature Importance)

Nesta fase não foi ainda realizada uma análise formal de importância dos atributos com base no modelo final.

No entanto, com base na análise exploratória desenvolvida no Milestone 2, é expectável que variáveis relacionadas com sensores químicos e poluentes atmosféricos — como `C6H6(GT)`, `PT08.S2(NMHC)` e `PT08.S1(CO)` — tenham relevância elevada na previsão da variável-alvo.

A análise formal da importância dos atributos será desenvolvida na continuação da modelação, garantindo coerência entre os resultados do relatório e o notebook.

## 5. Conclusão da Fase de Modelação

Os resultados obtidos demonstram que é possível prever a concentração de monóxido de carbono com bom nível de precisão utilizando modelos de machine learning.

O modelo **Gradient Boosting** revelou-se o mais adequado nesta fase, apresentando o melhor compromisso entre erro e capacidade de generalização.

A comparação com o modelo baseline evidenciou melhorias significativas, justificando a utilização de modelos mais complexos. Em termos práticos, a complexidade adicional dos modelos de ensemble traduziu-se em ganhos reais de desempenho.

Apesar dos bons resultados, foram identificadas limitações na previsão de valores extremos, o que indica margem para melhoria futura através de otimização de hiperparâmetros e análise mais aprofundada dos erros.

De forma geral, o modelo encontra-se suficientemente robusto para avançar para a fase seguinte de otimização e refinamento, mantendo coerência entre o relatório e o notebook `2.0_modelacao_treino.ipynb`.

---

*Data de última atualização: 22/04/2026*
