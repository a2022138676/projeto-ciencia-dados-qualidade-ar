# Milestone 2: Análise Exploratória e Engenharia de Atributos

> **Nota de Revisão:** Este documento pressupõe que o dataset já foi identificado e descrito no ficheiro `docs/M1_iniciacao.md`. Caso seja necessário consultar o significado original das variáveis, deve consultar-se essa Milestone.

## 1. Análise Exploratória de Dados (EDA)

### 1.1. Distribuição da Variável Alvo

A variável-alvo definida para este projeto é **`CO(GT)`**, correspondente à concentração de monóxido de carbono medida por um método de referência. Como o objetivo do trabalho é um problema de **aprendizagem supervisionada por regressão**, foi importante analisar a distribuição desta variável antes da fase de modelação, de forma a compreender a sua dispersão, assimetria e eventual presença de valores extremos.

Para esta análise foram utilizados **histogramas** e **boxplots**. O histograma foi escolhido por permitir observar a forma geral da distribuição da variável, enquanto o boxplot facilita a identificação de dispersão, mediana e possíveis outliers. Esta escolha foi adequada porque `CO(GT)` é uma variável numérica contínua e estas visualizações são apropriadas para análise univariada.

Antes da análise, os valores `-200` foram convertidos para `NaN`, uma vez que neste dataset representam valores em falta e não medições reais. Esta decisão foi necessária para evitar que a distribuição da variável-alvo fosse artificialmente distorcida por valores inválidos.

> **Factos importantes:**  
> - `CO(GT)` é uma variável numérica contínua.  
> - A distribuição apresenta maior concentração de observações em valores mais baixos.  
> - Verifica-se assimetria positiva, com alguns valores mais elevados afastados da maioria dos registos.  
> - O boxplot evidencia a presença de possíveis outliers, o que justificou atenção posterior na fase de preparação dos dados.

### 1.2. Correlações Relevantes

Após a análise univariada, foi realizada uma análise bivariada com o objetivo de identificar as variáveis com maior relação com a variável-alvo `CO(GT)`. Para isso, foi gerada uma **matriz de correlação (heatmap)** e foram criados **gráficos de dispersão (scatter plots)** entre `CO(GT)` e os restantes atributos numéricos.

A utilização da matriz de correlação permitiu obter uma visão global das associações lineares entre variáveis, enquanto os gráficos de dispersão ajudaram a perceber a forma dessas relações, a sua intensidade e o grau de dispersão.

A análise visual permitiu retirar as seguintes conclusões principais:

* **`C6H6(GT)` vs. `CO(GT)`:** apresenta uma **correlação positiva muito forte**, sugerindo forte capacidade explicativa para a variável-alvo.
* **`PT08.S2(NMHC)` vs. `CO(GT)`:** apresenta também uma **correlação positiva muito forte**, confirmando que este sensor poderá ser particularmente relevante para a modelação.
* **`PT08.S1(CO)` vs. `CO(GT)`:** mostra uma **correlação positiva forte**, coerente com a natureza do sensor e com o comportamento esperado da variável.
* **`PT08.S5(O3)` vs. `CO(GT)`:** revela uma **correlação positiva forte**, com tendência crescente visualmente clara.
* **`NOx(GT)` vs. `CO(GT)`:** apresenta uma **correlação positiva significativa**, embora com maior dispersão.
* **`PT08.S3(NOx)` vs. `CO(GT)`:** destaca-se por uma **correlação negativa forte**, evidenciando uma relação inversa relevante.
* **`T`, `RH` e `AH` vs. `CO(GT)`:** as variáveis meteorológicas revelam **correlações fracas** com a variável-alvo, o que sugere menor capacidade explicativa isolada.

De forma geral, conclui-se que **os sensores químicos e os poluentes atmosféricos apresentam relações mais fortes com `CO(GT)` do que as variáveis meteorológicas**. Verificou-se também a existência de **multicolinearidade** entre algumas variáveis independentes, o que justificou a etapa posterior de seleção de atributos.

## 2. Qualidade dos Dados e Limpeza

### 2.1. Tratamento de Dados em Falta (Missing Data)

A qualidade dos dados foi analisada através da identificação de colunas vazias, valores em falta e inconsistências no ficheiro original. Verificou-se que o dataset inclui valores `-200`, que não correspondem a medições reais, mas sim a ausência de registo.

As principais decisões tomadas nesta fase foram as seguintes:

- remoção das colunas finais totalmente vazias;
- substituição do valor `-200` por `NaN`;
- criação de uma tabela com o número e a percentagem de valores em falta por variável;
- definição de uma estratégia de tratamento dos missing values.

Estas decisões foram justificadas pelo facto de `-200` ser um código artificial e não um valor válido de medição. Mantê-lo no dataset introduziria enviesamentos na análise estatística e na futura modelação.

