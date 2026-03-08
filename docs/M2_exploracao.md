# Milestone 2: Análise Exploratória e Engenharia de Atributos

> **Nota de Revisão:** Este documento pressupõe que o dataset já foi identificado e descrito no ficheiro `docs/M1_iniciacao.md`. Caso seja necessário consultar o significado original das variáveis, deve consultar-se essa Milestone.

## 1. Análise Exploratória de Dados (EDA)

### 1.1. Distribuição da Variável Alvo

A variável-alvo definida para este projeto é **`CO(GT)`**, correspondente à concentração de monóxido de carbono medida por um método de referência. Como o objetivo do trabalho é um problema de **aprendizagem supervisionada por regressão**, foi importante analisar a distribuição desta variável antes da fase de modelação, de forma a compreender a sua dispersão, assimetria e eventual presença de valores extremos.

Para isso, foram utilizados **histogramas** e **boxplots**. A escolha do histograma justifica-se por permitir observar a forma da distribuição da variável, enquanto o boxplot ajuda a identificar a dispersão dos valores e possíveis outliers. Esta escolha está alinhada com o que foi desenvolvido no notebook `1.0_eda_limpeza.ipynb`, garantindo coerência entre código e documentação.

Antes da análise, os valores `-200` foram convertidos para `NaN`, uma vez que neste dataset representam valores em falta e não medições reais. Esta decisão foi necessária para evitar que a distribuição da variável-alvo fosse distorcida por valores artificiais.

> **Factos importantes:**  
> - A variável `CO(GT)` é uma variável numérica contínua.  
> - A análise gráfica mostrou que a distribuição de `CO(GT)` é **[preencher: ex. assimétrica à direita / relativamente dispersa / concentrada em valores mais baixos]**.  
> - O boxplot evidenciou **[preencher: ex. presença de outliers / amplitude elevada / concentração central dos valores]**.  
> - Estes resultados sugerem que **[preencher: ex. poderá ser necessário ter atenção a valores extremos na fase de modelação]**.

### 1.2. Correlações Relevantes

Após a análise univariada, foi realizada uma análise bivariada com o objetivo de identificar as variáveis com maior relação com a variável-alvo `CO(GT)`. Esta etapa é importante porque ajuda a perceber quais os atributos que poderão contribuir mais para o desempenho preditivo dos modelos de regressão na Milestone 3.

Para isso, foram geradas visualizações como **matriz de correlação** e **gráficos de dispersão**, permitindo avaliar a força e o sentido da relação entre `CO(GT)` e os restantes atributos numéricos. Estas escolhas metodológicas são adequadas porque o dataset é composto maioritariamente por variáveis numéricas contínuas.

Com base na análise realizada no notebook, verificou-se que:

* **Atributo [preencher] vs. Alvo:** [preencher com a observação real retirada do heatmap/scatter plot].
* **Atributo [preencher] vs. Alvo:** [preencher com a observação real retirada do heatmap/scatter plot].
* **Atributo [preencher] vs. Alvo:** [preencher com a observação real retirada do heatmap/scatter plot].

De forma geral, esta análise permitiu identificar quais as variáveis com maior potencial explicativo para prever `CO(GT)` e quais poderão ser menos relevantes ou redundantes.

## 2. Qualidade dos Dados e Limpeza

### 2.1. Tratamento de Dados em Falta (Missing Data)

A qualidade dos dados foi analisada através da identificação de valores em falta, colunas vazias e inconsistências de leitura do ficheiro original. O dataset exigiu alguns cuidados específicos, uma vez que os valores em falta não surgem imediatamente como `NaN`, estando codificados como `-200`.

As principais transformações realizadas foram as seguintes:

- remoção das colunas finais totalmente vazias (`Unnamed: 15` e `Unnamed: 16`);
- conversão do código `-200` para `NaN`;
- verificação da percentagem de valores em falta por coluna;
- preparação da base para decisões posteriores de imputação ou exclusão de variáveis.

Estas decisões foram tomadas para garantir que os dados utilizados na fase de modelação representam observações reais e não valores artificiais.

* **Colunas afetadas:** `CO(GT)`, `NMHC(GT)`, `C6H6(GT)`, `NOx(GT)`, `NO2(GT)`, `T`, `RH`, `AH` e outras colunas com valores `-200`, conforme identificado no notebook.  
* **Estratégia adotada:** os valores `-200` foram substituídos por `NaN`, porque representam ausência de medição. Esta estratégia é mais correta do que manter esse valor, uma vez que `-200` não corresponde a uma leitura válida da qualidade do ar.

Além disso, verificou-se que a variável **`NMHC(GT)`** apresenta **[preencher: ex. percentagem muito elevada de valores em falta]**, o que poderá justificar tratamento específico ou eventual exclusão em fases posteriores, caso se conclua que a sua utilidade preditiva é reduzida face à quantidade de dados ausentes.

### 2.2. Outliers e Inconsistências

