# Renewable Energy Finance: A Data Analytics Exploration

An end-to-end data analytics project examining the intersection of renewable energy growth,
cost trends, and financial market performance across investment flows, levelized cost of
energy, country-level generation, and clean energy stock returns.

---

## Sections

| Section | Description |
|---|---|
| 1. Setup and Data Loading | Loads all five datasets; explains what each measures and why it was chosen |
| 2. Global Investment Trends | Annual clean energy investment growth (2004-2023) alongside solar and wind generation |
| 3. LCOE Cost Revolution | Levelized cost decline curves for solar PV, wind, and natural gas (2010-2023) |
| 4. Country-Level Analysis | Interactive choropleth map, top-20 generation leaders, renewables share vs. GDP scatter |
| 5. Clean Energy Stocks | Normalized performance, annual returns heatmap, rolling correlation vs. fossil fuel ETF |
| 6. Correlations and Insights | Cross-variable Pearson correlation matrix with five quantified takeaways |
| 7. Conclusions | Summary findings and suggested next steps |

---

## Datasets

All datasets are free and publicly available. Static datasets are bundled in the `data/`
folder. Dynamic datasets (World Bank, Yahoo Finance) are fetched on first run and cached
as CSV files in `data/` for all subsequent runs — no re-downloading needed.

### 1. Our World in Data - Energy (`data/owid-energy.csv`)

- **Source:** https://github.com/owid/energy-data
- **Direct CSV link:** https://raw.githubusercontent.com/owid/energy-data/master/owid-energy-data.csv
- **Coverage:** 200+ countries, 1965-2023, 130 columns
- **Key columns used:**
  - `solar_electricity`, `wind_electricity`, `hydro_electricity`, `other_renewable_electricity` — generation in TWh
  - `renewables_share_elec` — renewables as % of electricity mix
  - `renewables_electricity` — total renewables generation (TWh)
  - `iso_code` — ISO 3-letter country code (enables choropleth maps)
  - `gdp`, `population` — for per-capita calculations


### 2. IEA World Energy Investment (`data/iea_investment.csv`)

- **Source:** IEA World Energy Investment 2024 report
- **Report link:** https://www.iea.org/reports/world-energy-investment
- **Coverage:** Global, 2004-2023
- **Columns:** `year`, `investment_bn` (USD billions), `source`


### 3. IRENA Renewable Power Generation Costs (`data/irena_lcoe.csv`)

- **Source:** IRENA Renewable Power Generation Costs 2023 edition
- **Report link:** https://www.irena.org/Publications/2024/Sep/Renewable-Power-Generation-Costs-in-2023
- **Coverage:** Global weighted averages, 2010-2023
- **Columns:** `year`, `solar_pv_utility_usd_mwh`, `onshore_wind_usd_mwh`, `natural_gas_ccgt_usd_mwh`, `source`


### 4. World Bank GDP per Capita (`data/worldbank_gdp.csv`)

- **Source:** World Bank Open Data — indicator `NY.GDP.PCAP.KD`
- **Indicator page:** https://data.worldbank.org/indicator/NY.GDP.PCAP.KD
- **Coverage:** 200+ countries, 2000-2023
- **Columns:** `iso_code`, `wb_country`, `year`, `gdp_per_capita` (constant 2015 USD)
- **Access:** Fetched automatically via the `wbgapi` Python library on first run and cached
  as `data/worldbank_gdp.csv`.


### 5. Yahoo Finance Stock Prices (`data/stock_prices.csv`)

- **Source:** Yahoo Finance via the `yfinance` Python library
- **Coverage:** 2019-01-01 to 2024-12-31, daily adjusted closing prices
- **Columns:** `Date` (index), `ICLN`, `XLE`, `SPY`, `NEE`, `ENPH`, `FSLR`, `SEDG`
- **Access:** Fetched automatically via `yfinance` on first run and cached as `data/stock_prices.csv`.
- **Tickers:**

  | Ticker | Name | Role in analysis |
  |---|---|---|
  | ICLN | iShares Global Clean Energy ETF | Clean energy benchmark |
  | XLE | Energy Select Sector SPDR ETF | Fossil fuel benchmark |
  | SPY | S&P 500 ETF | Broad market benchmark |
  | NEE | NextEra Energy | Largest US clean utility |
  | ENPH | Enphase Energy | Solar microinverters |
  | FSLR | First Solar | US solar panel manufacturer |
  | SEDG | SolarEdge Technologies | Solar inverters |


---

## Project Structure

```
renewable-energy-finance/
├── notebook.ipynb              # Main analysis notebook (fully executed with outputs)
├── generate_notebook.py        # Script that generates notebook.ipynb via nbformat
├── requirements.txt            # Python dependencies
├── README.md
└── data/
    ├── owid-energy.csv         # Bundled: OWID energy dataset (~9 MB)
    ├── iea_investment.csv      # Bundled: IEA global clean energy investment
    ├── irena_lcoe.csv          # Bundled: IRENA levelized cost of energy
    ├── worldbank_gdp.csv       # Auto-generated on first run (World Bank GDP)
    ├── stock_prices.csv        # Auto-generated on first run (Yahoo Finance prices)
    ├── sec2_investment.png
    ├── sec3_lcoe.png
    ├── sec4_map.html           # Interactive Plotly choropleth map
    ├── sec4_countries.png
    ├── sec5_stocks.png
    ├── sec5_heatmap.png
    ├── sec5_rolling_corr.png
    └── sec6_corr.png
```

---

## Setup and Installation

**Requirements:** Python 3.9 or higher

1. Clone the repository:
   ```bash
   git clone https://github.com/kbpate10/renewable-energy-finance.git
   cd renewable-energy-finance
   ```

2. Install dependencies:
   ```bash
   pip install -r requirements.txt
   ```

3. Launch the notebook:
   ```bash
   jupyter notebook notebook.ipynb
   ```

On first run, the notebook fetches World Bank GDP data (`wbgapi`) and stock prices (`yfinance`)
and saves them as CSV files in `data/`. All subsequent runs load from the local cache.
The OWID dataset, IEA investment data, and IRENA LCOE data are bundled in the repository
and require no network access.

---

## Key Findings

- Global clean energy investment grew approximately 16x from $40 billion (2004) to $651 billion (2023).
- Solar PV LCOE fell roughly 88% between 2010 and 2023, from $378/MWh to $44/MWh.
- Global solar electricity generation grew over 100x between 2010 and 2023.
- Despite the physical buildout, clean energy ETFs (ICLN) underperformed the S&P 500 from
  2019 to 2024, largely due to interest rate sensitivity in capital-intensive projects.
- Onshore wind LCOE dropped approximately 68% since 2010 and is now among the cheapest
  sources of new electricity generation in most markets.

---

## Suggested Extensions

- Regression model to quantify the solar learning curve (LCOE vs. cumulative capacity)
- K-means clustering to group countries by energy transition stage
- Green bonds market analysis using [Climate Bonds Initiative](https://www.climatebonds.net/resources/reports) data
- Carbon price impact using EU ETS data from [Ember](https://ember-climate.org/data/)
- ESG fund flow analysis for a deeper finance-sustainability link

---

## License

This project is open source under the [MIT License](LICENSE).