A análise da percentagem de nulos mostrou que a variável **`NMHC(GT)`** apresentava uma percentagem extremamente elevada de valores em falta, o que comprometia a sua utilidade analítica. Perante este resultado, optou-se por **remover esta coluna**.

Relativamente à variável-alvo **`CO(GT)`**, as linhas com valores em falta foram removidas, pois não faz sentido imputar artificialmente a variável que se pretende prever.

Nas restantes variáveis numéricas com valores em falta, foi aplicada **imputação pela mediana**. Esta opção foi escolhida em vez da média porque várias variáveis apresentam outliers e distribuições assimétricas, sendo a mediana uma medida mais robusta e menos sensível a valores extremos.

* **Colunas afetadas:** várias variáveis numéricas apresentavam valores em falta codificados como `-200`, com especial destaque para `NMHC(GT)`, `CO(GT)`, `NO2(GT)` e `NOx(GT)`.
* **Estratégia adotada:** remoção da coluna `NMHC(GT)`, eliminação das linhas com `CO(GT)` em falta e preenchimento dos restantes missing values com a mediana.

Após a aplicação desta estratégia, **deixaram de existir valores em falta no conjunto de dados**, permitindo avançar para as fases seguintes com uma base de dados limpa e consistente.

### 2.2. Outliers e Inconsistências

Os **outliers** foram identificados com recurso ao método do **intervalo interquartil (IQR)**, por se tratar de uma abordagem robusta para variáveis numéricas contínuas. Esta opção permitiu quantificar o número e a percentagem de valores atípicos por variável, sem repetir em excesso os boxplots já utilizados na análise univariada.

Foi também realizada uma verificação dos tipos de dados do dataset, de forma a garantir que a variável `timestamp` se mantinha em formato temporal e que as restantes variáveis quantitativas estavam corretamente reconhecidas em formato numérico. Esta validação foi importante para assegurar consistência na preparação dos dados.

Foram identificadas as seguintes inconsistências e aspetos a corrigir:

- existência de colunas totalmente vazias no ficheiro original;
- presença do valor `-200` como código de missing values;
- necessidade de juntar `Date` e `Time` numa única variável temporal;
- presença de valores extremos em várias variáveis numéricas.

Como estratégia de tratamento, optou-se por aplicar **clipping** nas variáveis preditoras, limitando os valores aos intervalos definidos pelo IQR. Esta decisão permitiu reduzir o impacto de observações extremas sem eliminar registos completos do dataset.

A variável-alvo **`CO(GT)`** não foi alterada, uma vez que pode refletir episódios reais de poluição atmosférica e corresponde ao valor que se pretende prever.

## 3. Engenharia de Atributos (Feature Engineering)

### 3.1. Transformações Realizadas

A engenharia de atributos teve como objetivo tornar o dataset mais adequado à análise e à modelação futura, melhorando a representação temporal dos registos e preparando os dados para utilização em algoritmos de regressão.

* **Encoding:** Não foi aplicado encoding diretamente às colunas originais `Date` e `Time`, uma vez que estas representam informação temporal bruta e gerariam demasiadas categorias. Em vez disso, foi criada a variável `timestamp` e, a partir desta, foram extraídas variáveis temporais derivadas mais interpretáveis. Posteriormente, foi aplicado **One-Hot Encoding** às variáveis categóricas `day_of_week` e `month`, transformando os diferentes dias da semana e meses em colunas binárias. Esta opção foi escolhida por permitir representar categorias sem introduzir uma ordem artificial entre elas.

* **Escalonamento:** Foi aplicado **StandardScaler** às variáveis numéricas preditoras contínuas, com o objetivo de colocar os atributos numa escala comparável e reduzir o impacto de diferenças de magnitude entre variáveis. Esta transformação é relevante porque alguns algoritmos de modelação são sensíveis à escala dos atributos. A variável-alvo **`CO(GT)`** foi mantida na sua escala original, por corresponder ao valor que se pretende prever.

### 3.2. Criação de Novos Atributos

Como forma de acrescentar valor ao dataset original, foi criada a variável **`timestamp`** a partir da combinação das colunas `Date` e `Time`. Esta transformação foi considerada relevante porque permite representar o momento de cada medição de forma adequada, facilitando análises temporais e a criação de novos atributos mais úteis para a modelação.

Numa fase posterior, foram ainda criadas novas variáveis a partir das colunas já existentes no dataset transformado:

* **Nova Variável `is_weekend`:** variável binária criada a partir das colunas geradas pelo encoding do dia da semana, permitindo distinguir observações correspondentes a fins de semana.
* **Nova Variável `is_warm_season`:** variável binária criada a partir das colunas geradas pelo encoding do mês, com o objetivo de representar períodos mais quentes do ano.
* **Nova Variável `sensor_mean`:** variável contínua correspondente à média das leituras dos sensores químicos (`PT08.*`), funcionando como indicador agregado do comportamento dos sensores.

