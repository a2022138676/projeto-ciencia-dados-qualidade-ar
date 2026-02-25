# projeto-ciencia-dados-qualidade-ar
# Projeto de Ciência de Dados — Qualidade do Ar (AirQualityUCI)

## Identificação da Equipa
* **Grupo nº:** [11]
* **Membros:**
  * **Tiago Rodrigues** - [a2022138676]
  * **Rodrigo Pedro** - [a2023]

---
## Organização do Portfólio de Resultados

Este repositório funciona como uma **Wiki de Projeto**, documentando as decisões, entregáveis e resultados obtidos ao longo das milestones, sem exposição de dados sensíveis ou código proprietário.

* **`milestones/`**: Documentação técnica detalhada de cada etapa do projeto (M1, M2, M3 e M4).
* **`assets/`**: Repositório de evidências visuais, dividido em `graficos/`, `diagramas/` e `tabelas/`.
* **`.gitignore`**: Filtro de segurança que impede a submissão acidental de dados brutos, ficheiros temporários ou scripts não destinados ao repositório público.

> **Nota:** Durante a Milestone 1, a estrutura poderá estar em fase inicial e algumas pastas/ficheiros poderão ser adicionados progressivamente.

---
## 1. Iniciação (Milestone 1)

### Contexto e Problema de Negócio
O projeto centra-se na **monitorização da qualidade do ar**, um tema com elevada relevância na **saúde pública**, **gestão ambiental** e **planeamento urbano**. A poluição atmosférica afeta diretamente a qualidade de vida da população e pode apoiar decisões relacionadas com prevenção, monitorização e políticas ambientais.

O dataset selecionado (**AirQualityUCI**) contém medições horárias de poluentes (ex.: `CO(GT)`, `NOx(GT)`, `NO2(GT)`), leituras de sensores químicos (`PT08.*`) e variáveis meteorológicas (`T`, `RH`, `AH`). Este conjunto de dados permite estudar padrões temporais, relações entre variáveis e, em fases posteriores, desenvolver modelos de regressão para previsão de variáveis-alvo de qualidade do ar.

### Objetivos do Projeto
* **Objetivo 1:** Construir um pipeline de preparação de dados reprodutível (tratamento de `Date` + `Time`, remoção de colunas/linhas vazias e substituição de `-200` por `NaN`).
* **Objetivo 2:** Realizar análise exploratória (EDA) e identificar padrões horários/diários, correlações entre sensores/poluentes e relações com variáveis meteorológicas.
* **Objetivo 3:** Desenvolver e comparar modelos de regressão para prever uma variável-alvo de qualidade do ar (ex.: `CO(GT)` ou `NO2(GT)`).

**[Consulta a Documentação Completa do Milestone 1](milestones/M1_iniciacao.md)**

---
## 2. Exploração (Milestone 2)

### Principais Conclusões (EDA)
> *Dica: Insere aqui o gráfico mais importante do projeto que resume a tua descoberta principal.*  
> ![Gráfico de Destaque](assets/graficos/insight_principal.png)

* **Conclusão Chave (prevista):** Espera-se identificar padrões temporais nas concentrações de poluentes (por hora/dia), bem como relações relevantes entre variáveis meteorológicas e leituras dos sensores.
* **Qualidade dos dados (prevista):** Será documentado o impacto dos valores inválidos (`-200`) e a estratégia de tratamento adotada.
* **Resultado esperado:** EDA com visualizações e conclusões técnicas que suportem a fase de modelação.

**[Consulta a Documentação Completa do Milestone 2](milestones/M2_exploracao.md)**

---
## 3. Modelação (Milestone 3)

### Desempenho do Modelo
| Modelo | Métrica (RMSE) | Tempo de Treino |
| :--- | :--- | :--- |
| Baseline (média histórica) | [a preencher] | [a preencher] |
| Regressão Linear | [a preencher] | [a preencher] |
| Random Forest Regressor | [a preencher] | [a preencher] |
| **Modelo Final** | **[a preencher]** | **[a preencher]** |

* **Nota:** O modelo final será selecionado com base no desempenho em métricas de regressão (**MAE, RMSE e R²**) e no equilíbrio entre precisão, robustez e capacidade de generalização.

**[Consulta a Documentação Completa do Milestone 3](milestones/M3_modelacao.md)**

---
## 4. Finalização (Milestone 4)

### Resposta ao Problema
Os resultados finais irão responder à questão inicial da Milestone 1, demonstrando de que forma a análise exploratória e os modelos desenvolvidos permitem compreender e prever variáveis de qualidade do ar no dataset **AirQualityUCI**.

O impacto prático da solução será discutido em termos de:
- apoio à monitorização ambiental;
- identificação de padrões relevantes de poluição;
- potencial de utilização em contextos académicos e de prototipagem de sistemas de apoio à decisão.

### Recomendações e Inovação
1. Propor melhorias no pipeline de preparação de dados (ex.: estratégias de imputação e seleção de variáveis).
2. Explorar modelos adicionais e validação temporal mais rigorosa para séries temporais.
3. Criar visualizações interativas ou dashboard para acompanhamento dos resultados.
4. Avaliar a possibilidade de automatizar alertas com base em previsões futuras (trabalho futuro).

**[Consulta a Documentação Completa do Milestone 4](milestones/M4_finalizacao.md)**

---
**Instituição:** Coimbra Business School | ISCAC  
**Curso:** Licenciatura em Ciência de Dados para a Gestão  
**Unidade Curricular:** Projeto em Ciência de Dados  
**Professor Responsável:** Dora Melo (dmelo@iscac.pt)

## Nota de Confidencialidade
Este repositório foi construído exclusivamente para fins de **portfólio e documentação de
resultados**. Por questões de proteção de dados e propriedade intelectual, este repositório **não
contém**:
1. Dados brutos (datasets originais).
2. Código-fonte proprietário da implementação.
3. Informação sensível de clientes ou parceiros. 
