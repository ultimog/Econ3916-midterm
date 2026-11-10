# Econ3916-midterm
# Does higher government debt go with slower growth the next year?

Income growth and general government debt across 191 economies, 2014-2023.
[Open the notebook in Colab](https://colab.research.google.com/drive/1x4o7eZhR-ERw851Waq1ZkcAi4fqPgjfg?usp=sharing) · [Report (PDF)](Midterm_Report.pdf)

## Question

Across 191 economies from 2014 to 2023, is higher general government gross debt (% of GDP) in the previous year associated with slower growth in real income per person, holding last year's income and each country and each year fixed?

## Hypothesis

Heavy debt should slow growth, through higher interest costs and less room for private borrowing and investment, so I expected a negative coefficient on previous-year debt.

## Data

| File | Source | What it holds |
|---|---|---|
| `data/imf_weo.csv` | [IMF Data Explorer, World Economic Outlook, version 9.0.0 (October 2026)](https://data.imf.org/en/Data-Explorer?datasetUrn=IMF.RES:WEO(9.0.0)) | the whole WEO database: 8,202 rows and 79 columns, one row per economy and indicator, one column per year (1980 to 2031) |

I use three indicators from it: general government gross debt, % of GDP (`GGXWDG_NGDP`); real GDP per person in constant 2021 international dollars (`NGDPRPPPPC`); and gross capital formation, % of GDP (`NID_NGDP`). The file was downloaded on 2026-11-02. The notebook drops the IMF's regional and group rows, reshapes the years into one row per economy-year, and builds growth, last year's income and last year's debt from the income and debt columns.

## How to run

1. Open the notebook in Colab (link above). It is saved in this repository as `Midterm Project/Econ_3916_Midterm.ipynb`.
2. The data cell reads the file through `DATA_PATH`. Set it to `https://raw.githubusercontent.com/YOURNAME/YOURREPO/main/data/imf_weo.csv`, or upload `data/imf_weo.csv` to the Colab session and use `imf_weo.csv`.
3. Run **Runtime > Restart and run all**. The notebook needs `pandas`, `numpy`, `matplotlib` and `statsmodels`, which Colab already has.

Every number in the report is printed by the notebook's last code cell, "Numbers my report quotes".

## Method

OLS of yearly income-per-person growth on previous-year debt and the log of previous-year income, with country and year dummies. Standard errors are clustered by country, with t-based intervals. Investment, same-year debt, a sample without 2020 and 2021, and a sample of 2014-2019 only are run as checks.

## Finding

An economy-year that follows a year with debt 10 points of GDP higher has income growth 0.20 percentage points higher (coefficient +0.020 per point; 95% CI -0.011 to +0.051; N = 1,901 economy-years, 191 economies). The interval includes zero, so the data cannot tell this from no relationship, and my hypothesis of a negative sign is not supported. The estimate shrinks toward zero without the pandemic years (+0.010 without 2020 and 2021; +0.001 on 2014-2019 only). With same-year debt the sign reverses (-0.063), which mostly reflects growth moving the debt ratio, because GDP is in the denominator. This is a conditional within-country association, not a causal effect.

## Files

- `data/imf_weo.csv`: the IMF data
- `Midterm Project/Econ_3916_Midterm.ipynb`: the analysis
- `Midterm_Report.pdf`: the written report

