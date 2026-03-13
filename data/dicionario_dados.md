# Dicionário de Dados — Variáveis Criadas

Este ficheiro documenta as novas variáveis criadas durante a fase de preparação e engenharia de atributos do dataset **AirQualityUCI**.

## Variáveis Criadas

| Variável | Tipo | Origem | Descrição |
| :--- | :--- | :--- | :--- |
| `timestamp` | Datetime | `Date` + `Time` | Variável temporal criada a partir da junção da data e hora originais. |
| `hour` | Integer | `timestamp` | Hora do dia extraída de `timestamp`, utilizada para captar padrões horários. |
| `day_of_week` | Categórica | `timestamp` | Dia da semana extraído de `timestamp`, utilizado para representar diferenças entre dias. |
| `month` | Categórica | `timestamp` | Mês extraído de `timestamp`, utilizado para captar possíveis padrões sazonais. |

## Variáveis Derivadas após Encoding

Após aplicação de **One-Hot Encoding**, as variáveis categóricas `day_of_week` e `month` deram origem a novas colunas binárias.

### Colunas criadas a partir de `day_of_week`
- `day_of_week_Monday`
- `day_of_week_Saturday`
- `day_of_week_Sunday`
- `day_of_week_Thursday`
- `day_of_week_Tuesday`
- `day_of_week_Wednesday`

### Colunas criadas a partir de `month`
- `month_2`
- `month_3`
- `month_4`
- `month_5`
- `month_6`
- `month_7`
- `month_8`
- `month_9`
- `month_10`
- `month_11`
- `month_12`

## Colunas Removidas

- `NMHC(GT)` — removida devido à elevada percentagem de valores em falta.
- `Date` — removida após criação de `timestamp`.
- `Time` — removida após criação de `timestamp`.

## Nota

As colunas binárias resultantes do One-Hot Encoding assumem valores booleanos (`True`/`False`) e representam a pertença de cada observação a uma categoria específica.
