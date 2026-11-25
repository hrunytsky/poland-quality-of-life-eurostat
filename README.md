
# How Has Quality of Life Changed in Poland?

A data project comparing Poland's quality of life with the rest of the European Union (EU27) over the last two decades. Data is pulled directly from the **Eurostat** API with Python, cleaned into a single analysis-ready table, and visualised in an interactive **Tableau** dashboard.

## Project overview

The goal is to show how Poland has developed since joining the EU in 2004 – in income, wages, health, labour market, safety, poverty and demographics – and how it compares with other member states and the EU27 average.

**Workflow**

1. `Data_download.ipynb` downloads nine indicators from Eurostat, harmonises them and merges them into one country–year table.
2. The table is exported to Excel (`dane_ue.xlsx`).
3. The Excel file is used as the data source for the Tableau dashboard.

## Indicators

| Column | Indicator | Eurostat dataset | Coverage (Poland) |
|---|---|---|---|
| `gdp_pc_pps` | GDP per capita, in purchasing power standards (PPS) | `nama_10_pc` | 2000–2025 |
| `min_wage_pps` | Monthly minimum wage, in PPS | `earn_mw_cur` | 2000–2026 |
| `life_expectancy` | Life expectancy at birth (years, both sexes) | `demo_mlexpec` | 2000–2024 |
| `unemployment` | Unemployment rate, ages 15–74 (% of active population) | `une_rt_a` | 2009–2025 |
| `homicides_per_100k` | Intentional homicide victims per 100,000 inhabitants | `crim_hom_soff` | 2008–2024 |
| `arop_60` | At-risk-of-poverty rate (threshold: 60% of median income, %) | `ilc_li02` | 2005–2025 |
| `pop_0_14` | Population aged 0–14 | `demo_pjanbroad` | 1995–2025 |
| `pop_15_64` | Population aged 15–64 | `demo_pjanbroad` | 1995–2025 |
| `pop_65_plus` | Population aged 65 and over | `demo_pjanbroad` | 1995–2025 |

## Output table structure

One row per country and year.

| Column | Description |
|---|---|
| `geo` | Eurostat country code (e.g. `PL`, `DE`; `EU27_2020` for the EU aggregate) |
| `country` | Country name |
| `year` | Reference year |
| *9 indicator columns* | See the table above |

## Getting started

**Requirements:** Python 3.9+ and the following packages.

```bash
pip install eurostat pandas openpyxl
```

**Run:** open `Data_download.ipynb` in Jupyter and run all cells. The notebook creates `eu_data.xlsx` in the working directory. An internet connection is required.

## Data processing notes

- **Country scope:** all 27 EU member states plus the EU27 aggregate (`EU27_2020`) where Eurostat provides it. The EU27 aggregate is not available for the minimum wage (`earn_mw_cur`) and homicide (`crim_hom_soff`) datasets.
- **Semi-annual data:** minimum wage data is published twice a year (S1/S2); it is averaged to a yearly value.
- **Uniqueness check:** the code asserts that after filtering there is exactly one value per country and period, so a change in a Eurostat dataset structure fails loudly instead of silently producing duplicates.
- **Missing values:** indicators have different start years and some countries have gaps; missing values are left empty rather than imputed.
- **PPS:** values in purchasing power standards allow comparisons between countries by removing price-level differences.

## Data source

[Eurostat](https://ec.europa.eu/eurostat) – the statistical office of the European Union. Data is accessed with the [`eurostat`](https://pypi.org/project/eurostat/) Python package. Please check Eurostat's [copyright notice](https://ec.europa.eu/eurostat/about-us/policies/copyright) before reusing the data.

## Tools

Python · pandas · Eurostat API · Tableau