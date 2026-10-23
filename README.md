# The Global Sneaker Market

An interactive data story about where athletic shoes are made, which companies sell them, and what collectors pay for them once they sell out. Built for FIT3179 Data Visualisation 2 (Monash University), October 2026, by Aman.

**Live page:** _add your GitHub Pages link here_

## What it shows

The page is one scrolling story in three acts.

| Act | Question | Charts |
|---|---|---|
| 1. Made in Asia, bought everywhere | Where are shoes made and shipped? | Proportional symbol map, flow map, choropleth |
| 2. A few brands sell the shoes | Who earns the money? | Bump chart, treemap, Sankey diagram |
| 3. Case study of sneaker collecting: USA | What do collectors pay, and which shoes hold their value? | Bubble chart, bar chart, line chart, heatmaps, dumbbell chart |

It ends with final takeaways: a few countries make the shoes, a few companies earn the money, and a few shoes make the collectors' money.

## Data

| Source | Used for |
|---|---|
| [CEPII BACI](http://www.cepii.fr/CEPII/en/bdd_modele/bdd_modele_item.asp?id=37) world trade, 2002 to 2024 (8 footwear product codes) | Act 1 |
| Company annual reports (SEC EDGAR, HKEX, EDINET, investor sites) and [Federal Reserve G.5A](https://www.federalreserve.gov/releases/g5a/) exchange rates | Act 2 |
| StockX resale prices from the embSneakers dataset, April 2012 to July 2020 | Act 3 |
| [Natural Earth](https://www.naturalearthdata.com) country and ocean shapes (TopoJSON from the unit's [FIT3179 repository](https://github.com/FIT3179/Vega-Lite)) | Map base layers |

The raw files are very large, so they are not in this repo. Python scripts reduce them to the small files in `data/`.

## Tech stack

- **Charts:** [Vega-Lite](https://vega.github.io/vega-lite/) 5.21 for ten charts and [Vega](https://vega.github.io/vega/) 5.30 for the treemap and Sankey, embedded with vega-embed 6.26. Each chart is one JSON spec in `js/`.
- **Page:** plain HTML and CSS, laid out with [Pure.css](https://purecss.io/) grids. Fonts are Bricolage Grotesque and DM Sans from Google Fonts. Everything is loaded from CDNs, so no build step is needed.
- **Data preparation:** Python with DuckDB and pandas, in `scripts/`.
- **Hosting:** GitHub Pages.

## Run it locally

From this folder:

```
python -m http.server 8000
```

Then open <http://localhost:8000>. Opening `index.html` directly does not work, because browsers block the charts from reading the data files.

## Folder guide

```
index.html     the page
css/           styles
js/            one chart spec per file (*.vg.json)
data/          the small data files the charts read
scripts/       Python data preparation (baci_prep, company_prep, resale_prep, behaviour_prep)
```

To rebuild a data file, run its script from this folder, for example `python scripts/behaviour_prep.py "<folder with the StockX files>"`.

## Notes and limits

- StockX is one US marketplace, and its data ends in July 2020. Company figures are whole-company revenue, not footwear alone, and the company charts stop at 2024 because the firms report on different calendars, currencies and rules.
- The flow-map curves join region centres to show size and direction. They are not shipping routes.
