# Milestone 1: Iniciação e Definição do Projeto

## 1. Descrição Detalhada do Problema
Este projeto insere-se no contexto da **monitorização ambiental e da saúde pública**, com foco na **qualidade do ar** em ambiente urbano/industrial. A poluição atmosférica tem impacto direto na saúde humana, na qualidade de vida e no planeamento de políticas públicas, sendo por isso um tema atual e relevante para análise de dados.

O dataset **AirQualityUCI** contém medições horárias de poluentes (ex.: CO, NOx, NO2), respostas de sensores químicos e variáveis meteorológicas (temperatura, humidade relativa e humidade absoluta). Este conjunto de dados permite estudar relações entre variáveis ambientais e construir modelos preditivos para apoiar a monitorização da qualidade do ar.

### Problema a resolver
Pretende-se analisar e preparar os dados para:
- compreender padrões temporais nas medições de qualidade do ar;
- identificar problemas de qualidade dos dados (valores em falta, inconsistências e codificações especiais);
- desenvolver, em fases posteriores, modelos preditivos (regressão) para estimar concentrações de poluentes com base nas restantes variáveis.

### Relevância atual
A monitorização da qualidade do ar é uma área crítica em:
- **cidades inteligentes (smart cities)**;
- **saúde pública**;
- **gestão ambiental**;
- **sistemas de alerta e prevenção**.

Além disso, este problema é adequado ao contexto académico da unidade curricular, por permitir aplicar várias etapas do ciclo de ciência de dados (CRISP-DM): compreensão do problema, compreensão dos dados, preparação, modelação e avaliação.

---

## 2. Objetivos SMART
*Definir os objetivos do projeto segundo a lógica SMART (Específico, Mensurável, Atingível, Relevante e Temporal):*

1. **Objetivo 1 (Preparação e Qualidade dos Dados):**  
   Até ao final da **Milestone 2**, construir um pipeline de preparação de dados reprodutível que:
   - converta corretamente `Date` + `Time` para um timestamp;
   - trate valores inválidos codificados como `-200`;
   - remova colunas/linhas vazias do ficheiro CSV;
   - produza um dataset limpo e documentado para modelação.

2. **Objetivo 2 (Análise Exploratória):**  
   Até ao final da **Milestone 2**, identificar e documentar **pelo menos 5 padrões relevantes** nos dados (ex.: padrões horários, diários, correlações entre sensores e poluentes, comportamento sazonal), com visualizações e respetiva interpretação.

3. **Objetivo 3 (Modelação Preditiva):**  
   Até ao final da **Milestone 3**, desenvolver e comparar **pelo menos 3 modelos de regressão** para prever uma variável-alvo de qualidade do ar (ex.: `CO(GT)` ou `NO2(GT)`), obtendo uma melhoria de **pelo menos 15% em MAE/RMSE** face a um modelo de referência (linha de base) simples, como a média histórica ou um baseline temporal.

### Métricas de Sucesso (proposta)
- **Regressão:** MAE, RMSE, R²
- **Qualidade do pipeline:** dataset limpo, reproduzível e notebook executável sem erros
- **Documentação:** resultados e decisões registados na pasta `docs/`

---

## 3. Metodologia de Gestão (PBL)

### Divisão de Tarefas
Como a equipa é constituída por **2 elementos**, as responsabilidades serão distribuídas de forma complementar, garantindo que ambos participam nas várias fases do projeto.

- **Tiago Rodrigues:** Responsável principal pela **Engenharia de Dados e Preparação**
  - carregamento dos ficheiros (CSV/XLSX);
  - limpeza inicial dos dados;
  - tratamento de valores inválidos (`-200`);
  - transformação de `Date` + `Time` para timestamp;
  - preparação do dataset para análise exploratória e modelação.

- **Rodrigo Pedro:** Responsável principal pela **Análise Exploratória, Modelação e Documentação**
  - estatística descritiva e visualizações;
  - análise de correlações e padrões temporais;
  - construção e avaliação de modelos de referência e modelos de regressão;
  - atualização de `README.md` e `docs/M1_iniciacao.md`;
  - apoio à preparação da apresentação final.

