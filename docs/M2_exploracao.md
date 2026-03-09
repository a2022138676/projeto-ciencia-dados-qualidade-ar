# Milestone 2: Análise Exploratória e Engenharia de Atributos

> **Nota de Revisão:** Este documento pressupõe que o dataset já foi identificado e descrito no ficheiro `docs/M1_iniciacao.md`. Caso seja necessário consultar o significado original das variáveis, deve consultar-se essa Milestone.

## 1. Análise Exploratória de Dados (EDA)

### 1.1. Distribuição da Variável Alvo

A variável-alvo definida para este projeto é **`CO(GT)`**, correspondente à concentração de monóxido de carbono medida por um método de referência. Como o objetivo do trabalho é um problema de **aprendizagem supervisionada por regressão**, foi importante analisar a distribuição desta variável antes da fase de modelação, de forma a compreender a sua dispersão, assimetria e a possível presença de valores extremos.

Para isso, foram utilizados **histogramas** e **boxplots**. O histograma foi escolhido por permitir observar a forma geral da distribuição da variável, enquanto o boxplot facilita a identificação de dispersão e de possíveis outliers. Esta escolha está de acordo com o que foi desenvolvido no notebook `1.0_eda_limpeza.ipynb`, garantindo ligação direta entre o código e a documentação.

Antes da análise, os valores `-200` foram convertidos para `NaN`, uma vez que neste dataset representam valores em falta e não medições reais. Esta decisão foi necessária para evitar que a distribuição da variável-alvo fosse distorcida por valores artificiais.

> **Factos importantes:**  
> - A variável `CO(GT)` é uma variável numérica contínua.  
> - Após a conversão de `-200` para `NaN`, a variável apresenta **7674 valores válidos**.  
> - A distribuição de `CO(GT)` mostra-se **assimétrica à direita**, com maior concentração de observações em valores mais baixos e presença de alguns valores elevados.  
> - O valor médio observado é aproximadamente **2,15**, enquanto a mediana é **1,80**, o que reforça a existência de assimetria positiva.  
> - O boxplot evidencia a presença de **valores extremos**, o que sugere a necessidade de atenção a outliers em etapas posteriores da preparação dos dados.

### 1.2. Correlações Relevantes

Após a análise univariada, foi realizada uma análise bivariada com o objetivo de identificar as variáveis com maior relação com a variável-alvo `CO(GT)`. Esta etapa é importante porque ajuda a perceber quais os atributos com maior potencial explicativo para os modelos de regressão da Milestone 3.

Para isso, foi gerada uma **matriz de correlação (heatmap)** com as variáveis numéricas e foram criados **scatter plots** para observar graficamente a relação entre os atributos e `CO(GT)`. O heatmap permite identificar relações lineares globais entre variáveis, enquanto os gráficos de dispersão ajudam a verificar a forma e intensidade dessas relações.

A análise realizada mostrou que as variáveis com maior associação a `CO(GT)` são, sobretudo, variáveis ligadas a outros poluentes e a sensores químicos. Em contraste, as variáveis meteorológicas apresentam correlação bastante mais fraca com a variável-alvo.

**Principais conclusões visuais:**

* **`C6H6(GT)` vs. `CO(GT)`:** foi observada uma **correlação positiva muito forte** (aproximadamente **0,93**), sugerindo que maiores concentrações de benzeno tendem a estar associadas a maiores concentrações de monóxido de carbono.
* **`PT08.S2(NMHC)` vs. `CO(GT)`:** verificou-se igualmente uma **correlação positiva muito forte** (aproximadamente **0,92**), o que indica que este sensor poderá ser bastante relevante para a previsão da variável-alvo.
* **`PT08.S1(CO)` vs. `CO(GT)`:** foi identificada uma **relação positiva forte** (aproximadamente **0,88**), o que é consistente com o facto de este sensor estar diretamente relacionado com medições de CO.
* **`PT08.S3(NOx)` vs. `CO(GT)`:** destacou-se uma **correlação negativa moderada a forte** (aproximadamente **-0,70**), indicando uma relação inversa entre estas variáveis.
* **`T`, `RH` e `AH` vs. `CO(GT)`:** as variáveis meteorológicas apresentaram **correlações fracas** com a variável-alvo, o que sugere menor capacidade explicativa isolada nesta fase da análise.

De forma geral, os gráficos indicam que os sensores químicos e algumas medições de poluentes têm maior relevância preditiva para `CO(GT)` do que as variáveis meteorológicas.

## 2. Qualidade dos Dados e Limpeza

### 2.1. Tratamento de Dados em Falta (Missing Data)

A qualidade dos dados foi analisada através da identificação de colunas vazias, valores em falta e inconsistências do ficheiro original. O dataset exigiu atenção especial porque os valores em falta não estavam inicialmente representados como `NaN`, surgindo sob a forma do valor **`-200`**.

As principais ações de limpeza efetuadas até ao momento foram:

- remoção de colunas totalmente vazias;
- substituição de `-200` por `NaN` nas variáveis numéricas;
- criação de uma tabela com o número e a percentagem de valores em falta por coluna.

Estas decisões foram tomadas para garantir que os dados utilizados nas fases seguintes representam medições reais e não códigos artificiais de ausência de valor.

* **Colunas afetadas:** `NMHC(GT)`, `CO(GT)`, `NO2(GT)`, `NOx(GT)`, `C6H6(GT)`, `PT08.S2(NMHC)`, `PT08.S3(NOx)`, `PT08.S1(CO)`, `T`, `RH`, `PT08.S4(NO2)`, `PT08.S5(O3)` e `AH`.
* **Estratégia adotada:** o valor `-200` foi substituído por `NaN`, porque não corresponde a uma medição válida e representa missing values no dataset original.