A identificação de outliers foi feita com recurso a boxplots, uma vez que esta visualização permite observar rapidamente valores extremos e dispersão. Esta escolha foi preferida a outras formas de visualização por ser mais adequada para variáveis numéricas contínuas e para análise univariada.

Foram também identificadas inconsistências estruturais no dataset original, nomeadamente:

- existência de colunas totalmente vazias;
- presença de valores `-200` a representar missing values;
- necessidade de combinar `Date` e `Time` numa variável temporal única.

No caso dos outliers, a análise inicial permitiu observar que **[preencher: ex. algumas variáveis apresentam valores bastante afastados da mediana]**. Nesta fase, os valores extremos foram **identificados e documentados**, ficando a decisão de tratamento mais detalhado para a continuação da Milestone 2, de forma a não eliminar informação potencialmente relevante sem análise adicional.

## 3. Engenharia de Atributos (Feature Engineering)

### 3.1. Transformações Realizadas

A engenharia de atributos teve como objetivo tornar o dataset mais adequado para a futura modelação, melhorando a interpretação temporal dos dados e preparando as variáveis para algoritmos de aprendizagem supervisionada.

* **Encoding:** O dataset original não possui variáveis categóricas clássicas que exijam aplicação de técnicas como One-Hot Encoding. As únicas variáveis não numéricas identificadas foram `Date` e `Time`, que representam informação temporal e, por isso, foram tratadas através da sua conversão para uma variável temporal unificada, em vez de encoding categórico tradicional.

* **Escalonamento:** O escalonamento das variáveis numéricas **[preencher: ex. ainda não foi aplicado nesta fase / será realizado antes do treino dos modelos]**. Esta decisão deve-se ao facto de o foco atual estar centrado na análise exploratória, limpeza e preparação estrutural dos dados. No entanto, algoritmos sensíveis à escala poderão beneficiar de normalização ou standardização na fase de modelação.

### 3.2. Criação de Novos Atributos

Como forma de acrescentar valor ao dataset original, foi criada a variável **`timestamp`** a partir da junção das colunas `Date` e `Time`. Esta transformação foi considerada relevante porque permite representar o momento de medição de forma mais adequada, facilitando análises temporais e a futura criação de atributos derivados.

* **Nova Variável `timestamp`:** criada a partir da combinação de `Date` e `Time`, permitindo representar corretamente a dimensão temporal de cada registo.

Caso tenham sido criadas mais variáveis no notebook, podem acrescentar aqui, por exemplo:

* **Nova Variável `hour`:** extraída de `timestamp`, permitindo captar variações horárias na concentração dos poluentes.  
* **Nova Variável `month`:** extraída de `timestamp`, permitindo observar possíveis padrões sazonais.  
* **Nova Variável `day_of_week`:** extraída de `timestamp`, permitindo analisar diferenças entre dias da semana.

Estas variáveis são relevantes porque ajudam a traduzir informação temporal bruta em atributos potencialmente úteis para os modelos preditivos.

## 4. Dicionário de Dados Final (Pós-Processamento)

A tabela seguinte apresenta as principais variáveis consideradas após a fase inicial de limpeza e preparação dos dados.

| Atributo | Tipo | Descrição |
| :--- | :--- | :--- |
| `Date` | Object | Data original do registo; usada para criar `timestamp` |
| `Time` | Object | Hora original do registo; usada para criar `timestamp` |
| `timestamp` | Datetime | Variável temporal criada a partir de `Date` e `Time` |
| `CO(GT)` | Float | Variável-alvo: concentração de monóxido de carbono |
| `PT08.S1(CO)` | Float | Leitura do sensor relacionada com CO |
| `NMHC(GT)` | Float | Medição de hidrocarbonetos não metânicos; elevada percentagem de missing values |
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
| `Unnamed: 15` | Removido | Coluna vazia removida na limpeza |
| `Unnamed: 16` | Removido | Coluna vazia removida na limpeza |


## 5. Conclusões da Fase de Exploração

A fase de exploração permitiu compreender melhor a estrutura e a qualidade do dataset, indo além da descrição inicial apresentada no Milestone 1. Em particular, foi possível confirmar que:

- o dataset é constituído maioritariamente por variáveis numéricas contínuas;
- existem problemas de qualidade dos dados, nomeadamente valores em falta codificados como `-200` e colunas totalmente vazias;
- a variável-alvo `CO(GT)` apresenta uma distribuição que exige atenção na fase de modelação;
- algumas variáveis poderão revelar maior utilidade preditiva do que outras, com base na análise de correlação;
- a criação da variável `timestamp` melhora a representação temporal dos registos e abre espaço para novas variáveis derivadas.

De forma geral, os dados apresentam qualidade suficiente para avançar para a fase seguinte, desde que sejam concluídas as etapas de tratamento de missing values, análise de outliers, eventual seleção de atributos e preparação final do dataset para treino dos modelos.

---

*Data de última atualização: [DD/MM/AAAA]*