### Trabalho Colaborativo (responsabilidade partilhada)
Ambos os elementos participarão em:
- definição dos objetivos SMART;
- formulação das perguntas de investigação;
- interpretação dos resultados;
- revisão final dos notebooks e da documentação;
- apresentação do projeto.

### Ferramentas de Colaboração
- **GitHub** (repositório, controlo de versões e histórico de commits)
- **GitHub Projects / Issues** (gestão de tarefas / Kanban)
- **Teams / Discord / WhatsApp** (comunicação e reuniões)
- **Kaggle Notebooks** (exploração inicial e prototipagem)
- **Python + Jupyter** (análise e modelação)

### Regras internas (boas práticas)
- Ambos os membros devem realizar commits regulares.
- Utilizar mensagens de commit descritivas (`docs:`, `feat:`, `fix:`, `chore:`).
- Registar decisões importantes na pasta `docs/`.
- Validar em conjunto as conclusões antes de cada entrega.

---

## 4. Análise de Viabilidade dos Dados

### Disponibilidade
- Os dados já foram descarregados e estão disponíveis em **dois formatos**:
  - `AirQualityUCI.csv`
  - `AirQualityUCI.xlsx`
- O ficheiro **XLSX** apresenta-se mais limpo para iniciar a exploração.
- O ficheiro **CSV** é útil para treino do pipeline de ingestão, mas exige parsing específico (`sep=';'`, `decimal=','`).

### Qualidade Inicial
Com base na inspeção preliminar realizada:
- O dataset útil contém **9357 observações** e **15 variáveis** (após limpeza do CSV).
- O ficheiro CSV inclui:
  - **2 colunas vazias extra** (ex.: `Unnamed: 15`, `Unnamed: 16`);
  - **linhas vazias no final** (a remover).
- Existem valores inválidos codificados como **`-200`**, que representam **valores em falta** e devem ser convertidos para `NaN`.
- A coluna **`NMHC(GT)`** apresenta uma percentagem muito elevada de valores em falta (~90%), podendo exigir:
  - exclusão da variável; ou
  - tratamento específico (a decidir na M2).
- `Date` e `Time` estão separados e necessitam de ser combinados numa coluna temporal única para análise de séries temporais.

### Ética
- O dataset contém **medições ambientais** e **não inclui dados pessoais**, pelo que o risco de incumprimento do **RGPD** é **muito reduzido**.
- Não existe identificação direta de indivíduos.
- Mesmo sem dados pessoais, serão seguidas boas práticas:
  - referência à origem do dataset;
  - utilização exclusivamente académica;
  - documentação transparente das transformações e limitações.
- Limitações éticas/técnicas a considerar:
  - os resultados podem não generalizar para outras cidades/períodos;
  - possíveis erros ou ruído dos sensores podem influenciar as conclusões.

---

## 5. Cronograma Interno

> **Nota:** Ajustar as datas ao calendário oficial da turma/UC. Abaixo segue uma proposta inicial.

| Fase | Data Limite | Entregável Esperado |
| :--- | :--- | :--- |
| M1: Iniciação | 24/02/2026 | Repositório estruturado, plano de projeto e definição inicial do problema. |
| M2: Exploração | 17/03/2026 | Notebook de EDA, tratamento inicial dos dados e observações documentadas. |
| M3: Modelação | 21/04/2026 | Comparação de algoritmos de regressão e avaliação com métricas (MAE/RMSE/R²). |
| M4: Finalização | 19/05/2026 | Pitch, relatório final e versão final do repositório. |

---

## (Opcional) Perguntas de Investigação
1. Quais são os padrões horários e diários mais evidentes nas concentrações de poluentes?
2. Que variáveis (sensores e meteorologia) apresentam maior relação com `CO(GT)` e `NO2(GT)`?
3. É possível prever a concentração de um poluente com desempenho significativamente superior a um modelo de referência simples?
4. O tratamento de valores `-200` melhora, de forma mensurável, o desempenho dos modelos?

---

*Data da última atualização: 25/02/2026*
