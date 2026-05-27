# Renewable Energy Finance: A Data Analytics Exploration

An end-to-end data analytics project examining the intersection of renewable energy growth,
cost trends, and financial market performance. The analysis spans investment flows, levelized
cost of energy, country-level generation, and clean energy stock returns.

---

## Sections

| Section | Description |
|---|---|
| 1. Setup and Data Loading | Downloads and prepares all datasets |
| 2. Global Investment Trends | Annual clean energy investment growth (2004-2023) alongside solar and wind generation |
| 3. LCOE Cost Revolution | Levelized cost decline curves for solar PV, wind, and natural gas (2010-2023) |
| 4. Country-Level Analysis | Interactive choropleth map, top-20 generation leaders, and renewables share vs. GDP scatter |
| 5. Clean Energy Stocks | Normalized performance, annual returns heatmap, and rolling correlation vs. fossil fuel ETF |
| 6. Correlations and Insights | Cross-variable Pearson correlation matrix with quantified takeaways |
| 7. Conclusions | Summary findings and suggested next steps |

---

## Datasets

All datasets are free and publicly available.

| Source | Coverage | Access |
|---|---|---|
| [Our World in Data - Energy](https://github.com/owid/energy-data) | Electricity generation by source, renewables share, 200+ countries, 1965-2023 | Auto-downloaded on first run |
| [IEA World Energy Investment](https://www.iea.org/reports/world-energy-investment) | Global clean energy investment in USD billions, 2004-2023 | Hardcoded from published reports |
| [IRENA Renewable Power Generation Costs](https://www.irena.org/Publications/2024/Sep/Renewable-Power-Generation-Costs-in-2023) | Levelized cost of energy by technology, 2010-2023 | Hardcoded from published reports |
| [World Bank Open Data](https://data.worldbank.org/) | GDP per capita by country | Fetched via `wbgapi` Python library |
| [Yahoo Finance](https://finance.yahoo.com/) | Daily stock prices for clean energy ETFs and individual companies | Fetched via `yfinance` Python library |

---

## Tickers Analyzed

| Ticker | Name |
|---|---|
| ICLN | iShares Global Clean Energy ETF |
| XLE | Energy Select Sector SPDR (fossil fuel benchmark) |
| SPY | S&P 500 ETF (market benchmark) |
| NEE | NextEra Energy |
| ENPH | Enphase Energy |
| FSLR | First Solar |
| SEDG | SolarEdge Technologies |

---

## Project Structure

```
renewable-energy-finance/
├── notebook.ipynb          # Main analysis notebook (fully executed)
├── generate_notebook.py    # Script that generates notebook.ipynb via nbformat
├── requirements.txt        # Python dependencies
└── data/
    ├── owid-energy.csv     # Cached OWID dataset (auto-downloaded on first run)
    ├── sec2_investment.png
    ├── sec3_lcoe.png
    ├── sec4_map.html       # Interactive Plotly choropleth map
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

The OWID energy dataset (~9 MB) is downloaded automatically on the first run and cached in the
`data/` folder. All subsequent runs use the local cache.

---

## Key Findings

- Global clean energy investment grew approximately 16x from $40 billion (2004) to $651 billion (2023).
- Solar PV levelized cost fell roughly 88% between 2010 and 2023, from $378/MWh to $44/MWh.
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

---

## License

This project is open source under the [MIT License](LICENSE).
