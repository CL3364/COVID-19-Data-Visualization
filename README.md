# COVID-19 Vaccines and Pharmaceutical Stock Performance

An exploratory data analysis on whether the development and rollout of COVID-19 vaccines produced measurable differences in the stock market performance of vaccine-manufacturing pharmaceutical companies relative to non-vaccine-manufacturing peers, over 2020–2021.

---

## Question

Did the companies that developed COVID-19 vaccines see different stock-price trajectories from other major pharmaceutical companies during the pandemic, and if so, when did the divergence appear?

## Approach

Two complementary notebooks:

1. **Per-company analysis** ([notebooks/per_company_analysis.ipynb](notebooks/per_company_analysis.ipynb)) — cleans and aligns 17 pharma stocks, plots individual price trajectories across 2020–2021, and compares volatility / drawdown patterns.
2. **Vaccine vs. control** ([notebooks/vaccine_vs_control.ipynb](notebooks/vaccine_vs_control.ipynb)) — splits the 17 companies into a vaccine cohort and a non-vaccine (control) cohort, averages monthly highs within each cohort, and plots the difference to isolate the vaccine-specific price movement.

### Cohorts

| Cohort | Companies |
|---|---|
| Vaccine makers (6) | AstraZeneca, BioNTech, Johnson & Johnson, Moderna, Pfizer, Zhifei |
| Non-vaccine control (4) | AbbVie, Bayer, Bristol Myers Squibb, Merck |
| Other pharma (7) | Amgen, Eli Lilly, GSK, Gilead, Roche, Sanofi, Takeda |

---

## Repository Structure

```
COVID-19-Data-Visualization/
│
├── README.md
│
├── data/                              # raw stock CSVs (2020–2021)
│   ├── AbbVie_stock.csv
│   ├── Amgen_stock.csv
│   ├── AstraZeneca_stock.csv
│   ├── Bayer_stock.csv
│   ├── BioNTech_stock.csv
│   ├── BristolMyersSquibb_stock.csv
│   ├── EliLilly_stock.csv
│   ├── GSK_stock.csv
│   ├── Gilead_stock.csv
│   ├── JNJ_stock.csv
│   ├── Merck_stock.csv
│   ├── Moderna_stock.csv
│   ├── Pfizer_stock.csv
│   ├── Roche_stock.csv
│   ├── Sanofi_stock.csv
│   ├── Takeda_stock.csv
│   └── Zhifei_stock.csv
│
└── notebooks/
    ├── per_company_analysis.ipynb     # individual stocks, 2020–2021
    └── vaccine_vs_control.ipynb       # vaccine cohort vs non-vaccine cohort (averaged)
```

Each CSV has `Date`, `Open`, `High`, `Low`, `Close`, `Adj Close`, `Volume` columns (standard Yahoo Finance format) for 2020-01 through 2021-12.

---

## Data preparation (summary)

- Rows where any column is null are dropped.
- Price columns are cast to float after stripping `$` / `,` symbols.
- Analysis window is constrained to 2020–2021 (`df['Date'].dt.year` filter).
- Cohort averages are computed at monthly resolution on the `High` column to reduce intra-day noise.

---

## Running locally

The notebooks were originally written in Google Colab (they include `drive.mount(...)` cells that can be removed or skipped when running locally).

```bash
pip install pandas numpy matplotlib seaborn scipy
jupyter notebook notebooks/per_company_analysis.ipynb
```

Stock CSVs load from `../data/<name>_stock.csv` relative to the notebook.

---

## Author

**Caleb Lee** — data analysis, visualization

---

## Notes

This is an exploratory analysis; it does not claim causal identification. Many confounding events (broader market moves, earnings announcements, unrelated regulatory news) overlap the vaccine rollout window and would need to be controlled for in a formal study.
