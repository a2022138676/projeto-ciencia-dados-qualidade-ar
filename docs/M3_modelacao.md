# Milestone 3: Modelação e Avaliação

## 1. Estratégia de Modelação

Nesta fase inicial da modelação foi definida a abordagem metodológica para preparação dos dados e avaliação dos modelos preditivos, tendo em vista a previsão da variável `CO(GT)`.

### Divisão do dataset

O conjunto de dados foi dividido em dois subconjuntos:

- 80% para treino  
- 20% para teste  

Dado que o dataset possui uma componente temporal, a divisão foi realizada de forma cronológica, garantindo que o modelo é treinado com observações passadas e avaliado em observações futuras. Esta abordagem permite simular um cenário real de previsão e evitar fugas de informação (*data leakage*).

### Métrica de Sucesso

Tratando-se de um problema de regressão, foram selecionadas as seguintes métricas de avaliação:

- **RMSE (Root Mean Squared Error)** — métrica principal, por penalizar mais fortemente erros de maior magnitude  
- **MAE (Mean Absolute Error)** — mede o erro médio absoluto  
- **R² (Coeficiente de determinação)** — indica a proporção da variabilidade explicada pelo modelo  

Estas métricas permitem avaliar diferentes dimensões do desempenho dos modelos.

### Preparação dos Dados

Foi definido um pipeline de pré-processamento com o objetivo de garantir consistência na transformação dos dados e evitar fugas de informação. Este pipeline inclui:

- imputação de valores em falta com a mediana (variáveis numéricas)  
- tratamento de outliers com base no método do IQR  
- codificação de variáveis categóricas com One-Hot Encoding  
- escalonamento das variáveis numéricas com StandardScaler  

Todas estas transformações são ajustadas exclusivamente com base no conjunto de treino e posteriormente aplicadas ao conjunto de teste.

Adicionalmente, foi definida uma estratégia de validação interna com `TimeSeriesSplit`, permitindo avaliar a estabilidade dos modelos ao longo do tempo.

---

## 2. Experiências Realizadas

### 2.1. Modelo Baseline

Nesta fase ainda não foram implementados modelos preditivos, encontrando-se o trabalho focado na definição da estratégia de avaliação e preparação dos dados.

A implementação do modelo baseline será realizada na etapa seguinte da modelação.

---

### 2.2. Modelos Candidatos

Ainda não foram testados modelos candidatos nesta fase do projeto.

A seleção e comparação de algoritmos de machine learning será realizada numa etapa posterior.

---

## 3. Otimização (Tuning)

Nesta fase não foi realizada otimização de hiperparâmetros, uma vez que ainda não foram treinados modelos.

Esta etapa será desenvolvida após a implementação dos modelos candidatos.

---

## 4. Avaliação do Modelo Final

### 4.1. Análise de Erros

Não aplicável nesta fase, uma vez que ainda não foram treinados modelos.

---

### 4.2. Importância dos Atributos (Feature Importance)

Não aplicável nesta fase.

A análise de importância dos atributos será realizada após o treino dos modelos.

---

## 5. Conclusão da Fase de Modelação

Nesta fase foi definida a base metodológica para a modelação, incluindo:

- divisão dos dados em treino e teste com abordagem temporal  
- definição de métricas de avaliação adequadas ao problema de regressão  
- construção de um pipeline de pré-processamento sem fuga de informação  
- definição de estratégia de validação interna  

O sistema encontra-se preparado para a fase seguinte, que consistirá na implementação de modelos preditivos e avaliação do seu desempenho.

---

*Data de última atualização: 24/04/2026*
