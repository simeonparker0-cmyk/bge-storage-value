# BGE Zone Price Analysis (2025)

How did 2025 wholesale electricity prices in the BGE zone (central Maryland) compare with PJM's Western Hub, and how much of the difference came from transmission congestion versus losses?

**Status:** Version 0.1. This is the first project in a self-directed curriculum in Python data analysis for energy markets. A follow-on version will estimate the arbitrage value of a 4-hour battery in the BGE zone and separate the share attributable to local congestion.

## Findings

1. [Finding on the BGE vs. Western Hub premium: size and congestion/loss split]
2. [Finding on day-ahead vs. real-time prices at BGE]
3. [Optional third finding]

## Data

Source: PJM Data Miner 2 (dataminer2.pjm.com), downloaded manually on [dates].

- Day-ahead hourly LMPs (`da_hrl_lmps`) and real-time hourly LMPs (`rt_hrl_lmps`)
- Nodes: BGE (zone, pnode ID [ID]) and WESTERN HUB (hub, pnode ID [ID])
- Period: January 1 to December 31, 2025, all 8,760 hours
- Filtered by Pnode Name. Filtering by Zone returns every pricing node inside the zone.
- The date range must run through the end of December 31. Ending at "12/31/2025" returns only the first hour of that day.

Raw files go in `data/raw/` and are not tracked in Git. Re-download using the settings above.

## Method

- Loaded each file with explicit timestamp formats, kept only current rows, and indexed on UTC. Eastern time is kept for labels only, because daylight saving time makes one Eastern hour repeat in November and one disappear in March.
- Validated each file with assert checks: 8,760 rows per node and market, no duplicate timestamps, no missing prices.
- Combined all four series into one long table and checked that energy + congestion + losses = LMP in every hour, and that the energy component is identical at both nodes. Since energy is identical, the BGE-to-hub spread is entirely congestion and losses.

## Limitations

- Zone and hub prices are averages. A specific site's prices depend on its own node.
- One year of data. 2025 may not be typical.
- Descriptive analysis only; no forecasting.

## Repository structure

- `notebooks/01_load_clean.ipynb`: loading, cleaning, validation, combined table
- `notebooks/02_exhibits.ipynb`: charts
- `exhibits/`: final charts (PNG and SVG)

## How to run

Download the data as described above into `data/raw/`, then run the notebooks in order with the `BGE_LMP` conda environment (Python with pandas, matplotlib, pyarrow).