A análise da percentagem de valores em falta mostrou que:

- **`NMHC(GT)`** apresenta cerca de **90,23%** de valores em falta, sendo a variável mais problemática do conjunto de dados;
- **`CO(GT)`**, **`NO2(GT)`** e **`NOx(GT)`** apresentam cerca de **18%** de valores em falta;
- várias outras colunas apresentam aproximadamente **3,91%** de valores em falta.

Esta análise é importante porque fundamenta futuras decisões de imputação, exclusão de variáveis ou seleção de atributos, tal como exigido na Milestone 2. 

### 2.2. Outliers e Inconsistências

A identificação de outliers foi realizada com recurso a **boxplots**, por serem uma ferramenta adequada para a análise univariada de variáveis numéricas contínuas. Esta opção foi adotada porque permite observar rapidamente dispersão, mediana, amplitude interquartil e valores extremos.

Foram também identificadas algumas inconsistências estruturais no dataset original:

- existência de colunas finais totalmente vazias;
- presença de valores `-200` a representar ausência de medição;
- necessidade de combinar `Date` e `Time` numa variável temporal única;
- presença de valores extremos em várias variáveis numéricas.

Nesta fase, os outliers foram **identificados e documentados**, mas não eliminados automaticamente. Esta decisão foi tomada para evitar a remoção precipitada de observações que possam conter informação relevante para o problema. O tratamento mais aprofundado de outliers será efetuado em continuação da Milestone 2, com base no impacto real que estes valores possam ter na modelação.

## 3. Engenharia de Atributos (Feature Engineering)

### 3.1. Transformações Realizadas

A engenharia de atributos teve como objetivo tornar o dataset mais adequado para análise e futura modelação, melhorando a representação temporal dos dados e preparando as variáveis para algoritmos de aprendizagem supervisionada.

* **Encoding:** nesta fase não foi aplicado encoding categórico tradicional. Embora `Date` e `Time` sejam inicialmente variáveis não numéricas, estas representam informação temporal e foram tratadas através da sua conversão para uma variável temporal unificada, em vez de técnicas como One-Hot Encoding.
* **Escalonamento:** o escalonamento das variáveis numéricas ainda não foi aplicado nesta fase. Esta decisão deve-se ao facto de o foco atual estar centrado na análise exploratória, limpeza inicial e compreensão da estrutura dos dados. O escalonamento será avaliado antes do treino dos modelos, dependendo dos algoritmos selecionados.

### 3.2. Criação de Novos Atributos

Como forma de acrescentar valor ao dataset original, foi criada a variável **`timestamp`** a partir da combinação das colunas `Date` e `Time`. Esta transformação foi considerada relevante porque permite representar o momento da medição de forma adequada, facilitando futuras análises temporais e eventual criação de novas variáveis derivadas.

* **Nova Variável `timestamp`:** criada a partir da junção de `Date` e `Time`, permitindo representar corretamente a dimensão temporal de cada registo.

Além disso, a frequência das variáveis não numéricas `Date` e `Time` foi analisada para verificar a regularidade temporal dos registos. Observou-se que cada data tende a surgir com **24 registos**, o que é consistente com medições horárias.

Até ao momento, `timestamp` é a principal variável derivada criada no notebook. A criação de novos atributos adicionais, como `hora`, `dia da semana` ou `mês`, poderá ser considerada nas próximas etapas, desde que se justifique a sua relevância para a previsão de `CO(GT)`.

## 4. Dicionário de Dados Final (Pós-Processamento)

A tabela seguinte apresenta as variáveis consideradas após a fase inicial de limpeza e preparação.

| Atributo | Tipo | Descrição |
| :--- | :--- | :--- |
| `Date` | Object | Data original do registo |
| `Time` | Object | Hora original do registo |
| `timestamp` | Datetime | Variável temporal criada a partir de `Date` e `Time` |
| `CO(GT)` | Float | Variável-alvo: concentração de monóxido de carbono |
| `PT08.S1(CO)` | Float | Leitura do sensor relacionada com CO |
| `NMHC(GT)` | Float | Medição de hidrocarbonetos não metânicos; variável com elevada percentagem de missing values |
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

As colunas totalmente vazias presentes no ficheiro original foram removidas na fase inicial de limpeza, pelo que não integram o conjunto de dados preparado para continuação da análise.

## 5. Conclusões da Fase de Exploração

A fase de exploração permitiu compreender melhor a estrutura, distribuição e qualidade do dataset, aprofundando a análise iniciada no Milestone 1.

Em particular, foi possível concluir que:

- o dataset é constituído maioritariamente por variáveis numéricas contínuas, complementadas por duas variáveis temporais originais (`Date` e `Time`);
- a variável-alvo `CO(GT)` apresenta uma distribuição assimétrica, com concentração em valores mais baixos e presença de valores extremos;
- os sensores químicos e alguns poluentes, como `C6H6(GT)` e `PT08.S2(NMHC)`, apresentam relações bastante fortes com `CO(GT)`, o que reforça o seu potencial para a modelação;
- as variáveis meteorológicas apresentam correlação fraca com a variável-alvo, sugerindo menor relevância isolada;
- o dataset contém problemas significativos de qualidade, sobretudo devido à existência de valores em falta codificados como `-200`, com especial destaque para `NMHC(GT)`;
- a criação da variável `timestamp` melhorou a representação temporal dos dados e tornou a estrutura do conjunto de dados mais adequada para análises posteriores.

De forma geral, os dados apresentam qualidade suficiente para continuar para as próximas etapas da Milestone 2, desde que sejam concluídas as decisões de tratamento de missing values, análise mais detalhada de outliers, eventual criação de novos atributos e preparação final do dataset para a fase de modelação.

---

*Data de última atualização: 09/03/2026*