Estas variáveis foram consideradas relevantes por poderem captar padrões temporais e estruturais adicionais, indo além da informação diretamente representada nas colunas originais. Posteriormente, foi analisada a correlação destas novas variáveis com a variável-alvo `CO(GT)`, de forma a verificar se acrescentam informação útil para a modelação.

## 4. Dicionário de Dados Final (Pós-Processamento)

A tabela seguinte apresenta as principais variáveis consideradas após a fase de limpeza, transformação e preparação dos dados.

| Atributo | Tipo | Descrição |
| :--- | :--- | :--- |
| `CO(GT)` | Float | Variável-alvo: concentração de monóxido de carbono |
| `PT08.S1(CO)` | Float | Leitura do sensor relacionada com CO |
| `C6H6(GT)` | Float | Concentração de benzeno |
| `PT08.S2(NMHC)` | Float | Leitura do sensor relacionada com NMHC |
| `NOx(GT)` | Float | Concentração de óxidos de azoto |
| `PT08.S3(NOx)` | Float | Leitura do sensor relacionada com NOx |
| `NO2(GT)` | Float | Concentração de dióxido de azoto |
| `PT08.S4(NO2)` | Float | Leitura do sensor relacionada com NO2 |
| `PT08.S5(O3)` | Float | Leitura do sensor relacionada com O3 |
| `T` | Float | Temperatura |
| `RH` | Float | Humidade relativa |
| `AH` | Float | Humidade absoluta |
| `hour` | Float | Hora do dia, após transformação e escalonamento |
| `day_of_week_*` | Binária | Conjunto de colunas binárias resultantes do One-Hot Encoding do dia da semana |
| `month_*` | Binária | Conjunto de colunas binárias resultantes do One-Hot Encoding do mês |
| `is_weekend` | Binária | Variável binária que identifica fins de semana |
| `is_warm_season` | Binária | Variável binária que identifica meses mais quentes |
| `sensor_mean` | Float | Média das leituras dos sensores químicos |

As colunas totalmente vazias presentes no ficheiro original foram removidas na fase inicial de limpeza. A variável `NMHC(GT)` também foi removida devido à percentagem excessiva de valores em falta. As colunas `Date`, `Time` e `timestamp` deixaram de integrar o dataset final após a criação e transformação das variáveis temporais. Na etapa de seleção de atributos, foram ainda removidas as variáveis redundantes identificadas por apresentarem correlação absoluta demasiado elevada com outras variáveis preditoras.

## 5. Conclusões da Fase de Exploração

A fase de exploração permitiu compreender melhor a estrutura, distribuição e qualidade do dataset, aprofundando a análise iniciada no Milestone 1.

As principais conclusões desta fase foram as seguintes:

- o dataset é constituído maioritariamente por variáveis numéricas contínuas, complementadas inicialmente por variáveis temporais;
- a variável-alvo `CO(GT)` apresenta uma distribuição assimétrica, com maior concentração de valores baixos e presença de possíveis outliers;
- os atributos com maior relação com `CO(GT)` são sobretudo **sensores químicos e outros poluentes**, com destaque para `C6H6(GT)`, `PT08.S2(NMHC)`, `PT08.S1(CO)`, `PT08.S5(O3)` e `NOx(GT)`;
- a variável `PT08.S3(NOx)` apresenta uma relação inversa forte com `CO(GT)`, sendo uma das relações mais distintivas da análise;
- as variáveis meteorológicas (`T`, `RH` e `AH`) revelam baixa capacidade explicativa isolada para a previsão de `CO(GT)`;
- existiam problemas relevantes de qualidade dos dados, sobretudo associados a missing values codificados como `-200`, que foram devidamente tratados;
- a estratégia de tratamento de missing values permitiu eliminar os nulos do dataset final, mantendo a informação mais relevante para a modelação;
- a verificação dos tipos de dados e o tratamento dos outliers contribuíram para tornar o dataset mais consistente e menos sensível a observações extremas;
- a criação e transformação de atributos temporais, bem como a definição de variáveis derivadas adicionais, enriqueceram a representação dos dados;
- a seleção de atributos permitiu remover variáveis redundantes e reduzir problemas de multicolinearidade;
- o dataset processado foi exportado para ficheiro CSV, ficando preparado para a fase seguinte do projeto.

De forma geral, os dados apresentam qualidade suficiente para avançar para as próximas etapas do projeto, nomeadamente treino, comparação e avaliação de modelos preditivos.

---

*Data de última atualização: [25/03/2026]*
