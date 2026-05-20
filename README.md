# ⚽ Premier League Dashboard — Power BI

Análise exploratória dos resultados da **Premier League entre as temporadas 2006/07 e 2016/17**, construída no Power BI Desktop com foco em tendências de gols, padrões de vitória e desempenho por temporada.

Disponível em: https://app.powerbi.com/view?r=eyJrIjoiYzg5ZmRjZjQtNDg1NC00MWY4LWIwYTAtZDYxOTVmNDllNGQ5IiwidCI6IjY1OWNlMmI4LTA3MTQtNDE5OC04YzM4LWRjOWI2MGFhYmI1NyJ9

---

## 📊 Visualizações

| Visual | Descrição |
|---|---|
| **Total de Gols por Temporada** | Gráfico de linhas mostrando a evolução do volume de gols ao longo das temporadas |
| **Maior Diferença de Gols** | Cartão KPI com o maior saldo absoluto entre mandante e visitante na(s) temporada(s) selecionada(s) |
| **Vitória da Casa × Visitante × Empate** | Gráfico de pizza com a distribuição percentual dos tipos de resultado |
| **Gols por Temporada** | Gráfico de barras empilhadas separando gols da casa, gols visitantes e empates |

**Filtro:** Segmentação por temporada (`season`), permitindo isolar qualquer período entre 2006/07 e 2016/17.

---

## Sobre os dados

A base contém os resultados de todas as partidas da Premier League no período, com as seguintes colunas originais:

| Coluna | Descrição |
|---|---|
| `home_team` | Time mandante |
| `away_team` | Time visitante |
| `FTHG` | Gols do mandante (Full Time Home Goals) |
| `FTAG` | Gols do visitante (Full Time Away Goals) |
| `FTR` | Resultado: `H` (casa), `A` (visitante), `D` (empate) |
| `season` | Temporada original no formato `2006-2007` |

### Transformações aplicadas no Power Query

- `season` foi separada em duas colunas — `season` (ano inicial) e `season_end` (ano final) — para que o Power BI interpretasse corretamente os valores como anos numéricos
- Criada a coluna `goal_difference`: diferença absoluta entre `FTHG` e `FTAG`
- Criada a coluna `result`: tradução de `FTR` para português (`Casa`, `Visitante`, `Empate`)

### Medidas DAX criadas

```
total_goals         = SUM de FTHG + FTAG
total_matches       = COUNTROWS da tabela de partidas
max_goal_difference = MAX('premier_league'[goal_difference]) na temporada selecionada
goal_avg            = AVERAGEX de gols por partida 
%home_victory       = % de partidas com FTR = 'H'
%away_victory       = % de partidas com FTR = 'A'
%draw               = % de partidas com FTR = 'D'
```

## Tecnologias

- Power BI Desktop
- Power Query (M)
- DAX

---

## Fonte dos dados

Os dados foram fornecidos como material didático do curso da EBAC - Power BI. Um dataset similar está disponível publicamente no Kaggle: https://www.kaggle.com/datasets/zaeemnalla/premier-league?select=results.csv
