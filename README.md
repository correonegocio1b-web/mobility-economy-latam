# Urban Mobility vs Economic Productivity — Latin American Cities

**Tools:** Python · pandas · NumPy · seaborn · matplotlib · Jupyter

Analysis of whether traffic congestion relates to economic productivity across major Latin American cities, built to answer a concrete question: **where should transport infrastructure investment be prioritized?**

Data sources: TomTom Traffic Index (1,004,464 raw traffic records) and OECD Cities economic indicators. Final merged dataset: 15 cities across 7 countries (Argentina, Brazil, Chile, Colombia, Mexico, Peru, Uruguay), 2024.

---

## Key findings

**There is no clear relationship between GDP per capita and congestion.** Cities with similar income levels show widely different congestion levels, meaning higher economic output neither causes nor prevents traffic delays. GDP per capita alone is not a useful signal for prioritizing infrastructure spending.

**Mexico City records the highest average congestion delay** of all cities analyzed, ahead of Tokyo, New York, London and Manila in the global dataset. Latin America's largest metros face congestion comparable to the world's major cities.

**Open hypothesis for future work:** city size and population density may explain congestion better than income. Density was not available in this dataset and was not tested here.

---

## Data preparation

The two sources arrived in incompatible formats and required significant cleaning before they could be joined:

| Issue | Action |
|---|---|
| Date columns stored as text | Converted to `datetime` with `errors='coerce'` |
| GDP, unemployment, PM2.5 and population stored as text with thousand separators, decimal commas and `%` symbols | Stripped symbols, normalized decimal separator, cast to float |
| Inconsistent column naming between sources | Standardized to `snake_case` |
| Multiple traffic records per city | Aggregated to city–year averages across seven traffic metrics |
| No year column in traffic data | Derived from timestamp, filtered to 2024 |

Join: INNER on `city` and `year`, keeping only cities present in both sources.

---

## Methodology

1. Load and inspect both datasets (structure, types, nulls)
2. Standardize column names and fix numeric and date formats
3. Extract year and filter to 2024
4. Aggregate traffic metrics to city–year level
5. Merge mobility and economic indicators
6. Visual analysis: boxplot for congestion distribution, histogram for GDP per capita, comparative bar chart by city
7. Export clean dataset and document findings

A note on the visualization: GDP per capita and congestion delay sit on very different scales, which makes a shared-axis comparison misleading. The analysis flags this and recommends normalizing or plotting separately.

---

## Repository contents

- `mobility-economy-analysis.ipynb` — full analysis notebook (written in Spanish)
- `ladb_mobility_economy_2024_clean.csv` — cleaned, merged output dataset
- `datasets/` — source data

---

*Completed as part of the TripleTen Data Analytics program. Reviewed and approved.*
